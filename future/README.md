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
- Visual direction: Black Leather + Royal Gold + Sky Blue/Cyan Neon + subtle premium glassmorphism; deep charcoal backgrounds (#080B0D), gold for premium emphasis, cyan for interactive states, warm-white text, and readable Tamil copy.
- `Build APK` workflow கைமுறையாக trigger செய்யப்படும்; அது APK-ஐ GitHub Release-ல் வெளியிடும். அதே tag-ஐ rerun செய்தால் அந்த release/tag-ஐ delete செய்து மீண்டும் உருவாக்கும்; Render redeploy இயல்பாக false. Trigger-க்கு முன் இந்த side effects-ஐ user-க்கு தெளிவுபடுத்தவும்.

## Requested design brief — Black Leather + Royal Gold (Step 2; implementation pending)

புதிய இணைக்கப்பட்ட file-ன் விவரக்குறிப்பு, முந்தைய Black + Electric Purple brief-ஐ முழுமையாக மாற்றுகிறது. Step 2 / app implementation இன்னும் தொடங்கவில்லை. ஒவ்வொரு code phase-க்கும் முன் user-ன் வெளிப்படையான OK பெறவும்.


### Reference Images

![Chat UI and Image Studio reference](references/chat-image-studio-premium.jpeg)

![Storage Hub, PIN, and intervals reference](references/storage-hub-pin-interval-premium.jpeg)

COMPLETE PREMIUM UI/UX REDESIGN

Black Leather + Royal Gold + Sky Blue Neon + Premium Glassmorphism

DESIGN VISION

Redesign the existing app into a futuristic luxury AI application inspired by the supplied reference images.

Combine:

- Black leather luxury aesthetics
- Royal gold metallic accents
- Sky blue / cyan neon highlights
- Premium glassmorphism
- Elegant typography
- Consistent text alignment
- Professional layouts and spacing
- Refined buttons, icons, cards, borders, and input fields

The result should feel like a premium luxury AI product, not a typical gaming interface.

IMPORTANT: Preserve existing functionality, APIs, backend logic, navigation, stored preferences, and workflows.

---

1. COMPLETE PREMIUM COLOUR PALETTE

Use the following colour system consistently across all targeted screens.

A. Background Colours

--color-bg-primary: #080B0D;
--color-bg-secondary: #0C1215;
--color-bg-tertiary: #111A1E;
--color-bg-elevated: #162126;
--color-bg-deep: #050708;

--color-leather-black: #101416;
--color-leather-charcoal: #1A2022;
--color-panel-dark: #0D171B;

Purpose:

- Main application background: "#080B0D"
- Secondary sections: "#0C1215"
- Elevated panels: "#162126"
- Premium dark surfaces: "#101416"

Use dark backgrounds as the foundation. Avoid bright backgrounds across the main interface.

B. Royal Gold Palette

--color-gold-primary: #D4AF6A;
--color-gold-bright: #F4D58D;
--color-gold-light: #FFE8B0;
--color-gold-dark: #9B773A;
--color-gold-deep: #705327;

--color-gold-border: #B89555;
--color-gold-muted: #8D774E;
--color-gold-glow: rgba(212, 175, 106, 0.24);

Use gold for:

- Premium headings and selected labels
- Luxury borders
- Selected controls
- Premium badges
- Special icons
- Important secondary actions
- Subtle decorative details

Gold must look metallic and elegant. Avoid using bright yellow as a substitute for gold.

C. Sky Blue and Cyan Neon Palette

--color-cyan-primary: #55DDF5;
--color-cyan-bright: #80EEFF;
--color-cyan-light: #B6F5FF;
--color-cyan-dark: #168FA8;
--color-sky-blue: #63BFF2;

--color-cyan-border: #278EA3;
--color-cyan-glow: rgba(85, 221, 245, 0.24);
--color-cyan-soft: rgba(85, 221, 245, 0.10);

Use cyan for:

- Active navigation icons
- Focused inputs
- Selected tabs
- Active buttons
- Chat interaction controls
- Progress indicators
- Important interactive highlights

Use cyan as an accent, not as the main background colour.

D. Typography Colours

--color-text-primary: #F5F1E8;
--color-text-secondary: #C8D0D1;
--color-text-tertiary: #96A5A8;
--color-text-muted: #718084;
--color-text-disabled: #505B5E;

--color-text-gold: #F4D58D;
--color-text-cyan: #80EEFF;
--color-text-on-gold: #15120B;
--color-text-on-cyan: #061014;

Maintain sufficient contrast between text and its background.

Do not make all text gold or cyan. Use warm white for primary text, muted grey for supporting text, gold for luxury emphasis, and cyan for interactive highlights.

E. Cards, Borders, and Glassmorphism

--color-card: #11191C;
--color-card-secondary: #172226;
--color-card-elevated: #1B292E;

--color-border: #29373B;
--color-border-subtle: #1C292D;
--color-border-gold: #B89555;
--color-border-cyan: #278EA3;

--color-glass-bg: rgba(17, 26, 30, 0.88);
--color-glass-gold-border: rgba(212, 175, 106, 0.42);
--color-glass-cyan-border: rgba(85, 221, 245, 0.32);
--color-overlay: rgba(0, 0, 0, 0.76);

Use:

- Gold borders for premium sections and selected luxury components.
- Cyan borders for interactive and focused elements.
- Neutral dark borders for ordinary cards.
- Translucent surfaces for modals and floating panels.

Keep glassmorphism subtle enough to preserve readability.

F. Buttons

--color-button-gold: #D4AF6A;
--color-button-gold-hover: #F4D58D;
--color-button-gold-pressed: #B89555;
--color-button-gold-text: #15120B;

--color-button-cyan: #55DDF5;
--color-button-cyan-hover: #80EEFF;
--color-button-cyan-pressed: #168FA8;
--color-button-cyan-text: #061014;

--color-button-secondary: #172226;
--color-button-secondary-hover: #223237;
--color-button-secondary-text: #F5F1E8;

--color-button-disabled: #293034;

Primary actions should use gold or cyan according to their role.

Use gold for premium or primary confirmation actions and cyan for active interactive tools. Avoid giving every button a different colour.

G. Inputs, Forms, and Search

--color-input-bg: #0B1215;
--color-input-border: #35464B;
--color-input-focus: #55DDF5;
--color-input-text: #F5F1E8;
--color-input-placeholder: #829196;
--color-input-label: #C8D0D1;

Provide clear focus indicators and readable placeholder text.

H. Chat Colours

--color-chat-bg: #080D10;
--color-chat-user-bubble: #153D46;
--color-chat-user-text: #F5FCFF;
--color-chat-ai-bubble: #172126;
--color-chat-ai-text: #F5F1E8;
--color-chat-divider: #29373B;
--color-chat-timestamp: #96A5A8;
--color-chat-online: #55DDF5;

Use dark, refined message bubbles with subtle cyan or gold accents.

I. Status Colours

--color-success: #55D6A0;
--color-warning: #F2C66D;
--color-error: #FF7D86;
--color-info: #63BFF2;

Preserve clear visual distinctions between success, warning, error, and informational states.

---

2. PREMIUM GRADIENTS AND LIGHT EFFECTS

Use gradients sparingly.

Royal Gold Gradient

linear-gradient(
  135deg,
  #8D6A32 0%,
  #D4AF6A 45%,
  #FFE8B0 70%,
  #B89555 100%
)

Sky Blue Neon Gradient

linear-gradient(
  135deg,
  #168FA8 0%,
  #55DDF5 55%,
  #B6F5FF 100%
)

Premium Dark Glass Gradient

linear-gradient(
  145deg,
  rgba(28, 41, 46, 0.96),
  rgba(8, 11, 13, 0.96)
)

Gold Glow

0 0 12px rgba(212, 175, 106, 0.18)

Cyan Glow

0 0 14px rgba(85, 221, 245, 0.20)

Do not apply strong glows to every component. Use them for active controls, focused inputs, selected cards, and important actions only.

---

3. TYPOGRAPHY REDESIGN

Create a consistent typography hierarchy across the application.

Font Families

- Primary UI font: use the existing readable sans-serif font or a compatible modern font such as Inter.
- Tamil text: use a font with reliable Tamil glyph coverage, such as Noto Sans Tamil, where supported.
- Decorative luxury typography: reserve elegant serif typography for selected branding or decorative headings only.

Do not use decorative fonts for every label, input, button, or paragraph.

Recommended Typography Scale

Element| Size| Weight
Main page title| 24–28 px| 700
Section heading| 18–22 px| 600
Card title| 16–18 px| 600
Body text| 14–16 px| 400
Supporting text| 12–14 px| 400
Button label| 14–16 px| 600
Small metadata| 11–12 px| 500

Use these as design targets and adapt them to the existing mobile framework and screen density.

Typography Rules

- Use consistent font weights.
- Maintain comfortable line heights.
- Avoid excessive letter spacing.
- Prevent clipped Tamil characters and mixed Tamil-English text.
- Keep buttons and input labels readable.
- Use gold for selected titles, not for all body text.
- Maintain consistent text hierarchy on every screen.

---

4. TEXT ALIGNMENT REDESIGN

Correct text alignment throughout all targeted UI components.

Page Titles

- Use consistent left alignment.
- Align titles with the main content edge.
- Keep back buttons and action icons vertically centered.

Forms

- Left-align labels, input fields, descriptions, and validation messages.
- Keep labels directly associated with their inputs.
- Align form controls consistently.

Buttons

- Center button labels vertically and horizontally where appropriate.
- Align icons and text consistently.
- Prevent icons from shifting when button labels change.

Cards

- Use consistent title and description alignment.
- Keep action buttons in predictable positions.
- Maintain uniform spacing between card elements.

Chat

- Preserve the established conversational alignment.
- Align timestamps, avatars, message bubbles, and input controls consistently.
- Prevent long messages from overflowing the viewport.

Settings

- Align icons, titles, subtitles, switches, and dropdown indicators.
- Keep each setting row visually balanced.

Do not center every element. Choose alignment based on content type and usability.

---

5. LAYOUT, SPACING, AND COMPONENT STYLES

Use a consistent spacing system:

--space-1: 4px;
--space-2: 8px;
--space-3: 12px;
--space-4: 16px;
--space-5: 20px;
--space-6: 24px;
--space-8: 32px;

Recommended component styling:

- Cards: consistent internal padding and border treatment.
- Inputs: consistent heights, padding, and focus states.
- Buttons: consistent heights, touch targets, and icon spacing.
- Settings rows: consistent vertical alignment and separators.
- Modals: clear hierarchy, appropriate margins, and readable actions.
- Navigation: consistent icon sizes and active-state indicators.

Respect existing platform conventions and component dimensions when necessary.

---

6. SCREEN-BY-SCREEN REDESIGN

A. Chat Screen

- Deep charcoal background.
- Refined dark message bubbles.
- Cyan active controls.
- Gold accents for premium highlights.
- Readable timestamps and message text.
- Polished message composer and action icons.

B. Character List

- Consistent portrait sizing and aspect ratios.
- Dark premium cards.
- Gold borders for selected premium states.
- Cyan selection indicators.
- Clear character names and descriptions.

C. Character Edit

- Consistent form layout.
- Refined input fields.
- Premium upload and preview cards.
- Clear save, cancel, and other existing actions.
- Consistent focus, disabled, success, and error states.

D. Settings and Nested Options

- Consistent settings sections.
- Dark surfaces with subtle borders.
- Cyan focus and active indicators.
- Gold highlights for premium options.
- Consistent switches, dropdowns, labels, and descriptions.

E. Storage Hub

- Premium dark storage cards.
- Gold or cyan outlined icons.
- Consistent image, camera, movie, document, music, cloud, and other existing category styles.
- Clear labels and notification badges.
- Preserve all existing storage actions.

F. PIN and Security Screens

- Clear PIN indicators.
- Consistent keypad buttons.
- Gold accents for security-related branding.
- Cyan focus and interaction feedback.
- Maintain readable instructions and status messages.

G. Character Interval Controls

- Consistent character rows.
- Clearly distinguish selected intervals.
- Use cyan for active selection and gold for premium emphasis.
- Preserve the existing interval options and saved values.

H. Cloudinary / Image Cloud

- Dark workspace panels.
- Consistent upload and preview areas.
- Cyan interactive borders.
- Gold primary action accents where appropriate.
- Preserve upload, processing, and existing image workflows.

I. Image to Script

- Consistent prompt inputs.
- Refined selection controls.
- Clear labels and action hierarchy.
- Readable results and status indicators.
- Preserve existing generation functionality.

J. Script to Image

- Premium dark prompt editor.
- Consistent model and style selectors.
- Clearly visible generation action.
- Refined image preview layout.
- Preserve existing model choices and generation behavior.

K. Swap

- Consistent upload cards and preview sections.
- Clear primary and secondary actions.
- Refined loading and result states.
- Preserve all existing swap functionality.

---

7. ICONS AND INTERACTION STATES

Use one consistent icon style throughout the app.

- Normal icons: muted silver-grey.
- Active icons: sky blue/cyan.
- Premium accents: royal gold.
- Disabled icons: subdued grey.
- Focused controls: visible cyan outline.
- Selected premium components: subtle gold outline.

Do not mix unrelated icon styles or use emoji as a substitute for existing interface icons.

Preserve existing icon meanings and click actions.

---

8. RESPONSIVE DESIGN

- Prioritize mobile layouts.
- Support existing tablet and desktop layouts.
- Prevent horizontal overflow.
- Avoid clipped text and overlapping controls.
- Respect device safe areas.
- Ensure forms remain usable with the keyboard open.
- Keep buttons and touch targets comfortably usable.
- Maintain image proportions across screen sizes.

---

9. IMPLEMENTATION REQUIREMENTS

Before making changes:

1. Inspect the existing codebase and theme-token architecture.
2. Identify all targeted non-Home UI files.
3. Reuse the existing shared theme-token file if available.
4. Do not create duplicate theme systems.
5. Map the palette to semantic tokens.
6. Replace hardcoded colours carefully.
7. Preserve dynamic colours, status indicators, and user-selected preferences.
8. Check both StyleSheet colours and inline icon/button colours.
9. Make changes in small, verifiable steps.

Strictly Preserve

- Home and Welcome screens.
- Route definitions and redirects.
- APIs and request/response formats.
- Backend logic.
- Existing features and navigation.
- State management and saved user choices.
- GitHub Actions workflows.
- APK build and GitHub Release configuration.
- Render deployment configuration.

Do not replace real functionality with mock data or remove existing options.

---

10. VALIDATION AND FINAL REPORT

After implementation:

- Run available local checks.
- Verify imports and theme-token references.
- Run available tests and the production build.
- Inspect all modified screens.
- Check typography, alignment, contrast, clipping, and responsive behavior.
- Verify that existing features and navigation remain intact.
- Report the changed files, checks performed, build results, and unresolved issues.

Do not claim successful validation unless the relevant checks were actually executed.

---

FINAL DESIGN GOAL

Create a unified luxury AI application inspired by the supplied references:

BLACK LEATHER + ROYAL GOLD + SKY BLUE NEON + PREMIUM GLASSMORPHISM.

The app should feel elegant, futuristic, polished, readable, and consistent across every targeted screen.

Prioritize usability, premium visual hierarchy, accurate text alignment, and preservation of existing functionality over excessive decoration.

## கட்டம்-வாரியான handoff பதிவு

- ஒவ்வொரு step முடிந்ததும், `future/step-N-<சுருக்கப்பெயர்>.md` என்ற file-ல் முடிந்த scope, மாற்றிய files, verification/build முடிவு, commit SHA, blockers, அடுத்த step மற்றும் pending approval-களை பதிவு செய்யவும். Step 1-க்கு உள்ள `step-1-audit.md` பெயரிடும் முறையைப் பின்பற்றவும்.
- `future/README.md`-ல் தற்போதைய status, முடிந்த step, அடுத்த step, அந்த step-க்கு தேவையான approval, தொடர்புடைய handoff file link ஆகியவற்றைப் புதுப்பிக்கவும். Verified evidence மட்டுமே குறிப்பிடவும்; secrets சேர்க்க வேண்டாம்.
- Handoff docs-ஐ GitHub-க்கு normal commit/push ஆகச் சேர்க்கவும்; இது `Build APK` workflow-ஐ trigger செய்யும் முறை அல்ல. Docs-only update-க்கு APK build தேவையில்லை.
- Code changes-ஐ ஒரே feature branch-ல் commit/push செய்யவும். ஏழு திட்டமிட்ட படிகளும் முடிந்து approval கிடைத்த பிறகே அந்த branch-ஐ `main`-க்கு merge செய்யவும்; பின்னர் `main`-இலிருந்து `Build APK`-ஐ ஒரே முறை கைமுறையாக trigger செய்யவும். இடைப்பட்ட build-கள் செய்ய வேண்டாம்.
- Build trigger-க்கு முன் Release side effect-ஐ தெரிவிக்கவும்: workflow APK-ஐ GitHub Release-ல் வெளியிடும்; அதே tag-ஐ rerun செய்தால் ஏற்கெனவே உள்ள release/tag-ஐ delete செய்து மீண்டும் உருவாக்கும். Render redeploy input இயல்பாக false.

## அடுத்த நிலை
Step 2-ல் கேட்ட design system-ஐ முடித்து/present செய்த பிறகே app UI-ஐ மாற்றத் தொடங்கவும். ஏழு கட்ட பரிந்துரை மற்றும் உறுதிப்படுத்தப்பட்ட route/handler map `step-1-audit.md`-ல் உள்ளது. Step 2 இன்னும் தொடங்கப்படவில்லை.
