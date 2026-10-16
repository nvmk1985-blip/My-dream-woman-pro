# Future handoffs

இந்த directory, ஏற்கெனவே உள்ள My Dream Woman Pro GitHub app-ஐத் தொடர்ந்து பராமரிக்க அடுத்த agent பயன்படும் உறுதிப்படுத்தப்பட்ட handoff தகவல்களுக்கானது. புதிய app உருவாக்க வேண்டாம்.

## தற்போதைய நிலை
- Step 1 read-only audit: **முடிந்தது** — [step-1-audit.md](step-1-audit.md).
- ஆய்வு செய்த app source commit: `7a1fadc0a928b6975edecd1e8d646c67382ce0fb`.
- இந்த handoff commit-ல் `future/` ஆவணங்கள் மட்டும் சேர்க்கப்பட்டன; app source/assets மாற்றப்படவில்லை.
- Step 1-க்கு GitHub Action trigger செய்யப்படவில்லை.

## கட்டாய guardrails
- `/welcome` மற்றும் `artifacts/tamil-ai-chat/app/home.tsx` மாற்றக்கூடாது.
- ஏற்கெனவே உள்ள செயல்பாடுகள், integrations, handlers, API payloads, storage, notifications மற்றும் media flows-ஐ பாதுகாக்கவும்.
- ஒவ்வொரு code phase-க்கும் முன் user-ன் வெளிப்படையான OK பெற வேண்டும்; OK வரும் வரை code மாற்றக்கூடாது.
- User கொடுத்த screenshot/error-ஐ மட்டுமே target ஆக எடுத்துக்கொள்ளவும். Error அல்லது CI failure-ஐ ஊகிக்காமல், தொடர்புடைய எல்லா failure path-களையும் parallel-ஆ விசாரித்து verified காரணங்களையும் proposed fix-ஐயும் report செய்து, OK வரும் வரை காத்திருக்கவும்.
- ஏழு திட்டமிட்ட படிகளுக்கான code changes-ஐ ஒரே feature branch-ல் வைத்திருக்கவும். இடைப்பட்ட phase/push-களுக்கு APK build செய்யக்கூடாது. ஏழு படிகளும் முடிந்து approval கிடைத்த பிறகு branch-ஐ `main`-க்கு merge செய்து, `main`-ல் இருந்து ஒரே `Build APK` workflow-ஐ கைமுறையாக trigger செய்யவும்.
- Visual direction: obsidian/கருப்பு, glossy layers, teal/green, purple, cyan/blue, red status, அளவான gold; தமிழ் copy-ஐ பாதுகாக்கவும்.
- `Build APK` workflow கைமுறையாக trigger செய்யப்படும்; அது APK-ஐ GitHub Release-ல் வெளியிடும். அதே tag-ஐ rerun செய்தால் அந்த release/tag-ஐ delete செய்து மீண்டும் உருவாக்கும்; Render redeploy இயல்பாக false. Trigger-க்கு முன் இந்த side effects-ஐ user-க்கு தெளிவுபடுத்தவும்.

## கட்டம்-வாரியான handoff பதிவு

- ஒவ்வொரு step முடிந்ததும், `future/step-N-<சுருக்கப்பெயர்>.md` என்ற file-ல் முடிந்த scope, மாற்றிய files, verification/build முடிவு, commit SHA, blockers, அடுத்த step மற்றும் pending approval-களை பதிவு செய்யவும். Step 1-க்கு உள்ள `step-1-audit.md` பெயரிடும் முறையைப் பின்பற்றவும்.
- `future/README.md`-ல் தற்போதைய status, முடிந்த step, அடுத்த step, அந்த step-க்கு தேவையான approval, தொடர்புடைய handoff file link ஆகியவற்றைப் புதுப்பிக்கவும். Verified evidence மட்டுமே குறிப்பிடவும்; secrets சேர்க்க வேண்டாம்.
- Handoff docs-ஐ GitHub-க்கு normal commit/push ஆகச் சேர்க்கவும்; இது `Build APK` workflow-ஐ trigger செய்யும் முறை அல்ல. Docs-only update-க்கு APK build தேவையில்லை.
- Code changes-ஐ ஒரே feature branch-ல் commit/push செய்யவும். ஏழு திட்டமிட்ட படிகளும் முடிந்து approval கிடைத்த பிறகே அந்த branch-ஐ `main`-க்கு merge செய்யவும்; பின்னர் `main`-இலிருந்து `Build APK`-ஐ ஒரே முறை கைமுறையாக trigger செய்யவும். இடைப்பட்ட build-கள் செய்ய வேண்டாம்.
- Build trigger-க்கு முன் Release side effect-ஐ தெரிவிக்கவும்: workflow APK-ஐ GitHub Release-ல் வெளியிடும்; அதே tag-ஐ rerun செய்தால் ஏற்கெனவே உள்ள release/tag-ஐ delete செய்து மீண்டும் உருவாக்கும். Render redeploy input இயல்பாக false.

## அடுத்த நிலை
Step 2-ல் கேட்ட design system-ஐ முடித்து/present செய்த பிறகே app UI-ஐ மாற்றத் தொடங்கவும். ஏழு கட்ட பரிந்துரை மற்றும் உறுதிப்படுத்தப்பட்ட route/handler map `step-1-audit.md`-ல் உள்ளது. Step 2 இன்னும் தொடங்கப்படவில்லை.
