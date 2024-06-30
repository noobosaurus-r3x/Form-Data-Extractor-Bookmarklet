

## Overview

The Form Data Extractor Bookmarklet extracts and displays form data from any web page, including actions, methods, and input details.
Still a WIP but working on a lot of websites.

## How to Use

### Creating the Bookmarklet

1. Copy the JavaScript code below.
2. Create a new bookmark in your browser.
3. Paste the JavaScript code into the URL/location field of the bookmark.

```javascript
javascript:(function(){
    var forms = document.getElementsByTagName('form');
    var newWindow = window.open('', '', 'width=800,height=600');
    newWindow.document.write('<html><head><title>Form Data</title>');
    newWindow.document.write('<style>body { font-family: Arial, sans-serif; }');
    newWindow.document.write('table { width: 100%; border-collapse: collapse; margin-bottom: 20px; }');
    newWindow.document.write('th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }');
    newWindow.document.write('th { background-color: #f2f2f2; }');
    newWindow.document.write('tr:nth-child(even) { background-color: #f9f9f9; }');
    newWindow.document.write('h2 { background-color: #4CAF50; color: white; padding: 10px; }');
    newWindow.document.write('</style></head><body>');
    
    for (var i = 0; i < forms.length; i++) {
        var form = forms[i];
        newWindow.document.write('<h2>Form ' + (i + 1) + ':</h2>');
        newWindow.document.write('<table>');
        newWindow.document.write('<tr><th>Name</th><th>Type</th><th>Value</th></tr>');
        newWindow.document.write('<tr><td>Action:</td><td colspan="2">' + (form.action || 'N/A') + '</td></tr>');
        newWindow.document.write('<tr><td>Method:</td><td colspan="2">' + (form.method || 'get') + '</td></tr>');
        
        var elements = form.elements;
        for (var j = 0; j < elements.length; j++) {
            var element = elements[j];
            var value = element.value || 'N/A';
            if (element.type === 'checkbox' || element.type === 'radio') {
                value = element.checked ? 'on' : 'off';
            }
            newWindow.document.write('<tr><td>' + (element.name || 'N/A') + '</td><td>' + (element.type || 'N/A') + '</td><td>' + value + '</td></tr>');
        }
        
        newWindow.document.write('</table>');
    }
    
    newWindow.document.write('</body></html>');
    newWindow.document.close();
})();
```

### Using the Bookmarklet

1. Go to the web page you want to analyze.
2. Click the bookmarklet.
3. A new window will display a table with form details.

## Limitations

- The bookmarklet does not work on all websites due to Content Security Policy (CSP) restrictions.
- Limited to displaying basic form data; may not handle complex input types or dynamically generated forms.


---

Feel free to modify as needed!
