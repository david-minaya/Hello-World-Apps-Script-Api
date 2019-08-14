# Google Apps Script example

This is a simple example of how run the Apps Script Api of Google.

This [guide](./Guide Google Apps Script Api (Form).md) to explain how write this project.

To access to the Apps Script project that run this project is need a google account. But this is the code that containt the Google Apps Script project.

```javascript
function HelloWorld() {
  
  // This is the url of the form that read this code
  const formUrl = 'https://docs.google.com/forms/d/1DjAM95DBwd4djPQgaRM1DsaZU90o5izr66Vw6MWnZiQ/edit'
  
  // Open the form and get its title
  const form = FormApp.openByUrl(formUrl)
  const title = form.getTitle()
  console.log(title);
  
  // Return the data of the fifth option of the seconds response of the form
  return form.getResponses()[1].getItemResponses()[4].getResponse();
}

```

If you are login with a Intellisys account you can access to the form url.

In the console this program must print some like this:

```
Run the script
>>>>>>>
{ done: true,
  response:
   { '@type':
      'type.googleapis.com/google.apps.script.v1.ExecutionResponse',
     result: 'Persna 2' } }
<<<<<<<<<
```

