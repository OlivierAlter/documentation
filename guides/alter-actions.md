# Alter Actions Guide

## Goal

Learn how to create and configure Alter Actions — customizable AI workflows that automate tasks on your Mac with voice triggers, conditional execution, and integrated tools.

## What is an Alter Action?

An **Alter Action** is an advanced automation workflow that combines:

- **AI instructions** - System prompts that define how the AI should behave
- **Triggers** - Voice commands, hotkeys, or conditional execution
- **Context** - Access to selected text, files, active applications
- **Tools** - Configured integrations with your Mac apps and 2000+ external services
- **Output formats** - How results are displayed (markdown, code, inline insertion)

Think of an Alter Action as a "specialized AI assistant" customized for a specific task.

**Examples:**
- "Code Explainer" — Select code, hold voice hotkey, say "explain", get detailed breakdown
- "Meeting Notes" — Paste transcript, AI extracts decisions, action items, and creates Gmail draft
- "Email Draft" — Select text, triggers an action that formats it as an email

## Opening the Action Editor

### Method 1: From Menu Bar (Fastest)
1. Click the **Alter menu icon** in the menu bar (top right)
2. Select **Action Editor**
3. Done! Action Editor opens immediately

![Menu Bar](https://alterhq.com/assets-doc/images/tools/menu-bar-action-editor.webp)

### Method 2: From Options Menu
1. Open Alter window (hover over notch or press hotkey)
2. Click **⋯** (three dots) in top right
3. Select **Action Editor**

![Options Menu](https://alterhq.com/assets-doc/images/tools/options-menu-action-editor.webp)

### Method 3: Keyboard Shortcut
Press **⌘ E** (Command + E) to open the Action Editor directly

> **Tip**: The keyboard shortcut is the fastest method after you've memorized it.



## Action Editor Walkthrough

The Action Editor has 7 main sections, each controlling different aspects of your action. Use the left panel to navigate between tabs.

### 1. General Settings

Configure basic metadata and execution context.

![General Tab](https://alterhq.com/assets-doc/images/tools/action-editor-01-general.webp)

**Fields:**
- **Name** - Human-readable action name (e.g., "Code Explainer")
- **Category** - Organize actions by type (code, productivity, business, etc.)
- **Workspace** - Assign to a specific workspace (optional)
- **Include Profile** - Include user profile information in AI context (toggle)

**Visibility Options:**
- **Show only when running** - Action only appears if an app is running
- **Show only when active** - Action only appears if an app has focus
- **Workspace context** - Choose which workspace(s) see this action

> Each action gets a unique UUID automatically. You don't need to set this yourself.

### 2. System Prompt

Define AI instructions and parameters for the model.

![System Prompt Tab](https://alterhq.com/assets-doc/images/tools/action-editor-02-systemprompt.webp)

**Fields:**
- **System Prompt** - Core AI instructions (e.g., "You are an expert code reviewer...")
- **Parameters Section** - Define input fields users can customize

**Example System Prompt:**
```
# IDENTITY AND PURPOSE
You are an expert software engineer who explains code clearly
and accessibly to developers of all skill levels.

# STEPS
1. Analyze the provided code
2. Identify its purpose and key components
3. Explain each section in simple terms

# OUTPUT INSTRUCTIONS
- Use markdown formatting
- Include code examples where helpful
- Keep language clear and non-technical where possible
```

**Parameters** allow dynamic inputs before execution:
- Text input fields
- Dropdown selections
- Multiple choice

### 3. User Prompt

Template for the user-facing prompt that gets sent to the AI.

![User Prompt Tab](https://alterhq.com/assets-doc/images/tools/action-editor-03-userprompt.webp)

**Fields:**
- **User Prompt** - Template with parameter interpolation

**Using Context Variables:**

Wrap variables in `{{ }}` to insert dynamic content:

```
Please explain this code:

{{ textSelection }}

Explanation detail: {{ detailLevel }}
```

**Available Context Variables:**
- `{{ textSelection }}` - Currently selected text
- `{{ filePath }}` - Path to selected file
- `{{ clipboard }}` - Clipboard contents
- Custom parameters you defined in System Prompt

### 4. When to Show

Control when and where this action appears.

![When to Show Tab](https://alterhq.com/assets-doc/images/tools/action-editor-04-whentoshow.webp)

**Visibility Conditions:**

- **Installed Applications** - Show action only in specific apps
  - Click **+ Add** to select apps (VSCode, Xcode, Safari, etc.)
  - Action only appears if one of these apps is running or active

- **Application is running** - Action requires the app to be running
- **Application has focus** - Action only works when app is in foreground
- **Web browser tab contains** - Show action when browsing specific domains
- **Has content** - Show action only when context is available

**Example Setup:**
- "Code Explainer" action → Show in VSCode, Xcode, and dev.zed.Zed
- "Email Draft" action → Show when app has focus
- "Web Search" action → Show when Safari tab contains "google.com"

### 5. Automation

Configure execution behavior, schedules, and background processing.

![Automation Tab](https://alterhq.com/assets-doc/images/tools/action-editor-05-automation.webp)

**Fields:**

- **Background Job** - Run action in background without showing UI
- **Schedules** - Execute action at specific times (e.g., "Every Monday at 9 AM")
  - Click **+ Add Schedule** to set up recurring execution
- **Quick Action** - Execute the next "Quick Action" automatically after this completes
  - Use for action chaining (first action → output → next action)

**Example Use Case:**
1. "Fetch Meeting Transcript" runs in background
2. "Generate Meeting Notes" runs as Quick Action next
3. "Email Report" auto-executes with notes as input

### 6. Tools

Scope which tools are available for this action.

![Tools Tab](https://alterhq.com/assets-doc/images/tools/action-editor-06-tools.webp)

**Tool Configuration:**

- **Disable Tools** - Toggle off individual tools to restrict functionality
- **Tools Section** - See which tools are available
  - When empty: All tools are available
  - When configured: Only selected tools are available

**Why Scope Tools?**
- Reduce AI decision overhead (focus on relevant tools)
- Speed up action execution
- Improve security (limit what actions can access)

**Example:**
- "Send Email" action → Enable only Mail & Contacts
- "Calendar Event" action → Enable only Calendar & Notifications
- "Code Analyzer" action → Enable only Finder & Script Editor

### 7. Model

Select AI model and adjust creativity level.

![Model Tab](https://alterhq.com/assets-doc/images/tools/action-editor-07-model.webp)

**Fields:**

- **Model** - Choose specific AI model for this action
  - Leave empty to use user's default model setting
  - Or select: Claude, GPT-4, local model, etc.

- **Temperature** - Adjust creativity vs. precision
  - **0.0** - Deterministic (consistent, predictable)
  - **0.5** - Balanced (default)
  - **1.0** - Creative (unpredictable, exploratory)

**Recommendations:**
- **Code/Analysis Tasks** - Temperature 0.3-0.5 (precision)
- **Creative Tasks** - Temperature 0.7-0.9 (variety)
- **General Tasks** - Temperature 0.7 (default, balanced)

## Best Practices

### 1. Clear Action Names
✅ "Code Explainer" — Describes what it does
❌ "Action 1" — Too vague

### 2. Specific System Prompts
✅ "You are an expert code reviewer who identifies bugs and suggests improvements"
❌ "Help me with code" — Too generic

### 3. Scope Tools Appropriately
✅ Email action uses only Mail + Contacts
❌ Email action has access to all tools (unnecessary overhead)

### 4. Use Context Variables
✅ `{{ textSelection }}` — Always works
❌ Manual copy/paste — Error-prone, less elegant

### 5. Conditional Visibility
✅ "Code Explainer" only in VSCode + Xcode
❌ "Code Explainer" available everywhere (cluttered menu)

### 6. Test with Sample Data
✅ Test action with real code samples before sharing
❌ Deploy untested action to team

## Common Action Examples

### Example 1: Code Explainer

**Setup:**
- Name: "Explain Code"
- Category: code
- Installed Apps: VSCode, Xcode
- System Prompt:
  ```
  You are an expert programmer who explains code clearly
  and accessibly to developers of all skill levels.
  
  Analyze the provided code and explain:
  1. What it does
  2. How each component works
  3. Why it's written this way
  ```
- User Prompt: `Please explain this code:\n\n{{ textSelection }}`
- Consumer: markdown
- Temperature: 0.5

### Example 2: Email Draft Creator

**Setup:**
- Name: "Draft Email"
- Category: productivity
- When to Show: Mail app active
- System Prompt:
  ```
  You are an expert business communicator who crafts
  professional, clear emails.
  
  Transform the provided notes into a professional email.
  Include:
  - Clear subject line
  - Warm greeting
  - Well-structured body
  - Professional closing
  ```
- User Prompt: `Transform this into a professional email:\n\n{{ textSelection }}`
- Tools: Enable only Mail
- Consumer: in-place
- Temperature: 0.6

### Example 3: Scheduled Daily Brief

**Setup:**
- Name: "Daily Brief"
- Category: productivity
- Automation: Schedule for 9:00 AM daily
- Background Job: Enabled
- System Prompt: `Generate a daily brief of priorities and weather`
- Consumer: markdown
- Temperature: 0.5

## Voice Triggers

Once created, assign voice hotkeys to trigger actions:

1. **System Settings** → Alter → Voice Triggers
2. **Click "+ Add Trigger"**
3. **Select Action** from dropdown
4. **Assign Trigger Phrase** (e.g., "explain" for Code Explainer)
5. Save

**Usage:**
- Hold voice hotkey + say trigger phrase
- Action executes with current context

## x-callback-url Integration

Trigger Alter actions from **any application** using special URLs. This enables powerful cross-app automation workflows.

### What is x-callback-url?

x-callback-url is an inter-app communication protocol that lets applications trigger actions in each other through formatted URLs. It works bidirectionally:

- **Inbound** - Trigger Alter actions from other apps (Shortcuts, Notes, Safari, etc.)
- **Outbound** - Create links in Alter that open other apps (Bear, OmniFocus, Drafts, etc.)

### Getting Your Action's Callback URL

Every action has a unique `alter://` URL scheme:

1. **Open Action Editor** - `Shift + Cmd + E`
2. **Select an action**
3. **Go to General tab**
4. **Find "URL Callback" section**
5. **Copy the `alter://` URL**

**Format:**
```
alter://action/{action-id}?input=VALUE&param2=VALUE
```

### Triggering Alter Actions from Other Apps

**Example 1: Web Search from Safari**
```
alter://action/ask-web?input=What+is+Alter+MacOS
```
Clicking this link opens Alter and runs a web search query.

**Example 2: Code Explainer with Input**
```
alter://action/explain-code?input=const+hello+%3D+%28%29+%3D%3E+%7B%7D
```
Passes pre-filled code to your Code Explainer action.

**Example 3: Using in Apple Shortcuts**
1. Create a new Shortcut
2. Add "Open URL" action
3. Paste your `alter://` URL
4. Run the shortcut to trigger the action

**Example 4: From a Note App**
```markdown
[Explain This Code](alter://action/explain-code?input=myFunction())
```
Click the link to trigger the action with pre-filled content.

### Creating Callback Links from Alter

Generate links in Alter that open other apps:

**Create Bear Note from Alter:**
```
bear://x-callback-url/create?title=Meeting+Notes
```

**Add to OmniFocus:**
```
omnifocus:///add?name=New+Task&note=Details
```

**Send Telegram Message:**
```
tg://msg?text=Important+update
```

### Use Cases

**Workflow Automation:**
- Trigger action from Calendar → Generate meeting notes → Create email draft
- Select text in Safari → Run Code Explainer → Save result to Notes

**Multi-App Integration:**
- Notion button → Trigger Alter action → Update task status
- Shortcut runs on schedule → Executes Alter action → Sends result to Slack

**Information Transfer:**
- Copy text → Trigger action with callback → Open result in external app
- No manual copying/pasting needed

### Best Practices

✅ **DO:**
- URL-encode special characters (`+` for spaces, `%20` for spaces, `%3D` for `=`)
- Test URLs in Safari first before using in other apps
- Use descriptive action IDs (avoid generic names)
- Document callback URLs in action descriptions

❌ **DON'T:**
- Share sensitive data in URLs (visible in history/logs)
- Assume apps will always be installed (provide fallbacks)
- Use unencoded special characters

### Testing Callback URLs

**Quick Test in Safari:**
1. Paste `alter://action/your-action-id` in address bar
2. Press Enter
3. Alter should open with action ready

**Test with Parameters:**
```
alter://action/explain-code?input=function%20test()%20{}
```

> **Note**: If the action doesn't trigger, verify:
> - Action ID is correct (check in Action Editor)
> - URL is properly encoded
> - Required parameters are included

## Troubleshooting

### Action doesn't appear in menu
- Check **When to Show** settings
- Verify app is running/active (if configured)
- Ensure action is **enabled**

### Action runs but produces poor output
- Review **System Prompt** — be more specific
- Adjust **Temperature** (lower for precision, higher for creativity)
- Check **User Prompt** — ensure variables are correct

### Voice trigger not working
- Verify hotkey is configured in Settings
- Check microphone permissions
- Test with manual trigger first

### Tools not available in action
- Go to **Tools** tab
- Verify tools aren't disabled
- Check system permissions for the tool

## Related Docs

- [Tools & Integrations](./integrations.md) — Learn about available tools
- [Alter Settings](./alter-settings.md) — Configure global model and voice settings
- [Voice Commands](./dictation.md) — Set up voice triggers
- [Quick Actions](./integrations.md#quick-actions) — Chain actions together
- [x-callback-url Guide](https://alterhq.com/blog/alter-callback-urls-guide) — Deep dive into callback URL automation
- [URL Callbacks Reference](./url-callbacks.md) — x-callback-url protocol details

---

**Ready to build?** Open Alter, press `Shift + Cmd + E`, and start creating your first action!

**Want to automate across apps?** Use x-callback-urls to trigger actions from Safari, Shortcuts, Notes, or any app that supports URL schemes.
