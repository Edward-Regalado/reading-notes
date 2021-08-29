## Django Working with Forms

- An HTML Form is a group of one or more field/widgets on a web page, which can be used to collect information from users for submissions to a server.
- they include different types of data, text boxes, checkboxes, radio buttons, dates and so on.
- allow us to send data in POST requests with cross-site request forgery protection.

## HTML Forms

- form is defined in HTML as a collection of elements inside <form>...</form> tags, containing at least one input element of type='submit'.
- The `name` and `id` of the field are used to identify the field in JS/CSS/HTML, while `value` defines teh initial value for the field when it is first displayed.
- action: the resource/URL where data is to be sent for processing when the form is submitted. If not set (or set to empty string), then the form will be submitted back to the current page URL.
- method: the HTTP method used to send the data- post or get.
    - The `POST` method should always be used if the data is going to result in a change to the server's database.
    - The `GET` method should only be used for forms that don't change user data (e.g. a search form).
- once the server gets a request with all valid form data, it can perform an appropiate action (saving, returning,uploading a file, etc).

## Declaring a Form

- declartion syntax for a Form is similar to that for declaring a Model and shares the same field types.
- Form data is stored in an application's forms.py file, inside the app's directory.
- `from django import forms`
`class RenewBookForm(forms.Form):`
    `renewal_date = forms.DateField(help_text="Enter a date between now and 4 weeks (default 3).")`

## Form Fields

- required: If True, the field may not be left blank or given a None value.
- label: used when rendering the field in HTML. If a label is not specified, Django wil create one from the field name by capitalizing the first letter and replacing underscores with spaces.
- lable_suffix: by default, a colon is displayed after the label.
- initial: intitial value for the field when the form is displayed.
- widget: the display widget to use.
- help_text: additional text that can be displayed in form to explain how to use the field.
- error_message: list of error messages for the field.
- validators: list of functions that will be called on the field when it's validated.
- localize: enables the localization of form data input.
- disabled: the field is displayed but its value cannot be edited if this is True.

