
## Creating Sample Automation Sequences in `WORKFLOW_EXAMPLES.md`

To clearly illustrate your system’s automation capabilities, `WORKFLOW_EXAMPLES.md` should include step-by-step sample “workflows” for common query types. Each workflow specifies the browser automation sequence (using MCP commands) carried out by your system in response to user input. Here’s how to structure and present these examples:

### 1. Product Search

#### Example Query
> “Find me laptops under ₹50,000”

#### Sample MCP Workflow (Amazon)
- **browser_navigate:** Go to `https://www.amazon.com/s?k=laptop`
- **browser_scroll:** Scroll down by 2000 pixels to load more results
- **browser_wait:** Wait for 2 seconds to allow content to load

#### Sample MCP Workflow (Flipkart)
- **browser_navigate:** Go to `https://www.flipkart.com/s?k=laptop`
- **browser_scroll:** Scroll down by 2000 pixels
- **browser_wait:** Wait for 2 seconds
- **browser_type:** Enter `laptop under ₹50000` in `input[name='q']`
- **browser_press:** Press `Enter` to trigger search

### 2. Price Comparison

#### Example Query
> “Compare the prices of Samsung Galaxy M15 on Amazon and Flipkart”

#### Sample MCP Workflow (Both Sites)
- **browser_navigate:** Go to the respective site search URL with `Samsung Galaxy M15`
- **browser_scroll:** Scroll to ensure all results are loaded
- **browser_wait:** Allow time for dynamic content to appear

| Command            | Amazon Step                           | Flipkart Step                              |
|--------------------|---------------------------------------|--------------------------------------------|
| browser_navigate   | `https://www.amazon.com/s?k=Samsung+Galaxy+M15` | `https://www.flipkart.com/s?k=Samsung+Galaxy+M15` |
| browser_scroll     | `2000`                                | `2000`                                     |
| browser_wait       | `2`                                   | `2`                                        |
| browser_type       | —                                     | (if filtering) `input[name='q']`           |
| browser_press      | —                                     | (if filtering) `Enter`                     |

### 3. Flight Price Search

#### Example Query
> “Search for flights from Delhi to Mumbai next Friday”

#### Sample MCP Workflow (Sample Travel Site)
- **browser_navigate:** Go to `https://www.exampleflightsite.com`
- **browser_type:** Enter `Delhi` in the `From` field
- **browser_type:** Enter `Mumbai` in the `To` field
- **browser_type:** Enter date (e.g., `YYYY-MM-DD`) in the date picker
- **browser_press:** Click or press `Search`
- **browser_wait:** Wait for results to load
- **browser_scroll:** Scroll if necessary to load all fares

### 4. Multi-site Comparison

#### Example Query
> “Show me wireless headphones under ₹2000 on Amazon and Flipkart”

#### Sample Workflow Steps

For **Amazon:**
- browser_navigate (`https://www.amazon.com/s?k=wireless+headphones`)
- browser_scroll (`2000`)
- browser_wait (`2`)

For **Flipkart:**
- browser_navigate (`https://www.flipkart.com/s?k=wireless+headphones`)
- browser_scroll (`2000`)
- browser_wait (`2`)
- browser_type (`wireless headphones under ₹2000` in `input[name='q']`)
- browser_press (`Enter`)

## Tips for Writing `WORKFLOW_EXAMPLES.md`

- For each query type, include a short natural language example.
- Provide separate step sequences for each supported site, noting any site-specific actions (like `browser_type` or extra waits).
- Use simple Markdown formatting for readability (bullets, code blocks, or tables as appropriate).
- Clearly indicate where selectors or keywords are different across sites.
- If a query can have multiple valid workflows, describe them or note the differences.

By presenting your examples using these guidelines, you will make it easy for users, testers, and developers to understand how queries map to browser automation workflows within your system.

[1] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/83300653/06873ca5-adaa-434f-8fd0-04579e0d2c39/app.py
[2] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/83300653/39dcb870-0f6d-4fb4-95db-521acff65861/requirements.txt
