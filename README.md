# Spreadsheet CMS Demo

This project is a demo & test of using **Google Spreadsheets** as a tiny CMS, fetching data from the API generated using [App Script](https://www.google.com/script/start/).

**JSON file:** [Google Spreadsheet API](https://script.googleusercontent.com/macros/echo?user_content_key=hoxKlP7BD88BZCs7Nws2CLJMDQXSY-dCK0hjtY0ot6jsBN1H5BoCT6Yrj9rVLLf3_tbRNqQN6IT4oWeC_eUKjhJExhDvcRWZm5_BxDlH2jW0nuo2oDemN9CCS2h10ox_1xSncGQajx_ryfhECjZEnLKQD0xlRdQNORBeubHhskJtf2UCBubGj2B2xfutiOdgkRnT3lsoHqFVKfrWto-uf_VFUtiN9nc_zwS1fN0fcKGlHOSTBWM63dz9Jw9Md8uu&lib=McmiJzxE192vUTCqyMMT_iInk_TX2PQ6s)

**Code of the function additionally turning it into a JSON**

```js
function doGet() {
  const doc = SpreadsheetApp.getActiveSpreadsheet();
  const sheet = doc.getSheetByName("Earnings");
  const values = sheet.getRange(1, 1, 8, 5).getDisplayValues();

  const result = [];
  for (let i = 0; i < values[0].length; i++) {
    result.push({
      week: values[0][i],
      days: [
        { day: "Monday", earnings: values[1][i] },
        { day: "Tuesday", earnings: values[2][i] },
        { day: "Wednesday", earnings: values[3][i] },
        { day: "Thursday", earnings: values[4][i] },
        { day: "Friday", earnings: values[5][i] },
        { day: "Saturday", earnings: values[6][i] },
        { day: "Sunday", earnings: values[7][i] }
      ]
    });
  }
  
  return ContentService.createTextOutput(JSON.stringify({data: result})).setMimeType(ContentService.MimeType.JSON);
}
```
