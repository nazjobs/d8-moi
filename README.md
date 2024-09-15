pretty much stolen from https://github.com/byquangthanh/valentine.github.io but wanted a "spin" to tit :) 

so u can deploy this static page on github and get the answers via google spreadsheet api lol

so i used google spreadsheet and put this script for the web app

`function doPost(e) { var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet(); var data = JSON.parse(e.postData.contents);

// This will prepare the row data WE NEED to store the DATA in var row = [new Date()]; row.push(data.noCount ||''); row.push(data.foods ? data.foods.join(", ") : ''); row.push(data.desserts ? data.desserts.join(", ") : ''); row.push(data.activities ? data.activities.join(", ") : ''); row.push(data.selectedDate || '');

// Append the data to the sheeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeet sheet.appendRow(row);

// This will set CORS headers... maybe, idk.

var output = ContentService.createTextOutput(JSON.stringify({ 'result': 'success' })); output.setMimeType(ContentService.MimeType.JSON); output.setHeader('Access-Control-Allow-Origin', '*'); output.setHeader('Access-Control-Allow-Methods', 'POST'); output.setHeader('Access-Control-Allow-Headers', 'Content-Type');`

um u can replace the google spreadsheet api url on the fetch function in ✨Decollector.js✨ file...

hab fun ! :)

ps: fuck cors...