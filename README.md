```markdown
# Custom HAVEDINNERWITHMEPLSPLSPLSPLS' Day Form - Google Spreadsheet Integration

This project is inspired by [valentine.github.io](https://github.com/byquangthanh/valentine.github.io) but with a unique twist! It allows you to deploy a static webpage on GitHub, where you can send form responses to Google Spreadsheets using Google Spreadsheet API. Sounds fun? Let's dive in!

## Project Overview

We use Google Spreadsheet as the backend to store user responses. The frontend form is a static page that can be deployed on GitHub Pages. The responses are collected via a Google Apps Script that acts as an API, handling POST requests from the web page.

### Tech Stack:
- **Static Webpage**: Hosted on GitHub Pages
- **Google Apps Script**: To handle form submissions
- **Google Spreadsheet API**: To store form data

## Getting Started

### 1. Google Spreadsheet Setup

1. Create a new Google Spreadsheet.
2. Go to **Extensions > Apps Script**.
3. Replace the content of the script editor with the following code:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);

  // Prepare row data to store in the spreadsheet
  var row = [new Date()];
  row.push(data.noCount || '');
  row.push(data.foods ? data.foods.join(", ") : '');
  row.push(data.desserts ? data.desserts.join(", ") : '');
  row.push(data.activities ? data.activities.join(", ") : '');
  row.push(data.selectedDate || '');

  // Append data to the spreadsheet
  sheet.appendRow(row);

  // Set CORS headers
  var output = ContentService.createTextOutput(JSON.stringify({ 'result': 'success' }));
  output.setMimeType(ContentService.MimeType.JSON);
  output.setHeader('Access-Control-Allow-Origin', '*');
  output.setHeader('Access-Control-Allow-Methods', 'POST');
  output.setHeader('Access-Control-Allow-Headers', 'Content-Type');

  return output;
}
```

4. Save and deploy the script as a **web app**. You will need to set permissions so that "Anyone" can send requests.

### 2. Frontend Code Changes

In your `✨Decollector.js✨` file, replace the Google Spreadsheet API URL in the `fetch` function with the URL of your deployed Google Apps Script web app.

```javascript
fetch('YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify(formData),
})
```

Make sure the form data (e.g., `formData`) you're sending matches the structure expected in the Google Apps Script.

### 3. Deploy the Static Page on GitHub

1. Clone your repository or use an existing static page setup.
2. Push your project to GitHub.
3. Enable GitHub Pages in your repository settings to host your webpage.

### CORS Issues

Yes.

## Have Fun!


P.S. Fuck CORS!
```
