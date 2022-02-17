## Django: Using Models

- Django web applications access and manage data through Python objects refferred to as models.
- Models define the structure of stored data, including the field types and possibly also their maximum size, default values, selection list options, help text for documentation, label text for forms, etc.

## Designing the LocalLibrary models

- when designing your models it makes sense to have separate models for every "object" (a group of related information).
- use models to represent selection-list options (e.g. like a drop down list of choices), rather than hard coding the choices inot the website itself.
- use models to represent selection-list options(drop down list of choices), rather than hard coding the choices into the website itself.
- Django allows you to define relationships that are one to one (OneToOneField), one to many (ForeignKey) and many to many (ManytoManyField).


## Model primer

### Model definition

- Models are usually defined in an application's models.py file. They are implemented as subclasses of django.db.models.Model, and can include field, methods and metadata.

### Typical model

from django.db import models

class MyModelName(models.Model):
    """A typical class defining a model, derived from the Model class."""

    # Fields
    my_field_name = models.CharField(max_length=20, help_text='Enter field documentation')
    ...

    # Metadata
    class Meta:
        ordering = ['-my_field_name']

    # Methods
    def get_absolute_url(self):
        """Returns the url to access a particular instance of MyModelName."""
        return reverse('model-detail-view', args=[str(self.id)])

    def __str__(self):
        """String for representing the MyModelName object (in Admin site etc.)."""
        return self.my_field_name

### Fields

- A model can have an arbitrary number of fields, of any type - each one represents a column of data that we want to store in one of our database tables.
- Each databe record (row) will consist of one of each field value.
- my_field_name = models.CharField(max_length=20, help_text='Enter field documentation')
- Charfield means the field will contain strings and alphanumeric characters.

### Common Field Arguments

- help_text: provides a text label for HTML forms (like the admin stie).
- verbose_name: human-readable name for the field used in field labels.
- default: the default value for the field. This can be a value or a callable object.
- null: if True, Django will store blank values as NULL in the database for fields where this is appropiate. 
- blank: if True, the field is allowed to be blank in your forms. The default is False, which means the django's form validation will force you to enter a value.
- choices: a group of choices for this field.
- primary_key: if True, sets the current firled as the primary key for the model. A primary key is a speical database column designated to uniquely identify all the diff table records.

### Common Field types

- CharField: used to define short-to-mid sized fixed-length strings. You must specify the max_length of the data to be stored.
- TextField: used for large arbitrary-length strings. You may specify a max_length for the field, but this is used only when the field is displayed in forms.
- IntergerField: for storing interger (whole number) values, and for validating entered values as ints in forms.
- DateField and DateTimeField: used for storing/rep dates and date/time info. Thsi fields can additionally declare the parameters auto_now = True (to set the field to the current date every time the model is saved).
- EmailField: used to store and validate email addy.
- FileField: used to upload files and images. These have params to define how and where the uploaded files are stored.
- AutoField: special type of int field that automatically increments. A primary key of this type is auto added to your model if you don't specify one.
- ForeignKey: sued to specify a one-to-many relationship to antoher database model (a car has one manufactuer, but a manufactuer can make many cars.)
- ManytoManyField: used to specify a many-to-many relationship (a book can have serveral genres, and each genre can contain several books.)

### Metadata

- control the default ordering of records returned when you query the model type.
- The ordering will depend on the type of field (characters fields are sorted alphabetically, while date fields are sorted in chronological order).
- class Meta:
    ordering = ['-my_field_name']
- ordering = ['title', '-pubdate']

### Methods

- At a minimum, you should define the standard Pytyon class method __str__() to return a human-readable string for each object.
- def __str__(self):
    return self.field_name
- get_absolute_url() reutnrs a URL for displaying individual model records on the website.
- def get_absolute_url(self):
    return reverse('model-detail-view', args=[str(self.id)])