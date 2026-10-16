# Step 1 — Read-only audit மற்றும் handoff

## நிலை
- Step 1 முடிந்தது: read-only ஆய்வு; app source, asset, workflow, dependency அல்லது lockfile எதுவும் மாற்றப்படவில்லை.
- ஆய்வு செய்த code நிலை: `main` @ `7a1fadc0a928b6975edecd1e8d646c67382ce0fb` (`fix: restore valid home hero image asset`). Handoff ஆவணங்கள் மட்டும் இந்த commit-இல் சேர்க்கப்படுகின்றன.
- GitHub repo root-ல் duplicate `app/` directory இல்லை. Expo route source `artifacts/tamil-ai-chat/app/`-ல் உள்ளது. புதிய app உருவாக்க வேண்டாம்.

## கட்டாய scope மற்றும் பாதுகாப்பு விதிகள்
- `/welcome` (`artifacts/tamil-ai-chat/app/welcome.tsx`) மற்றும் Home (`artifacts/tamil-ai-chat/app/home.tsx`) மாற்றக்கூடாது.
- தற்போதைய navigation, handlers, API/services மற்றும் payloads, AsyncStorage, notifications, Cloudinary/media செயல்கள், progress/error states ஆகியவற்றை பாதுகாக்க வேண்டும். Visual-only மாற்றங்களை முன்னுரிமை கொடுக்கவும்.
- User-இன் தெளிவான OK இல்லாமல் எந்த error/CI failure-யும் சரிசெய்யக்கூடாது. Error screenshot அல்லது தனி failure-ஐக் கண்டால் காரணத்தை report செய்து காத்திருக்கவும்.
- Reference தோற்றம்: obsidian/கருப்பு அடிப்படை; glossy அடுக்குகள்; தேர்வு/செயல்பாட்டு states-க்கு teal/green, purple, cyan/blue; error/off-க்கு red; குறைந்த அளவு gold. தமிழ் copy-ஐ பாதுகாக்கவும்.
- User ஒப்புதல் பெற்ற ஒவ்வொரு code phase-க்கும் ஒரே coherent push மற்றும் Build APK Action வேண்டும் எனக் கூறியுள்ளார். ஆனால் தற்போதைய Action GitHub Release-ஐ உருவாக்க/அதே tag-ஐ நீக்கி மீண்டும் உருவாக்கும்; அதனால் ஒவ்வொரு trigger-க்கும் முன் இந்த side effect-ஐ உறுதிப்படுத்தவும்.

## Route மற்றும் screen map

| Route / file | தற்போதைய பொறுப்பு மற்றும் redesign கவனம் |
|---|---|
| `/welcome` — `app/welcome.tsx` | பாதுகாக்கப்பட்ட screen. `/prompt-image`, `/ai-girls` (script/group params), `/face-swap`, `/home`, `/settings`-க்கு navigation உள்ளது. மாற்ற வேண்டாம். |
| `/home` — `app/home.tsx` | பாதுகாக்கப்பட்ட Home. `/ai-girls-cloud` மற்றும் `/settings` போன்றவற்றுக்கான launch points உள்ளன. மாற்ற வேண்டாம்; linked destination-களை மட்டும் scope-க்குள் restyle செய்யலாம். |
| `/ai-girls` — `app/ai-girls.tsx` (2016 lines) | Character list, add/group/relationship flows, URL settings navigation; screenshot-இல் உள்ள Settings modal (Online, Auto Message, character intervals, Gemma, ringtone, PIN, Keys & Accounts); Photo-to-Script modal. பல behavior-கள் ஒரே பெரிய screen-ல் உள்ளன; முழு file-ஐ rewrite செய்யாமல் visual பகுதிகளை தனித்தனியாக மாற்றவும். |
| `/edit-character` — `app/edit-character.tsx` (1332 lines) | Character profile/sections, avatar picker/Cloudinary URL, image analysis, prompt/story save, local/cloud state. Save மற்றும் media flows பாதுகாக்கப்பட வேண்டும். |
| `/chat` — `app/chat.tsx` (3358 lines) | Chat history/persona, online/offline AI, media/image/video, Cloudinary, image prompt, translation மற்றும் பல stateful flows. மிக உயர்ந்த regression risk; UI-only edits மற்றும் நடத்தை சோதனை அவசியம். |
| `/settings` — `app/settings.tsx` (1114 lines) | Screenshot settings sheet அல்ல; server/API configuration, keys, latest APK, GitHub build trigger/status/download, app-icon upload, global photo-style management போன்ற technical settings. |
| `/keys` — `app/keys.tsx` (935 lines) | Keys/Accounts screen மற்றும் provider key validation. Settings modal-இலிருந்து திறக்கப்படுகிறது. |
| `/character-urls` — `app/character-urls.tsx` (373 lines) | Character URL add/edit/status/delete/reorder/save. |
| `/ai-girls-cloud` — `app/ai-girls-cloud.tsx` (1547 lines) | Character/style அடிப்படையிலான Cloudinary image manager: folders, upload, select/delete, metadata restore, gallery save. |
| `/cloud-storage` — `app/cloud-storage.tsx` (1339 lines) | Cloudinary credentials UI, videos, app icon மற்றும் project ZIP/backup/sync செயல்கள். Credentials-ஐ audit-ல் வெளியிடக்கூடாது. |
| `/gallery` — `app/gallery.tsx` (1606 lines) | Device albums, Cloudinary மற்றும் Google Drive backup, upload progress, pause/resume/cancel, folders/downloads. Media backup behavior-க்கு regression testing தேவை. |
| `/prompt-image` — `app/prompt-image.tsx` (552 lines) | Text prompt-to-image மற்றும் image upload → Gemini image-to-prompt → image generation flow; styles/models/negative prompt/progress/error states. |
| `/face-swap` — `app/face-swap.tsx` (727 lines) | Source/target image pick, external HF/Gradio face swap, optional face/image enhancement, result/save மற்றும் failure states. |

Shared error/media surfaces: `ErrorBoundary` மற்றும் `ErrorFallback` render failure/restart/details-ஐ கையாள்கின்றன; `MediaVideoPlayer`-ல் video load-error state உள்ளது. Screen-level async errors பெரும்பாலும் alerts, progress அல்லது local error state வழியாக கையாளப்படுகின்றன. Redesign-ல் error details, retry/progress மற்றும் media controls-ஐ வெறும் அலங்காரமாக மாற்றி நீக்கக்கூடாது.

## GitHub Actions failure ஆய்வு
- 2026-10-14-ன் run `38587062210` தோல்வியடைந்தது; failure step: `Bundle JS with expo export:embed`. Expo bundler: `assets/images/home-hero.jpg: unsupported file type: undefined`.
- அந்த commit (`63da6d48…`)-இல் asset 61,430 bytes என GitHub metadata காட்டுகிறது. Error log-இல் பாதை உறுதி செய்யப்பட்டுள்ளது; அந்தக் கால binary-ஐ shallow local clone-ல் ஆய்வு செய்ய முடியவில்லை.
- அடுத்த commit `7a1fadc0…` (`fix: restore valid home hero image asset`) அந்த image-ஐ மாற்றியது. தற்போதைய asset `file`/`identify` மூலம் JPEG, 340×576, 39,667 bytes எனச் சரிபார்க்கப்பட்டது. அது `welcome.tsx`-இல் மட்டுமே reference செய்யப்பட்டுள்ளது.
- அதன்பின் run `38587599390` வெற்றி பெற்றது. ஆகவே இந்த குறிப்பிட்ட historical failure தற்போதைய `main`-ல் ஏற்கெனவே தீர்க்கப்பட்டுள்ளது; இந்த ஆய்வில் எந்த fix-மும் செய்யப்படவில்லை.
- Latest checked Action: `Build APK` run `38587599390` — success. [Actions](https://github.com/nvmk1985-blip/My-dream-woman-pro/actions).
- `.github/workflows/build-apk.yml` `workflow_dispatch` வழியாக மட்டுமே தொடங்குகிறது; push-இல் auto-trigger இல்லை. APK build முடிவில் Release tag-ஐ delete/recreate செய்து APK வெளியிடுகிறது; optional `deploy_render` default false. இது சாதாரண test-only build அல்ல. Step 1 docs-only என்பதால் Action trigger செய்யப்படவில்லை.

## Local baseline மற்றும் வரம்புகள்
- `pnpm install --frozen-lockfile --ignore-scripts` lockfile mismatch-ல் நின்றது: `artifacts/tamil-ai-chat/package.json`-ல் `expo-intent-launcher@~13.0.8` உள்ளது; `pnpm-lock.yaml`-ல் lock entry இல்லை. எந்த lockfile மாற்றமும் செய்யப்படவில்லை.
- `--no-frozen-lockfile` முயற்சியில் Replit package firewall `orval@8.5.3`-க்கு 403 தந்தது; app-filtered முயற்சியில் `shell-quote@1.8.3`-க்கும் 403 கிடைத்தது. இவை temporary inspection clone-இல் நடந்தன; lockfile-ஐ மீட்டெடுத்த பின் clone clean எனச் சரிபார்க்கப்பட்டது.
- Dependencies install ஆகாததால் app `typecheck` இயக்கப்படவில்லை. `artifacts/tamil-ai-chat`-ல் `*.test.*` / `*.spec.*` files எதுவும் கிடைக்கவில்லை. GitHub Action-ன் தற்போதைய successful run மட்டும் Android bundle/APK flow-க்கு கிடைத்த remote baseline; local typecheck வெற்றி எனக் கருதக்கூடாது.
- User கூறிய 1,247 style color / 427 inline icon-button color எண்ணிக்கைகளை உருவாக்கிய dry-run script அல்லது method repo-வில் கிடைக்கவில்லை. வேறு, எளிய grep முறையில் Home/Welcome-ஐத் தவிர்த்த app TS/TSX-ல் 1,828 hex-token matches மற்றும் 1,620 color-like property matches கிடைத்தன. இவை user-ன் வகைப்பாட்டுடன் ஒப்பிடத்தக்கவை அல்ல; acceptance count-ஆகப் பயன்படுத்த வேண்டாம்.
- `app.json`-ல் `userInterfaceStyle: light`; launcher/adaptive icon மற்றும் splash தனி assets-ஆக உள்ளன. Global dark-mode மாற்றம் protected Home/Welcome-ஐ பாதிக்கக்கூடும். Local screen styling-ஐ முதலில் பரிசீலிக்கவும்; splash/Home assets-ஐ தொடக்கூடாது.

## அடுத்த கட்டத்திற்கான பரிந்துரைக்கப்பட்ட வரிசை — இன்னும் தொடங்கப்படவில்லை
1. Step 2: Screenshot-களை அடிப்படையாகக் கொண்டு கேட்ட design system-ஐ முடித்து/present செய்யவும்; app UI மாற்றத்திற்கு முன் அதன் tokens/components-ஐ தீர்மானிக்கவும். புதிய mobile app உருவாக்க வேண்டாம்.
2. Step 3: Settings modal, `/settings`, `/keys` — state/handlers மாற்றமின்றி.
3. Step 4: Character list, Edit, character URL screens.
4. Step 5: Chat மற்றும் media/error views.
5. Step 6: Cloudinary, cloud storage, Gallery.
6. Step 7: Photo-to-Script, `/prompt-image`-ன் Script-to-Image/Image-to-Prompt, Face Swap, icon மட்டும்; பின்னர் scope முழுவதும் regression check.

ஒவ்வொரு implementation phase-க்கும் முன் user approval பெறவும்; Home/Welcome diff இல்லாததைச் சரிபார்க்கவும். Commit/push மற்றும் Action trigger செய்யும் முன் Release replacement side effect-ஐ உறுதிப்படுத்தவும். Step 2 அல்லது code phases எதுவும் இந்த handoff-இல் தொடங்கப்படவில்லை.
