This chapter outlines variaDoc's core concepts and how to use them.

# Merge project

One of the biggest features of variaDoc is the ability to easily merge projects with a few steps::

1. Add a database with all needed information to your project.
2. Add a document you want to work with. This can be an existing PDF, or a new document.
3. In the properties of the document, indicate how you want to export the final result.
4. Merge the needed data from the database with the corresponding fields in the document(s).
Now you can save the project and use it as often as needed.
**Running a merge project**
You can run a created merge project in one of the following ways:
- Interactively
Open the merge project in variaDoc and click on **Merge** in the toolbar. variaDoc will merge the project, create the resulting documents and list them in the log at the bottom of variaDoc. Double click on documents to open them.
- As a web service
To run a merge as an Microsoft IIS web service, copy the merge project and all related resources (PDF files, data sources, images etc) to your website and publish an URL that points to that project file.
See the Webservice chapter for more information.
- From your own .NET application
Use the variaDoc's Reports assembly.
See the .NET assembly chapter for more information.
- Unattended (batch)
Pass the path of the merge project as an argument to the command line application to run it unattended.
See the Command line application chapter for more information.
**Project script**
For larger projects, the number of nodes that specify what needs to be done may become too large to manage efficiently.
For easy management of these kinds of merge projects, specify your nodes using project script.
This is a single node with an XML-esque notation.
This sample describes a single Section node with a text paragraph in it.
<pm:section>
This is a simple piece of text.
And another line.
</pm:section>

# [Fields](#concepts-fields)

A great number of PDF forms contains fields where data can be filled in.
There are two sorts of fields: flattened and interactive. Flattened fields are a static representation of their content. They are no longer editable.
A field can be made interactive by clicking on the tab Settings and then choosing the option "Preserve interactive field". Interactive field have zero or more actions attached to them. For instance, the field value can be calculated or the field can be made read-only.
**Filling field values**
Fields are filled using an expression in the "field binding" section.
$picture$
The expression entered is evaluated during the merge and the result is placed in the field.
Different field types can require different ways to fill in data.
**Checkbox fields**
In checkbox fields you have to specify a condition. If the condition evaluates to true, the checkbox is checked, otherwise the checkbox is unchecked.
$picture$
**Combo box, list box and radio button fields**
In these types of option fields, the value of the field is specified in terms of an option.
$picture$
You can either specify a condition on each option (given a child nodes of the field) or specify the name of the option that should be selected.
If you choose to specify a condition on each option, you'll must enter an expression in the text box for each option node.
$picture$
If you choose to specify an expression that evaluates to the name of the selected option, you should enter this expression in here:
$picture$
**Adding new fields**
Besides fillings fields that are already in an existing PDF form, variaDoc also enables you to add new fields to a page in a merge project. Just like fields that already exist in the PDF form, these fields can be flattened or non-flattened. Adding fields to a page in a merge project will not change the existing PDF form in any way, only  the output document(s).
To add a field to a page, first select the field node in the toolbar, click on the appropriate field, then select the region on the page where the new field should be placed with the mouse.
Fields added in the merge project are displayed in light purple compared to light pink for existing fields.
For fields added in a merge project, you should specify the field value as you do for existing fields, and the appearance of the field(e.g. the border, font and font size).
**Overriding existing fields**
If you have an existing field in a PDF that you want to control the appearance of, but don't have control over the template PDF (e.g. because it is created by a third party) you can choose to override the appearance and behavior. When you override the appearance, use a Style to set the new appearance.
**Using fields in content sections**
Fields can also be used in a section containing dynamic content. In that case you need to specify the name and the size of the field. You specify this in the setting of the field node. You can find the settings next to the binding tab.
Field used in sections can only use styles for their appearance.
The name of the field is specified using the **Field name** property.
$picture$
This property is an expression, which means that the field name can be derived from data references. If this is left empty, the node name is used. Note that a field in PDF may only contain normal letters and certain special characters.
The size of the field must be specified by editing the **width** and **height** in the **Field size** settings.
$picture$
The width and height can be specified in various units. The width of the field can also be specified relative to the width of the containing element(e.g. a field in a table cell with a width of 50% results in a field that uses half the horizontal space of the cell its contained in).

# Typical project structures

variaDoc allows you to specify the export method, as well as the number and structure of generated documents.
**Single document, single page**
If you want to create a single document containing a single page you should first add an output document and then a new page. This page can be either an empty page or an existing PDF document. Once you added this, your project should look like this:
$picture$
This can be useful for automated form filling.
Single document, multiple pages
To generate a single document for every item in your data source, add a new document, then add the database with the needed data underneath. Finally, add the page you want to work with, using an existing PDF or a new document.
If you followed the described steps, your project should look like this:
$picture$

The output document is higher up in the tree than the data source. Consequently the data source will repeat the page for each row. All the generated pages are gathered by the output document and combined into a single PDF document.
This project structure can be used to prepare a mailing letter that will be printed.
**Multiple documents, each with a single page**
To generate a single document for every item in your data source, start by adding a database, then a new document and under this document, a new page(using either an existing PDF or a new page). Your project should look like this:
$picture$	

In this project the data source is higher up in the tree than the output document. Now the output document is repeated, similarly to the template page in the previous sample. The effect is that a document is generated for each row in the data source.
This project structure is most suited for sending personalized documents via e-mail to as many addresses as you like.
**Multiple documents, multiple pages**
variaDoc allows the nesting of data sources to generate almost any conceivable document structure.
The following structure generates multiple documents. Each document has multiple pages.
$picture$
This project structure can be used to generate multiple reports.
**Multiple template pages**
You can add multiple template pages to your project by first adding a new database, then a new document, and finally the pages you want to work with(as demonstrated in the figure below).
$picture$
This project will generate multiple documents, each with two pages.

# Using expressions

variaDoc features a powerful language that uses expressions. Expressions can be used to assign values to a wide variety of properties such as output file names, form field values, e-mail message subjects and SQL statements.
**Expressions**
Almost all settings in a merge project can be entered as an expression.
An expression can be literal text, but it may also contain data references or VB.NET expressions.
Literal text can be used only in certain contexts. For instance, if you added a section node to your document, then literal text can be converted into text paragraphs.
A data reference is a dynamic part of an expression. It is typically used to fill the value from a database in a field. During a merge it will be replaced by the value that it refers to at that time.
For example, if we have a list of customers in our database, we could refer to the company name of the customer like this:
$[Customers:CompanyName]
In this expression Customers is the name of a data source that connects to the database of the list of customers. CompanyName is the name of a column in the table that holds the list of customers.
The data reference will result in a different value for each row in the data source.
VB.NET expressions can perform tasks such as calculations and formatting. Here you can think of adding a calculated value or a date to your form.
Other examples of expressions are SQL queries and XPath expressions.
The use of expressions is not limited to form fields. They are used through out the project as well. For example, they can also be used to set file names and other document information.
The use of expressions gives unlimited possibilities for combining data into forms.
**Entering expressions**
Most text boxes in variaDoc allow you to enter expressions.
$picture$
Every entry box in variaDoc that lets you enter an expression has a preview button, . Clicking this button will evaluate the expression and show the results. If the expression is located in the merge project below one or more data sources, all possible instances of the evaluated expression are shown. This allows you to test expressions without having to run the entire project.
**Anatomy of an expression**
As previously mentioned, an expression can contain three kinds of sub-expressions:
Literal text
Data references
Embedded VB.NET expressions.
To distinguish between these parts, some special characters are used.
|--------------|------------------------------------------------------------|-------------------------|
|**Characters**|**Description**                                             |**Example**              |
|--------------|------------------------------------------------------------|-------------------------|
| $[ ]         | A data reference.                                          |$[customers:first]       |
|              | See Data reference.                                        |                         |
| -------------|------------------------------------------------------------|-------------------------|
| :            | If inside a data reference, separates the data source name |$[customers:first]       |
|              | from the data query.                                       |                         |
|--------------|------------------------------------------------------------|-------------------------|
| |            | If inside a data reference, separates the query from the   |$[customers:first|Upper] |
|              | inline format specifier.                                   |                         |
|--------------|------------------------------------------------------------|-------------------------|
| { }          | A VB.NET expression.                                       |{ DateTime.Now }         |
|--------------|------------------------------------------------------------|-------------------------|
Every character that is not part of a data reference or an embedded expression is literal text.
You can combine all kinds of sub-expressions in a single expression.
For example:
$picture$
This is piece of literal text combined with data $[Users:Name] from the Users data source and a VB.NET for the current date { DateTime.Now }.
**What happens during a merge**
Expressions are evaluated during a merge. Evaluation of an expression always results in a single value for either a setting or a form field. If an expression is specified on a page that is repeated many times, the expression is evaluated just as many times.
Evaluation of an expression happens in two steps.
Data references are replaced with actual data. If inline formatting is used, the formatted data is used instead of the actual data.
Any embedded VB.NET expressions are evaluated and replaced with their result.
The resulting value is used by variaDoc to fill form fields or set properties.
**Syntax coloring**
While typing expressions, syntax coloring will help you identify how the different parts of the expression are interpreted by variaDoc. The following shows the color scheme.
|---------------------|------------------------------------------------------------------|
|**Color sample**     |**Description**                                                   |
|---------------------|------------------------------------------------------------------|
|“static text”        |Static text in SQL expressions ( red )                            |
|---------------------|------------------------------------------------------------------|
|SELECT               |SQL keyword ( blue ), VB keyword                                  |
|---------------------|------------------------------------------------------------------|
|{ String.Format() }  |Embedded VB.NET expression ( accolades marked yellow )            |
|---------------------|------------------------------------------------------------------|
|$[mydata:field]      |Data reference ( dark red / dark yellow with light yellow back )  |
|---------------------|------------------------------------------------------------------|


**Type assist**
variaDoc provides type assist. For example if you type in the $ character, variaDoc knows you are trying to reference a data source or merge parameter and will display a list of available options. This will help you to type expressions quickly and reduce the number of typing errors. See figure below.
$picture$
If you select a data source from the suggested list and type the : (colon) character, variaDoc knows you are trying to select a field from the selected data source and will display a list of available options.
variaDoc provides type assist for:
1. Data sources
2. Database fields
3. Merge Parameters
4. XML/XPath entities
**Preview expressions**
Every entry box in variaDoc that lets you enter an expression has a preview button,$picture$. Clicking this button will evaluate the expression and show the results. If the expression is located in the merge project below one or more data sources, all possible instances of the evaluated expression are shown. This allows you to test expressions without having to run the entire project.
               
## Data preferences

See [fields](concepts-fields)

               
               
               
