# Remaining Risks

## ஆய்வு நிலை

- கண்டறிந்த check: **Step 7 — Step 1: Source Code & Theme Validation**, குறிப்பாக Diff Check மற்றும் Chat செயல்பாட்டு மாற்றங்களின் read-only regression review.
- ஒப்பீடு: `main` மற்றும் `feature/black-leather-royal-gold`.
- இவை source-level findings; device/runtime test மூலம் உறுதிப்படுத்தப்படவில்லை.
- இங்கு ஆபத்துகளை மட்டும் பதிவு செய்கிறோம். எந்த app code-மும் மாற்றப்படவில்லை.

## 1. Clear Chat நடக்கும் போது AI பதில் வந்துவிடுதல்

- **எந்த check-இல் கண்டறிந்தது:** Step 7, Step 1 — `chat.tsx`-ன் clear/history/send செயல்பாடுகளை ஒப்பிட்டபோது.
- **மீதமுள்ள ஆபத்து:** AI பதில் காத்திருக்கும் நேரத்தில் Clear Chat செய்தால், clear முடிந்த பிறகு பழைய request-ன் பதில் புதிய chat-ல் சேரலாம்; அதன் பின் அந்த நிலை history-ஆக மீண்டும் சேமிக்கப்படலாம். இது `main`-லேயே இருந்த நடத்தை; feature branch-ல் புதிதாக ஏற்பட்ட regression அல்ல.
- **சரிசெய்ய வேண்டிய கோப்பு/பகுதி:** `artifacts/tamil-ai-chat/app/chat.tsx` — `clearChat` மற்றும் `handleSend`-ன் பதில் கையாளும் பகுதி.

## 2. Special send பாதைகளில் in-flight guard இல்லாமை

- **எந்த check-இல் கண்டறிந்தது:** Step 7, Step 1 — `handleSend`-ல் சேர்க்கப்பட்ட in-flight guard மற்றும் அதன் முன் உள்ள early-return பாதைகளை ஆய்வு செய்தபோது.
- **மீதமுள்ள ஆபத்து:** `sendInFlightRef` சாதாரண AI send பாதையில் மட்டுமே அமைக்கப்படுகிறது. URL, video, photo பாதைகள் அதற்கு முன் return ஆகின்றன; அதனால் guard அவற்றை உள்ளடக்காது. மிக வேகமாகத் தொடர்ச்சியாகத் தொடங்கினால் ஒரே special action ஒன்றுக்கு மேல் செயல்பட வாய்ப்பு உள்ளது. இந்தப் பாதைகள் `main`-லிருந்து மாற்றப்படவில்லை; புதிதாக அறிமுகமான regression என்று உறுதிப்படுத்தப்படவில்லை.
- **சரிசெய்ய வேண்டிய கோப்பு/பகுதி:** `artifacts/tamil-ai-chat/app/chat.tsx` — `handleSend`-ன் URL, video, photo special branches.

## 3. சேமித்த message-களின் முழுமையான schema validation இல்லை

- **எந்த check-இல் கண்டறிந்தது:** Step 7, Step 1 — `loadChatHistory`-ன் parse மற்றும் format failure பாதைகளை ஆய்வு செய்தபோது.
- **மீதமுள்ள ஆபத்து:** JSON parse மற்றும் மேல்நிலை value array-ஆக உள்ளதா என்பவை சரிபார்க்கப்படுகின்றன; ஒவ்வொரு entry-யின் `id`, `role`, `content`, `timestamp` போன்ற fields முழுமையாகச் சரிபார்க்கப்படவில்லை. சரியான JSON array-க்குள் தவறான message வடிவம் இருந்தால் அது ஏற்றுக்கொள்ளப்பட்டு, UI-யில் எதிர்பாராத நடத்தையை ஏற்படுத்தலாம்.
- **சரிசெய்ய வேண்டிய கோப்பு/பகுதி:** `artifacts/tamil-ai-chat/app/chat.tsx` — `loadChatHistory`-ல் parse செய்யப்பட்ட entries-ஐ `Message`-ஆக மாற்றும் பகுதி.

## 4. புதிய shadow நிறங்கள் shared token-ஐப் பயன்படுத்தவில்லை

- **எந்த check-இல் கண்டறிந்தது:** Step 7 — Theme Tokens Check; மாற்றப்பட்ட app screens-ல் புதிதாகச் சேர்க்கப்பட்ட color literals-ஐ ஆய்வு செய்தபோது.
- **மீதமுள்ள ஆபத்து:** `ai-girls.tsx`-ல் இரண்டு புதிய `shadowColor: '#000'` மதிப்புகள் நேரடியாக உள்ளன. இதனால் புதிய hard-coded color value சேர்க்க வேண்டாம் என்ற theme வழிகாட்டி முழுமையாகப் பின்பற்றப்படவில்லை. இவை shadow நிறங்கள்; runtime-ல் visual impact உள்ளதா என்பது device-ல் சரிபார்க்கப்படவில்லை.
- **சரிசெய்ய வேண்டிய கோப்பு/பகுதி:** `artifacts/tamil-ai-chat/app/ai-girls.tsx` — user avatar toolbar மற்றும் floating action button shadow styles.

## 5. Design token JSON, runtime palette-ன் முழு export அல்ல

- **எந்த check-இல் கண்டறிந்தது:** Step 7 — Theme Tokens Check; runtime `colors.ts`-ஐ design token JSON-உடன் ஒப்பிட்டபோது.
- **மீதமுள்ள ஆபத்து:** `colors.ts`-ல் 55 தனித்துவமான நிற மதிப்புகள் உள்ளன; `tokens.json`-ல் 30 மட்டுமே உள்ளன. JSON-ல் உள்ள மதிப்புகள் runtime source-ல் உள்ளன; ஆனால் 25 தனித்துவமான runtime நிற மதிப்புகள் JSON-ல் விடுபட்டுள்ளன. `docs/design-system/README.md`-ல் JSON தற்போதைய `useColors()` மதிப்புகளின் export எனக் குறிப்பிடப்படுவதால், design export முழுமையற்றதாக இருக்கலாம்.
- **சரிசெய்ய வேண்டிய கோப்பு/பகுதி:** `docs/design-system/tokens.json` — விடுபட்ட palette values சேர்க்க; `docs/design-system/README.md` — முழு export அல்ல என்றால் அதன் scope-ஐத் தெளிவுபடுத்த.
