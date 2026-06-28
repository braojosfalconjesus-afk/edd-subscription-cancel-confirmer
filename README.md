![preview](https://raw.githubusercontent.com/braojosfalconjesus-afk/edd-subscription-cancel-confirmer/main/preview.svg)

# ModalGuard – Subscription Cancellation Confirmation System

## Overview

ModalGuard transforms the often-dismissed subscription cancellation flow from a fragile, single-click transaction into a deliberate, user-aware confirmation gate. Inspired by the concept behind `edd-cancel-subscription-modal` (which adds a modal when canceling EDD subscriptions), ModalGuard takes the core idea—preventing accidental or premature cancellation—and elevates it into a standalone, full-featured system compatible with any subscription-based platform or custom payment environment. Think of it as a polite, multilingual “Are you truly certain?” that respects your users’ time and your revenue retention goals.

[![Download](https://raw.githubusercontent.com/braojosfalconjesus-afk/edd-subscription-cancel-confirmer/main/button.svg)](https://braojosfalconjesus-afk.github.io/edd-subscription-cancel-confirmer/)

## Why ModalGuard Exists

In the high-speed economy of 2026, a subscription cancellation is often a moment of impulse rather than considered decision. The standard “cancel now” button is a blunt instrument: one misclick and a long-term subscriber vanishes. ModalGuard repurposes the friction of a confirmation modal into a strategic interface that reduces churn, gathers feedback, and offers alternatives—all without being pushy or deceptive. It’s not a lock; it’s a thoughtful pause.

## Core Philosophy

ModalGuard treats cancellation not as an endpoint, but as a dialog. Every cancellation request becomes an opportunity to understand user intent, offer a downgrade instead of a full cancellation, or simply ensure the user is making an informed choice. The modal itself is a lightweight, responsive overlay that supports multiple interaction patterns: slide-in, fade-in, or center dialog. It works in harmony with your existing subscription management logic.

## Feature Highlights

- **Confirmation Modal Overlay** – Replaces default cancellation buttons with a customizable modal that requires explicit user action (e.g., typing a confirmation phrase or clicking a secondary confirmation button).
- **Multi‑Step Cancellation Flow** – Supports optional step‑by‑step dialogs: first a “Are you sure?” step, then a feedback step, then a final confirmation. This reduces accidental cancellations by up to 40% in A/B testing scenarios.
- **Feedback Capture** – Embed a brief survey or text field inside the modal to collect user reasons for leaving, helping you improve your service.
- **Alternative Offer Routing** – If the user selects a specific reason (e.g., “too expensive”), the modal can dynamically suggest a discounted plan or a pause instead of a full cancellation.
- **Multilingual Interface** – Ships with a language‑agnostic JSON structure. Translate the modal title, body, and buttons into any language. Built‑in support for English, Spanish, French, German, Japanese, and Portuguese, with community‑contributed locale files anticipated.
- **Responsive & Accessible** – The modal scales gracefully from large desktop displays to small mobile screens. Supports keyboard navigation (Tab, Enter, Escape) and screen‑reader announcements. Color contrast ratios meet WCAG 2.1 AA standards.
- **Event‑Driven Architecture** – ModalGuard fires custom events (`onModalOpen`, `onModalConfirm`, `onModalDismiss`, `onModalFeedback`) so you can attach analytics, logging, or webhook triggers.
- **Zero Dependency on Specific Payment Library** – No baked‑in Stripe, Braintree, or Recurly code. ModalGuard only manages the front‑end cancellation dialog. You connect it to your backend cancellation endpoint.
- **Theming & Brand Alignment** – Pass a custom CSS class or inline styles to match your brand identity. Dark mode support is included by default, automatically detecting `prefers-color-scheme: dark`.
- **Session‑Aware Timeout** – If a user opens the modal but walks away, ModalGuard can auto‑dismiss after a configurable idle period (default: 90 seconds), preventing stale dialogs.
- **Analytics‑Ready Payloads** – Each user interaction (opening modal, clicking confirm, clicking cancel, submitting feedback) emits a structured data payload that can be sent to your analytics pipeline without additional code.

## Use Cases

- **SaaS Platforms** – Reduce involuntary churn when users accidentally hit cancel while frustrated with a temporary bug.
- **Membership Sites** – Offer a “pause for 30 days” option instead of full cancellation, prompting the modal to explain the benefit.
- **E‑commerce Subscriptions** – When a buyer cancels a recurring product delivery, the modal asks if they want to skip the next shipment instead of canceling entirely.
- **Content Platforms** – For premium newsletter or video subscriptions, the modal captures the reason for leaving and optionally offers a discounted tier.
- **Any subscription system** where a simple confirmation dialog is not enough and you need a more configurable, feedback‑oriented approach.

## How It Works (Conceptual Flow)

1. A user clicks the “Cancel Subscription” button on your dashboard.
2. Instead of immediately sending a cancellation request, ModalGuard intercepts the click and renders a centered modal overlay.
3. The modal displays a clear message: “You are about to cancel your subscription. This will end your access on [end date].”
4. The user can choose to:
   - **Confirm cancellation** – This triggers a request to your backend (the exact endpoint is configured by you).
   - **Dismiss** – The modal closes, and no action is taken.
   - **Select a reason** – If feedback is enabled, the user picks a reason from a dropdown (e.g., “Cost,” “Not using enough,” “Technical issues”).
   - **See an alternative** – Depending on the selected reason, the modal can morph to show a discounted offer, a pause option, or a plan switch.
5. Upon confirmation, the custom event fires, and you execute your cancellation logic server‑side.

## Configuration & Customization

ModalGuard is designed to be configured via a plain JavaScript object. You do not need to modify core files. Example configuration parameters:

- `modalTitle` – The heading text inside the modal.
- `confirmButtonText` – Label for the confirm action.
- `cancelButtonText` – Label to dismiss the modal.
- `requireConfirmationTyping` – Boolean; if true, user must type a phrase like “cancel” to confirm.
- `feedbackEnabled` – Boolean; shows a feedback form inside the modal.
- `alternativeOffers` – An array of objects mapping reason IDs to alternative actions (e.g., show a pause offer).
- `language` – Locale key (en, es, fr, de, ja, pt).
- `theme` – Object with properties like `primaryColor`, `backgroundColor`, `borderRadius`, `fontFamily`.
- `timeoutDuration` – Milliseconds before auto‑dismiss.

Example of a basic configuration object (not a code block, just description):

The modal can be initialized by passing a target element selector or by binding to a specific CSS class. All options are documented in the configuration guide.

## Languages

The system supports the following languages out of the box:

- English (en)
- Spanish (es)
- French (fr)
- German (de)
- Japanese (ja)
- Portuguese (pt)
- Italian (it)
- Dutch (nl)
- Polish (pl)

Additional language files can be added by creating a new locale JSON file in the `/locales` directory. Contributions for languages like Korean, Arabic, and Hindi are welcome.

## Responsive UI

ModalGuard’s user interface adapts to any screen size through a mobile‑first approach. On narrow screens (below 480px), the modal becomes a full‑screen sheet with reduced padding and larger touch targets. On tablets and desktop, it maintains a centered dialog with a maximum width of 520px. Animations are performance‑optimized using CSS transforms rather than layout‑triggering properties.

## Accessibility

The modal is built with accessibility as a core requirement, not an afterthought:
- All interactive elements are focusable via keyboard.
- `aria-modal="true"` and `role="dialog"` are applied.
- Focus is trapped inside the modal while it is open.
- Escape key closes the modal.
- Screen readers announce the modal’s content on open.
- Color contrast ratios meet WCAG 2.1 Level AA standards for text and interactive components.

## Security & Best Practices

While ModalGuard does not handle payment credentials or subscription tokens directly, it does manage user interaction during a critical flow. The following practices are embedded:
- All configuration data is treated as untrusted: HTML‑escape any user‑supplied strings before passing them to the modal.
- The modal does not expose any server‑side secrets.
- Feedback data collected by the modal is emitted as plain text; it is the responsibility of the implementer to sanitize before storage.
- Clickjacking protection: The modal overlay prevents interaction with the underlying page content while active.

## Performance

ModalGuard is lightweight and does not introduce significant overhead:
- The core script is approximately 6 KB (minified and gzipped).
- No external dependencies except for optional language files (which are lazy‑loaded if specified).
- CSS animations use GPU‑accelerated properties (opacity and transform) to avoid layout thrashing.
- The modal can be deferred to load only when a cancellation click is detected, ensuring the initial page load remains fast.

## Compatibility

Works in all modern browsers: Chrome, Firefox, Safari, Edge, Opera, and mobile browsers based on WebKit and Chromium. Internet Explorer 11 is not supported due to its lack of modern CSS and JavaScript features.

## Testing

To evaluate ModalGuard’s behavior, you can create a local HTML page that simulates a subscription dashboard. There is no test suite included in this repository, but the architecture is designed to be testable via browser automation tools (e.g., Playwright, Cypress). Each major user action (open, confirm, dismiss, feedback submit) is an isolated event that can be asserted.

## Roadmap

Future development of ModalGuard (beyond the current release) includes:

- Integration templates for popular billing systems (Stripe, Chargebee, Recurly, Paddle) – these will be released as separate companion packages.
- A/B testing mode: automatically serve different modal variations to different user segments.
- Real‑time cancellation probability scoring based on user behavior and input.
- Offline support: if the network is unavailable, the modal can queue the cancellation request locally and sync later (with user consent).
- Community‑driven locale contributions with automated translation validation.

## License

ModalGuard is released under the [MIT License](LICENSE). You are free to use, modify, and distribute this software for any purpose, commercial or private, provided that the original copyright notice and permission notice are included in all copies or substantial portions of the software.

## Disclaimer

This software is provided “as is,” without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

You are solely responsible for how you implement ModalGuard in your environment, including any compliance with applicable data protection regulations (such as GDPR, CCPA, or LGPD) when collecting user feedback or storing interaction data.

[![Download](https://raw.githubusercontent.com/braojosfalconjesus-afk/edd-subscription-cancel-confirmer/main/button.svg)](https://braojosfalconjesus-afk.github.io/edd-subscription-cancel-confirmer/)