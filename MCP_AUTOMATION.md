## What is MCP?

MCP (Micro Command Protocol) is a set of standardized browser automation commands. In this project, queries are parsed by an LLM and mapped to an MCP workflow: a sequence of actions that can be executed in-browser via Playwright to automate search and extraction on e-commerce and travel sites.

## Supported MCP Commands

| Command           | Parameters                                   | Description                                           |
|-------------------|----------------------------------------------|-------------------------------------------------------|
| browser_navigate  | `value` (str, URL)                           | Open a specific web page.                             |
| browser_scroll    | `value` (int, pixel distance)                | Scroll down the web page by a specified amount.        |
| browser_wait      | `value` (int, seconds)                       | Pause for a number of seconds.                        |
| browser_type      | `selector` (str), `value` (str)              | Type into an input found by CSS selector.              |
| browser_press     | `value` (str, key name e.g. 'Enter')         | Press a specified keyboard key (e.g., Enter).          |

## Automation Workflow: How It Works

1. **User types a natural query**, e.g. “Find me laptops under ₹50,000”.
2. The LLM parses the query and outputs:
    - `query_type` (e.g. "product_search")
    - `target_websites` (e.g. ["amazon", "flipkart"])
    - `search_params` (like category, budget, keywords)
3. The application maps this to MCP workflows for each site, e.g.:

    **Amazon:**
    ```json
    [
      {"command": "browser_navigate", "value": "https://www.amazon.com/s?k=laptop"},
      {"command": "browser_scroll", "value": 2000},
      {"command": "browser_wait", "value": 2}
    ]
    ```
    **Flipkart:**
    ```json
    [
      {"command": "browser_navigate", "value": "https://www.flipkart.com/s?k=laptop"},
      {"command": "browser_scroll", "value": 2000},
      {"command": "browser_wait", "value": 2},
      {"command": "browser_type", "selector": "input[name='q']", "value": "laptop under ₹50000"},
      {"command": "browser_press", "value": "Enter"}
    ]
    ```

4. **Execution:**  
   In code (`scrape_site` in `app.py`), Playwright processes these steps in order:  
   - Navigates to the URL
   - Scrolls
   - Waits for content to load
   - Types/presses keys as needed
   - Then extracts search results via site-specific CSS selectors  

## Example: Full Workflow for a Price Comparison

**Query:** "Compare iPhone 14 prices on Amazon and Flipkart"

- Parsed query → MCP workflows generated for both sites.
- The system applies:
    - Navigate to each site’s search results
    - Scroll/wait
    - For Flipkart, type the search term and press 'Enter'
    - Yield a uniform structure for scraping

## Adding a New Command or Site

- **Update `generate_mcp_workflow`** to generate extra step(s) as needed for the new command or site.
- **Expand `scrape_site`** to interpret and act on new commands.

Example for a new command:
```python
elif step['command'] == 'browser_click':
    await page.click(step['selector'])
```
And document in the table above!

## Error Handling

- Each command logs its action.
- Non-critical errors (missing elements, etc.) are logged and workflow continues, so partial results are possible.

## References in Code

- **Command execution loop**: See `scrape_site()` in `app.py`
- **Workflow generation**: See `generate_mcp_workflow()` in `app.py`

By presenting your documentation in **sections** (Overview > Commands > Workflow Walk-through > Adding/Expanding Commands > Error Handling > Code References), you’ll make it easy for readers to understand, maintain, and extend the automation system.

[1] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/83300653/06873ca5-adaa-434f-8fd0-04579e0d2c39/app.py
[2] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/83300653/39dcb870-0f6d-4fb4-95db-521acff65861/requirements.txt
