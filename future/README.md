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
- User-ன் தெளிவான OK இல்லாமல் எந்த error அல்லது CI failure-யும் fix செய்யக்கூடாது; முதலில் காரணத்தை report செய்து காத்திருக்கவும்.
- Visual direction: obsidian/கருப்பு, glossy layers, teal/green, purple, cyan/blue, red status, அளவான gold; தமிழ் copy-ஐ பாதுகாக்கவும்.
- ஒப்புதல் பெற்ற ஒவ்வொரு code phase-க்கும் push + GitHub Actions build வேண்டுமென user கூறியுள்ளார். தற்போதைய `Build APK` Action Release tag-ஐ delete/recreate செய்து APK வெளியிடும்; trigger செய்வதற்கு முன் இந்த side effect-ஐ உறுதிப்படுத்தவும்.

## கட்டம்-வாரியான handoff பதிவு

- ஒவ்வொரு step முடிந்ததும், `future/step-N-<சுருக்கப்பெயர்>.md` என்ற file-ல் முடிந்த scope, மாற்றிய files, verification/build முடிவு, commit SHA, blockers, அடுத்த step மற்றும் pending approval-களை பதிவு செய்யவும். Step 1-க்கு உள்ள `step-1-audit.md` பெயரிடும் முறையைப் பின்பற்றவும்.
- `future/README.md`-ல் தற்போதைய status, முடிந்த step, அடுத்த step, அந்த step-க்கு தேவையான approval, தொடர்புடைய handoff file link ஆகியவற்றைப் புதுப்பிக்கவும். Verified evidence மட்டுமே குறிப்பிடவும்; secrets சேர்க்க வேண்டாம்.
- Handoff docs-ஐ GitHub-க்கு normal commit/push ஆகச் சேர்க்கவும்; இது `Build APK` workflow-ஐ trigger செய்யும் முறை அல்ல. Docs-only update-க்கு APK build தேவையில்லை.
- User-ஒப்புதல் பெற்ற code phase-க்கு code மற்றும் handoff update-ஐ commit/push செய்த பின் `Build APK`-ஐ தனியாக trigger செய்யவும்; trigger செய்வதற்கு முன் workflow-ன் Release/deploy side effects-ஐ சரிபார்த்து தெரிவிக்கவும்.

## அடுத்த நிலை
Step 2-ல் கேட்ட design system-ஐ முடித்து/present செய்த பிறகே app UI-ஐ மாற்றத் தொடங்கவும். ஏழு கட்ட பரிந்துரை மற்றும் உறுதிப்படுத்தப்பட்ட route/handler map `step-1-audit.md`-ல் உள்ளது. Step 2 இன்னும் தொடங்கப்படவில்லை.
