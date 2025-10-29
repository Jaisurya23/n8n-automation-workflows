## n8n Workflows Collection

This repository contains several n8n workflows for scraping, enrichment, and email processing. All sensitive API keys/tokens have been redacted and replaced with placeholders so it’s safe to publish to Git.

### What's Included
- `company_name_revenue_generate_from_llm.json`: Enriches company rows from Google Sheets with revenue estimates using a Gemini LLM and writes results back to Sheets.
- `email_filtered_using_code.json`: Reads Gmail messages, filters using custom code/keywords, and stores matches in Google Sheets.
- `multiple_city_seriapi_search__not_completed_.json`: Uses SerpAPI Google Maps to fetch business data across paginated results, writes to Google Sheets. Marked not completed.
- `reddit_post_scabber_edited_and_finetuned_.json` and `reddit_post_scabber_edited_and_finetuned__copy.json`: Searches Reddit, filters/scores posts, applies LLM analysis, and appends insights to Google Sheets.
- `reddit_scrapping__template_.json`: A template version of the Reddit workflow with LLM-based classification and summarization.
- `scrape_company_name_with_seriapi.json`: SerpAPI Google Maps-based company scraping with pagination, writes structured data to Google Sheets.
- `scrape_company_name_with_the_apify_api.json`: Calls Apify Google Places crawler and appends results to Google Sheets.
- `web_scarping_through_google_custom_search.json`: Uses Google Custom Search API (CSE) to extract company details and writes to Google Sheets.

### Redacted Secrets (Placeholders)
Replace the placeholders below with your real values inside n8n after import.

- SerpAPI
  - `REPLACE_WITH_SERPAPI_API_KEY`
- Apify
  - `REPLACE_WITH_APIFY_API_TOKEN`
- Google Custom Search (CSE)
  - `REPLACE_WITH_GOOGLE_CSE_API_KEY`
  - `REPLACE_WITH_GOOGLE_CSE_CX`

Note: n8n credential references like `credentials.googleSheetsOAuth2Api.id` are safe identifiers and not secrets. Actual OAuth secrets are stored in your n8n credentials store, not in these files.

### Prerequisites
- An n8n instance (desktop or self-hosted)
- Accounts/keys for required services as needed by each workflow:
  - Google Sheets (OAuth credential in n8n)
  - Gmail (OAuth credential in n8n) for `email_filtered_using_code.json`
  - SerpAPI key for Serp-based workflows
  - Apify API token for Apify workflow
  - Google Custom Search API key and CX for CSE workflow
  - Reddit OAuth App/credential configured in n8n for Reddit workflows

### Importing Workflows into n8n
1. Open n8n → Workflows → Import from File.
2. Select any of the `.json` files in this folder.
3. After import, open the workflow and set credentials on nodes that show missing credentials.
4. Replace any placeholder values in HTTP Request nodes with your real keys/tokens:
   - SerpAPI: set `api_key` to your key.
   - Apify: set `token` query or URL parameter to your token.
   - Google CSE: set `key` and `cx` query parameters.
5. Update Google Sheet `documentId`/`sheetName` if you want to point to your own spreadsheets.
6. Save and run with “Test workflow” to validate.

### Recommended: Use n8n Credentials Instead of Hardcoding
Where possible, move secrets into n8n Credentials rather than hardcoding in nodes. For HTTP nodes, you can:
- Use HTTP Credentials (API Key/Bearer) and reference them in the node.
- Or store values in n8n Variables/Environment and inject via expressions.

### Security Notes
- Do not commit real API keys, OAuth client secrets, or tokens to Git.
- This repo replaces any detected keys/tokens with placeholders for safe sharing.
- Review and rotate any keys that were previously exposed.

### Troubleshooting
- If a node shows “Credentials not found”: create/select the matching credential in n8n.
- HTTP 401/403: verify you replaced the placeholder with a valid key/token and the service is enabled.
- Google Sheets write errors: ensure the target sheet exists and your credential has access.

### License
Provided as-is for your automation use. Replace keys, test in your environment, and ensure compliance with each API’s terms.


