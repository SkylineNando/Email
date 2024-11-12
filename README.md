---

# Email Suggestion Input with JavaScript

This repository provides a simple HTML and JavaScript solution that suggests popular email domains (providers) as the user types an email address. When the user types `@`, a list of suggestions from commonly used email providers appears, allowing for quick selection.

## Features

- Provides up to 8 popular email provider suggestions.
- Filters suggestions based on the user's input after typing `@`.
- Allows users to click on a suggestion to auto-fill the email input field.
- Customizable and easy to extend with more providers.

## Usage

1. **Clone the repository** or copy the HTML and JavaScript code provided below.
2. Open the HTML file in a web browser to test the email suggestion functionality.

### HTML & JavaScript Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Email Suggestion Input</title>
    <style>
        /* Basic styling for suggestion dropdown */
        #suggestions {
            display: none;
            position: absolute;
            background: white;
            border: 1px solid #ccc;
            list-style-type: none;
            padding: 0;
            margin: 5px 0;
            width: 100%;
            z-index: 10;
        }
        #suggestions li {
            padding: 8px;
            cursor: pointer;
        }
        #suggestions li:hover {
            background-color: #f0f0f0;
        }
    </style>
</head>
<body>
    <div class="col-md-6 form-group" style="position: relative;">
        <input name="email" type="email" id="email" placeholder="Seu email *" required oninput="suggestEmail(this)">
        <ul id="suggestions">
            <!-- Email suggestions will appear here -->
        </ul>
    </div>

    <script>
        function suggestEmail(input) {
            const providers = ["@gmail.com", "@yahoo.com", "@outlook.com", "@hotmail.com", "@icloud.com", "@aol.com", "@protonmail.com", "@zoho.com"];
            const suggestionsBox = document.getElementById("suggestions");
            suggestionsBox.innerHTML = ""; // Clear previous suggestions
            const value = input.value;

            // Show suggestions only if "@" is present
            if (value.includes("@")) {
                const [localPart, domainPart] = value.split("@");
                const suggestions = providers
                    .filter(provider => provider.includes(domainPart)) // Filter providers by what is typed after "@"
                    .map(provider => `<li onclick="selectSuggestion('${localPart}${provider}')">${localPart}${provider}</li>`)
                    .join(""); // Join list items into the suggestions box

                suggestionsBox.innerHTML = suggestions;
                suggestionsBox.style.display = suggestions ? "block" : "none";
            } else {
                suggestionsBox.style.display = "none";
            }
        }

        // Function to fill input with selected suggestion
        function selectSuggestion(email) {
            document.getElementById("email").value = email;
            document.getElementById("suggestions").style.display = "none";
        }
    </script>
</body>
</html>
```

### How It Works

1. **Event Trigger**: The `oninput` event on the email input field triggers the `suggestEmail` function every time the user types.
2. **Checking for "@"**: When the `@` symbol is detected in the input, the script splits the input into `localPart` (text before `@`) and `domainPart` (text after `@`).
3. **Filtering Providers**: The `providers` array contains popular email domains. These are filtered to match what the user has typed after the `@` symbol.
4. **Displaying Suggestions**: Matching providers are displayed in a dropdown below the input field. When a user clicks on a suggestion, it automatically fills the input field with the selected email.

### Example

To try the code, simply enter an email address up to the `@` symbol in the input field. You'll see suggestions for common email providers:

- **Type:** `user@`
- **Suggestions:** `user@gmail.com`, `user@yahoo.com`, `user@outlook.com`, etc.

### Customization

To add more email providers, simply add them to the `providers` array:

```javascript
const providers = ["@gmail.com", "@yahoo.com", "@outlook.com", "@hotmail.com", "@icloud.com", "@aol.com", "@protonmail.com", "@zoho.com", "@custom.com"];
```

### License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

---

This `README.md` file provides a clear description and documentation, making it ready to be published on GitHub.
