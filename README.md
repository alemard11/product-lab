# product-lab
A product management playground for experimenting with features, UI improvements, and GitHub workflows.

## Run locally

From the repository root, run `python3 -m http.server 8000` and open the served app in a browser. No build or dependency installation is required.

## Roadmap

Select **Roadmap** to see ideas on a monthly timeline. Select an idea (or create a new one) to set optional target months for **Alpha**, **Beta**, **EA** (Early Access), and **GA** (General Availability). Stages follow that order; multiple stages may share a month, and stages may be left unscheduled. Year controls let you view targets across years. On smaller screens, scroll the timeline horizontally.

Ideas and milestone dates are saved in this browser's local storage, including after reload. Existing ideas start unscheduled; dates are planning targets rather than release guarantees. Data is not shared across browsers or devices.

## Feedback survey (Amplitude)

The top-bar Feedback button opens a published Amplitude Guides & Surveys survey on demand. Setup is incomplete until both configuration values are filled in. No survey is created by this code.

1. In Amplitude project `default` (project ID `883218`), enable Guides & Surveys and create **Product Lab feedback** with these questions:
   - How easy was Product Lab to use today? Scale 1–5, from Very difficult to Very easy.
   - How satisfied are you with Product Lab? Scale 1–5, from Very dissatisfied to Very satisfied.
   - What's one thing we could improve? Optional open text.
   - Thank-you: Thanks! Your feedback helps us improve Product Lab.
2. Set the survey trigger to **None**, allow the website URL in page targeting, and publish the survey.
3. Copy the project's public **API key** from project settings and the published survey's **key**. The survey key is the value used by `engagement.gs.show(key)`; do not substitute the numeric project ID or assume a numeric survey ID is the key.
4. In `index.html`, find `FEEDBACK_CONFIG` and fill `apiKey` and `surveyKey`. Set `serverZone` to `EU` only for an EU-hosted Amplitude project. Never put an Amplitude secret key in website code.
5. Deploy the updated branch through your existing website hosting workflow. Click Feedback and complete the survey, then verify the response in Amplitude.

The SDKs load when Feedback is first selected. Analytics and Engagement share one API key and anonymous device identity through the Engagement plugin; the plugin forwards survey events and responses to Amplitude. Autocapture is disabled. No SDK requests are made while either configuration value is blank. Loading failures produce a retry message; reload the page before retrying.

The launch call bypasses audience and frequency limits, but still obeys page targeting. Configure page targeting to include every website page where Feedback should work.

Reference: [Amplitude Guides & Surveys Web SDK](https://amplitude.com/docs/sdks/guides-and-surveys/sdk).

Validation: page JavaScript syntax and mocked checks for missing configuration, successful launch, initialization reuse, script failure, and button recovery. Live ingestion requires real project and survey keys.
