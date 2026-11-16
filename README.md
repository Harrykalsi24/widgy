Widgy Quotes Widget

A lightweight, dynamic quote widget for iOS powered by Widgy, JavaScript, and GitHub.

The project uses a public GitHub repository as a remote data source to store and manage quotes. Widgy retrieves the JSON data through its API Connector, while JavaScript processes the response and selects a random quote to display directly on the home screen.

✨ Features

* GitHub-powered data: Stores all quotes in a public JSON file.
* Dynamic content: Fetches quotes remotely instead of hardcoding them into the widget.
* Random quote selection: JavaScript selects a random quote from the available collection.
* Easy updates: Add, edit, or remove quotes directly from GitHub.
* Lightweight architecture: No dedicated backend, database, or hosting server required.
* Centralized management: All quote content is maintained in one place.

🛠️ Technologies Used

* Widgy – iOS home screen widget customization.
* JavaScript – Fetching, parsing, filtering, and selecting quote data.
* JSON – Structured storage for quote collections.
* GitHub – Public repository and remote data hosting.

📁 Project Structure

widgy/
│
├── widgy_quotes.json
└── README.md

Data Source

The widget retrieves its data from:

https://raw.githubusercontent.com/Harrykalsi24/widgy/main/widgy_quotes.json

📄 JSON Data Structure

All quotes are stored in widgy_quotes.json.

Example:

{
  "title": "Widgy Quotes",
  "collection_author": "Harry",
  "version": 1,
  "quotes": [
    {
      "id": 1,
      "text": "Great things are done by a series of small things brought together.",
      "author": "Vincent van Gogh"
    },
    {
      "id": 2,
      "text": "Simplicity is the ultimate sophistication.",
      "author": "Leonardo da Vinci"
    }
  ]
}

Each quote contains:

Field	Description
id	Unique quote identifier
text	Quote content
author	Quote author

The collection also includes metadata such as its title, author, and version.

⚙️ How It Works

The project follows a simple data-fetching workflow:

1. Data storage: Quotes are maintained in a JSON file inside the GitHub repository.
2. Remote access: Widgy’s API Connector sends a GET request to GitHub’s raw content URL.
3. Data processing: JavaScript receives and parses the JSON response.
4. Filtering: Empty or invalid quote entries are excluded.
5. Random selection: A random quote is selected from the remaining collection.
6. Widget display: The selected quote is displayed in the Widgy widget.

JavaScript Logic

The core selection logic follows this approach:

var xhr = new XMLHttpRequest();
xhr.open(
  "GET",
  "https://raw.githubusercontent.com/Harrykalsi24/widgy/main/widgy_quotes.json",
  false
);
xhr.send();
if (xhr.status === 200) {
  var data = JSON.parse(xhr.responseText);
  var validQuotes = data.quotes.filter(function(q) {
    return q.text && q.text.trim() !== "";
  });
  if (validQuotes.length > 0) {
    var randomIndex = Math.floor(
      Math.random() * validQuotes.length
    );
    return validQuotes[randomIndex].text;
  }
}
return "Unable to load quotes.";

This demonstrates the core processing logic; the actual Widgy script should follow the variable and output requirements of its configured API Connector.

🔄 Updating the Quotes

One of the main advantages of this approach is that the quote collection can be updated without rebuilding the widget.

To add or modify quotes:

1. Open the GitHub repository.
2. Navigate to widgy_quotes.json.
3. Add, edit, or remove entries.
4. Commit and push the changes.
5. Allow Widgy to retrieve the updated JSON data on its next refresh.

Note: Widget refreshes are managed by iOS. Updates are not guaranteed to appear immediately.

🔐 Privacy & Hosting

* The repository contains publicly accessible quote data.
* No private API keys or authentication credentials are required for the public JSON endpoint.
* No personal user information is collected by this data source.
* GitHub provides the hosting through its raw content service.

🎯 Project Goal

The goal is to demonstrate how a simple, serverless content-delivery approach can power a dynamic iOS widget.

By combining GitHub’s raw content hosting, structured JSON, JavaScript processing, and Widgy’s API Connector, the project provides a simple way to manage and deliver changing widget content without maintaining a dedicated backend.

⸻

Built with GitHub, JavaScript & Widgy.