# Make Scenario – UrbanKitchen AI Customer Service Assistant

This folder contains the automation built in [Make](https://www.make.com/) for this project.

- **Live scenario (read-only, view in Make):** https://eu1.make.com/public/shared-scenario/DXwtum02BQ2/urban-kitchen-ai-customer-service-assis
- **Exported blueprint:** [`UrbanKitchen.blueprint.json`](./UrbanKitchen.blueprint.json) — the full scenario export. It can be imported directly into a Make account (**Create a new scenario → Import Blueprint**) to inspect or run it.

## What the scenario does

The scenario receives a customer email via a Mailhook, analyzes it with Google Gemini (classification, information extraction, summary, confidence score and a draft reply), looks up the customer and order in Google Sheets, routes the inquiry through one of four business paths (order status / product question / complaint-refund / human review), and finally either sends an automatic reply by email or creates a task for a customer service representative — logging every inquiry along the way.

The full technical write-up of the scenario — module by module, routing logic, error handling and optimization — is in [`/docs/step_E_make_implementation.md`](../docs/step_E_make_implementation.md).
