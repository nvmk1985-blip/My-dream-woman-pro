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
- User நேரடியாகக் கூறிய issue/error-ஐ மட்டுமே target ஆக எடுத்துக்கொள்ளவும். Screenshot-கள் துணை ஆதாரங்கள் மட்டுமே; அவற்றிலிருந்து user சொல்லாத error-ஐ ஊகிக்கவோ, screenshot-ஐ user-ன் விளக்கத்தை விட மேலானதாகக் கருதவோ கூடாது. Error அல்லது CI failure-ஐ ஊகிக்காமல், user சுட்டிக்காட்டிய issue-க்கு தொடர்புடைய எல்லா failure path-களையும் parallel-ஆ விசாரித்து verified காரணங்களையும் proposed fix-ஐயும் report செய்து, OK வரும் வரை காத்திருக்கவும்.
- ஏழு திட்டமிட்ட படிகளுக்கான code changes-ஐ ஒரே feature branch-ல் வைத்திருக்கவும். இடைப்பட்ட phase/push-களுக்கு APK build செய்யக்கூடாது. ஏழு படிகளும் முடிந்து approval கிடைத்த பிறகு branch-ஐ `main`-க்கு merge செய்து, `main`-ல் இருந்து ஒரே `Build APK` workflow-ஐ கைமுறையாக trigger செய்யவும்.
- Visual direction: Cyberpunk Luxury — deep black surfaces (#07060B), electric-purple accents, restrained neon/glass effects, readable Tamil copy; keep semantic success/warning/error/info colors distinct.
- `Build APK` workflow கைமுறையாக trigger செய்யப்படும்; அது APK-ஐ GitHub Release-ல் வெளியிடும். அதே tag-ஐ rerun செய்தால் அந்த release/tag-ஐ delete செய்து மீண்டும் உருவாக்கும்; Render redeploy இயல்பாக false. Trigger-க்கு முன் இந்த side effects-ஐ user-க்கு தெளிவுபடுத்தவும்.

## Requested design brief — Cyberpunk Luxury (Step 2; implementation pending)

இணைக்கப்பட்ட இரண்டு design brief-களின் ஒருங்கிணைந்த விவரக்குறிப்பு இது. இது theme-க்கான source of truth; Step 2/code implementation இன்னும் தொடங்கவில்லை. UI-ஐ மாற்றும் ஒவ்வொரு code phase-க்கும் முன் user-ன் வெளிப்படையான OK தேவை.

### Scope
- Theme-ஐ எல்லா existing non-Home UI screens-க்கும் பொருந்தச் செய்யவும்: Chat, Character List/Edit, Settings மற்றும் nested options, Keys/Accounts, Character URLs, Cloudinary/Image Cloud, Cloud Storage, Gallery, Image-to-Script, Script-to-Image, Swap/Face Swap, மற்றும் அவற்றின் dialogs, modals, dropdowns, menus, forms, inputs, cards, buttons, loading/progress/error states.
- `/welcome` மற்றும் Home (`/home`) பாதுகாக்கப்பட்டவை; அவற்றை மாற்ற வேண்டாம்.
- இது visual-only redesign. Existing navigation, routes, handlers, APIs/request-response payloads, backend, state management, persistence, stored preferences, feature workflows, uploads/generation/swap/download, notifications, GitHub Actions, Release publishing, மற்றும் Render configuration மாற்றப்படக்கூடாது. Mock data கொண்டு real functionality-ஐ மாற்றவோ feature-ஐ நீக்கவோ கூடாது.

### Theme tokens
ஏற்கெனவே உள்ள shared theme/token architecture-ஐ முதலில் ஆய்வு செய்து அதையே reuse செய்யவும். Duplicate token system உருவாக்க வேண்டாம். Targeted hardcoded colors-ஐ semantic tokens-ஆக மாற்றவும்; dynamic/platform colors மற்றும் user preferences-ஐ பாதுகாக்கவும்.

```css
:root {
  --color-background: #07060B;
  --color-background-secondary: #0B0912;
  --color-background-tertiary: #100D1A;
  --color-background-elevated: #151020;
  --color-surface: #100D18;
  --color-surface-secondary: #171126;
  --color-surface-elevated: #201632;
  --color-surface-hover: #281B3D;
  --color-surface-active: #32204D;
  --color-primary: #A855F7;
  --color-primary-hover: #B96BFF;
  --color-primary-active: #8B3DE0;
  --color-primary-light: #D8B4FE;
  --color-primary-dark: #6D28D9;
  --color-neon-purple: #BF5AF2;
  --color-neon-purple-bright: #D946EF;
  --color-purple-glow: #9333EA;
  --color-purple-muted: #7C3AED;
  --color-secondary: #7C4DFF;
  --color-secondary-hover: #9575FF;
  --color-accent: #E879F9;
  --color-accent-soft: #C084FC;
  --color-text-primary: #F8F5FF;
  --color-text-secondary: #C4B5D8;
  --color-text-tertiary: #9686AA;
  --color-text-muted: #766783;
  --color-text-disabled: #51475F;
  --color-text-on-primary: #FFFFFF;
  --color-border: #30213F;
  --color-border-subtle: #21182E;
  --color-border-strong: #68409A;
  --color-border-primary: #A855F7;
  --color-border-focus: #C084FC;
  --color-icon-primary: #F3E8FF;
  --color-icon-secondary: #BFA7D9;
  --color-icon-muted: #78658F;
  --color-icon-active: #C084FC;
  --color-icon-accent: #D946EF;
  --color-button-primary: #9333EA;
  --color-button-primary-hover: #A855F7;
  --color-button-primary-pressed: #7E22CE;
  --color-button-secondary: #21152F;
  --color-button-secondary-hover: #322044;
  --color-button-disabled: #30263A;
  --color-button-text: #FFFFFF;
  --color-button-secondary-text: #E9D5FF;
  --color-input-background: #0D0A14;
  --color-input-border: #352344;
  --color-input-border-focus: #A855F7;
  --color-input-placeholder: #887795;
  --color-input-text: #F8F5FF;
  --color-chat-background: #09070F;
  --color-chat-user-bubble: #45216C;
  --color-chat-user-text: #FFFFFF;
  --color-chat-ai-bubble: #171020;
  --color-chat-ai-text: #F3E8FF;
  --color-chat-divider: #2A1D37;
  --color-chat-timestamp: #9583A8;
  --color-success: #34D399;
  --color-success-background: #0D281F;
  --color-warning: #FBBF24;
  --color-warning-background: #30240D;
  --color-error: #FB7185;
  --color-error-background: #30121D;
  --color-info: #67E8F9;
  --color-info-background: #0D222B;
  --color-overlay: rgba(0, 0, 0, 0.72);
  --color-purple-overlay: rgba(168, 85, 247, 0.12);
  --shadow-purple: rgba(147, 51, 234, 0.18);
  --shadow-purple-strong: rgba(168, 85, 247, 0.30);
  --color-neon-line: #A855F7;
  --color-glass-background: rgba(21, 16, 32, 0.82);
  --color-glass-border: rgba(192, 132, 252, 0.22);
}
```

### Visual and interaction rules
- Use translucent dark glass surfaces for cards/panels/dialogs/menus/floating controls, subtle purple borders, restrained blur with a no-blur fallback, and soft depth. Keep foreground text readable; do not make every component transparent.
- Reserve neon glow for active/selected navigation, tabs/cards, focused inputs, primary actions, progress, and important status. Suggested glow: `0 0 12px rgba(168, 85, 247, 0.18)`; stronger glow only for key selections. Avoid visual clutter and distracting animation.
- Use gradients sparingly: primary action `linear-gradient(135deg, #7E22CE 0%, #A855F7 55%, #C026D3 100%)`; premium card accent `linear-gradient(135deg, #21152F 0%, #151020 55%, #241332 100%)`; subtle highlight `linear-gradient(90deg, rgba(168, 85, 247, 0.12), rgba(217, 70, 239, 0.04))`. Do not put bright gradients across entire screens.
- Maintain near-white headings, legible supporting text, consistent type hierarchy, left-aligned titles/forms/settings, and vertically aligned icons/text. Center only appropriate empty/loading states. Preserve Tamil and English rendering; prevent clipping, overlap, unexpected wrapping, and horizontal overflow.
- Chat: deep-black background; premium purple user bubbles; dark-glass AI bubbles; aligned composer, controls, avatars, timestamps, spacing, and subtle purple focus border. Preserve every current chat/data flow.
- Character List/Edit: clear portraits with consistent aspect ratios; premium cards and restrained selected borders; readable names/descriptions/actions. Preserve create/edit/select/save/delete flows.
- Settings and nested options: consistent groups, rows, dividers, switches, dropdowns, selection/focus/disabled states. Preserve every option, value, and saved preference.
- Image workspaces: dark panels and purple upload/primary-action accents; correctly scaled previews; aligned prompts/forms; clear progress/results. Preserve upload, processing, generation, swapping, saving, and download behavior.
- Prioritize mobile usability while retaining tablet/desktop layouts. Prevent horizontal scroll; respect touch-target sizes, safe areas, viewport-fitting dialogs/bottom sheets, and the on-screen keyboard.

### Validation and completion report
After each approved implementation phase, run the available local checks; verify imports, syntax, token references, affected screens, navigation, and existing behavior. Inspect for inconsistent colors, text alignment, clipping, and responsive regressions. Do not claim a check passed unless it ran. Report changed files, checks/build results, remaining hardcoded colors, and unresolved issues. Final goal: a cohesive futuristic luxury UI with deep-black surfaces, electric-purple accents, restrained glass/neon effects, readable Tamil/English text, and existing functionality intact.

## கட்டம்-வாரியான handoff பதிவு

- ஒவ்வொரு step முடிந்ததும், `future/step-N-<சுருக்கப்பெயர்>.md` என்ற file-ல் முடிந்த scope, மாற்றிய files, verification/build முடிவு, commit SHA, blockers, அடுத்த step மற்றும் pending approval-களை பதிவு செய்யவும். Step 1-க்கு உள்ள `step-1-audit.md` பெயரிடும் முறையைப் பின்பற்றவும்.
- `future/README.md`-ல் தற்போதைய status, முடிந்த step, அடுத்த step, அந்த step-க்கு தேவையான approval, தொடர்புடைய handoff file link ஆகியவற்றைப் புதுப்பிக்கவும். Verified evidence மட்டுமே குறிப்பிடவும்; secrets சேர்க்க வேண்டாம்.
- Handoff docs-ஐ GitHub-க்கு normal commit/push ஆகச் சேர்க்கவும்; இது `Build APK` workflow-ஐ trigger செய்யும் முறை அல்ல. Docs-only update-க்கு APK build தேவையில்லை.
- Code changes-ஐ ஒரே feature branch-ல் commit/push செய்யவும். ஏழு திட்டமிட்ட படிகளும் முடிந்து approval கிடைத்த பிறகே அந்த branch-ஐ `main`-க்கு merge செய்யவும்; பின்னர் `main`-இலிருந்து `Build APK`-ஐ ஒரே முறை கைமுறையாக trigger செய்யவும். இடைப்பட்ட build-கள் செய்ய வேண்டாம்.
- Build trigger-க்கு முன் Release side effect-ஐ தெரிவிக்கவும்: workflow APK-ஐ GitHub Release-ல் வெளியிடும்; அதே tag-ஐ rerun செய்தால் ஏற்கெனவே உள்ள release/tag-ஐ delete செய்து மீண்டும் உருவாக்கும். Render redeploy input இயல்பாக false.

## அடுத்த நிலை
Step 2-ல் கேட்ட design system-ஐ முடித்து/present செய்த பிறகே app UI-ஐ மாற்றத் தொடங்கவும். ஏழு கட்ட பரிந்துரை மற்றும் உறுதிப்படுத்தப்பட்ட route/handler map `step-1-audit.md`-ல் உள்ளது. Step 2 இன்னும் தொடங்கப்படவில்லை.
