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

**Characters** | **Description** | **Example**
--- | :---: | ---:
$[ ] | A data reference. See Data reference. | $[customers:first]
: | If inside a data reference, separates the data source name from the data query. | $[customers:first]
| | If inside a data reference, separates the query from the inline format specifier. | $[customers:first|Upper]
{ } | A VB.NET expression. | { DateTime.Now }

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

**Color sample** | **Description**
--- | :---:
“static text” | Static text in SQL expressions ( red )
SELECT | SQL keyword ( blue ), VB keyword
{ String.Format() } | Embedded VB.NET expression ( accolades marked yellow )
$[mydata:field] | Data reference ( dark red / dark yellow with light yellow back )


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

A data reference is a reference to data in a data source. Once you run a merge, it will be replaced with the current data from the data source.
In its simplest form, it consists of 2 parts:
1. The data source name
2. A query
These parts are separated by a : (colon).
Example 1:
$[customers:name]
This data reference refers to the column **name** in a data source named **customers**. In this case, the query part is a column name.
This only works for non-XML data sources. For XML based data sources, the query part is an XPath expression.
Example 2:
$[authors:name/@name]
This data reference will return the **name** attribute of the **name** element in the current node set of a (XML) data source named **authors**.
$picture$ Data references that cannot be resolved result in an error.
**Using a sub-string**
If you want to use only a small part of the value resulting from a data reference, you can use the inline sub-string operator.
The sub-string operator directly follows the query. It consists of two number surrounded by '(' and ')' and separated by a comma ','. The first number indicates the start index in the value. The second number indicates the length of the sub-string. The start index starts at zero (0).
Example 3:
$[customer:name(2,1)]
This examples  takes a sub-string of the name column. The sub-string is 1 character long and starts at the third character of the name (index 2).
If the name was originally "Theo", this example will return "e".
If the length of the sub-string is greater that what is available, an empty string is returned.
**Data formatting**
Data references can be formatted according to an inline format specifier.
The inline format specifier is separated from the query by a | (vertical bar).
Example 4:
$[customers:name|Upper]
This data refers to the column **name** in a data source called **customers**. The resulting data is converted to upper case.
**Data type conversion**
The type of the current data to which a data reference evaluates depends on the data source. Typically a number column results in number values, but in some cases there is a need to convert from one data type to another. A typical example is an XML data source. All values from an XML data source will be of the type string. If you have a number in your XML data that you want to calculate with, it is necessary to convert that data to a number first.
Data references can be converted to a specific type using an inline data conversion.
The inline conversion surrounds the data source name and the query like this:
$[CInt(data source name:query)]
Where **CInt** is one of the possible conversions. In this case the data is converted to a 32-bit signed integer.
It is also possible to combine inline conversion and inline formatting in one data reference like this:
$[CDbl(order:price)|#.##0]
In this example the value of the **price** column from the **order** data source is first converted to a 64-bit floating point number and then formatted using the **#.##0** format specifier.

### Inline format specifiers

Data from a data source can be formatted using an inline format specifier.
Format specifiers can be standard or custom. With custom format specifiers you can e.g. specify your own currency or date format.
**Standard string format specifiers**

**Specifier** | **Description** | **Example**
--- | :---: | ---:
Upper | Convert to upper case | $[Addresses:City|Upper]
Lower | Convert to lower case | $[Addresses:City|Lower]
EscaleSQL | Escape all SQL special characters, for use in SQL expressions. | SELECT * FROM Table WHERE Field='$[Data:Value|EscapeSQL]'
EscapeXHTML | Escale all XHTML special characters, for use in XHTML content. | <b>$[Users:Name|EscapeXHTML]</b>
Trim | Remove all leading and trailing whitespace. | $[FIELD:Name|Trim]
TrimStart | Remove all leading whitespace. | $[FIELD:Name|TrimStart]
TrimEnd | Remove all trailing whitespace. | $[FIELD:Name|TrimEnd]
Newline | Append a newline separator if the value is not empty. | { $[Users:Addres1|Newline] + $[Users:Address2|Newline] }

**Standard number format specifiers**

**Specifier** | **Description** | **Example (all values are 1805,4573)**
--- | :---: | ---:
C | Standard currency format | $[data:value|C] ð $1,805.45
N | Standard number format | $[data:value|N] ð 1,805.46
F | Standard fixed point format | $[data:value|F] ð 1805.46
P | Standard percentage format | [data:value|P] ð 180545.73%
To set the number of digits after the decimal separator, post fix the letter with a number.
For example **F3** will format a fixed point number with 3 decimals.
**Standard date and time format specifiers**

**Specifier** | **Description** | **Example (all values are August 24, 2004 2:12:36 PM)**
--- | :---: | ---:
D | Standard full date | $[data:value|D] ð Tuesday, August 24, 2004
d | Standard short date | $[data:value|d] ð 8/24/2004
T | Standard full time | $[data:value|T] ð 2:12:36 PM
t | Standard short time | $[data:value|t] ð 2.12 PM
m | Month and day | $[data:value|m] ð August 24

**Custom number format specifiers**

**Specifier** | **Description** | **Example (all values are 42.000)**
0 | Zero placeholder. If the value being formatted has a digit in the position where the 0 appears in the format string, then that digit is copied to the result string, if not a zero is inserted. | $[data:value|0] ð 42000
**#** | Digit placeholder. If the value being formatted has a digit in the position where the # appears in the format string, then that digit is copied to the result string. Otherwise, nothing is stored in that position in the result string. Note that this specifier never displays the 0 character if it is not a significant digit, even if 0 is the only digit in the string. | $[data:value|#####0] ð 42000
. | Decimal point. The first . character in the format string determines the location of the decimal separator in the formatted value; any additional . characters are ignored. The actual character used as the decimal separator is determined by the computers regional settings. | $[data:value|0.00] ð 42000.00
, | Thousand separator and number scaling. If the format string contains a , character between two digit placeholders (0 or #) and to the left of the decimal point , then the output will have thousand separators inserted between each group of three digits to the left of the decimal separator. The actual character used as the decimal separator in the result string is determined by the computers regional settings. | $[data:value|#,##0] ð 42,000
% | Percentage placeholder. The presence of a % character in a format string causes a number to be multiplied by 100 before it is formatted. The appropriate symbol is inserted in the number itself at the location where the % appears in the format string. The percent character used is dependent on the computers regional settings. | $[data:value|0%] ð 4200000%
; | Section separator. ; is used to separate sections for positive, negative, and zero numbers in the format string.

**Custom date format specifiers**

**Specifier** | **Description** | **Range**
--- | :---: | ---:
d | Day of the month | 1 - 31
dd | Day of the month with leading zero | 01 - 31
ddd | Abbreviated name of the day of the week | mon, tue, wed ...
dddd | Full name of the day of the week | monday, tuesday ...
M | Numeric month | 1 - 12
MM | Numeric month with leading zero | 01 - 12
MMM | Abbreviated name of the month | Jan, Feb, Mar ...
MMMM | Full name of the month | January, february...
y | Year without century | 1 - 99
yy | Year without century with leading zero | 01 - 99
yyyy | Year with century | 1999, 2000, 2001 ...

**Custom time format specifiers**

**Specifier** | **Description** | **Range**
--- | :---: | ---:
h | Hour in a 12-hour clock | 0 - 12
hh | Hour in a 12-hour clock with leading zero | 00 - 12
H | Hour in a 24-hour clock | 0 - 23
HH | Hour in a 24-hour clock with leading zero | 00 - 23
m | Minutes | 0 - 59
mm | Minutes with leading zero | 00 - 59
S | Seconds | 0 - 59
ss | Seconds with leading zero | 00 - 59
tt | AM/PM designator | AM, PM
zz | Time zone offset (in hours) with leading zero | 00, +02, -06 ...
zzz | Full time zone offset (hours and minutes) with leading zeros | +02:00 , -06:00 ...

### Inline datatype conversion

Sometimes it is necessary to convert data to a specific type in order to avoid possible errors during operation. In such cases you can use the inline conversion functions below.
Data from XML data sources and merge parameters is always text (the type is string). This means that you may have to convert it into a number before you can use it in a calculation.

**Conversion function** | **Description** | **Default value** | **Example**
--- | :---: | ---: | ---:
CBool | Converts the data into a boolean (true / false) | false | $[CBool(Data source:Option1)]
CByte | Converts the data into a byte, an unsigned number from 0 to 255. | 0 | $[CByte(Data:SmallNumber)]
CChar | Converts the data into a character. | space | $[CChar(Data:Text)]
CDate | Converts the data into a date/time object. | Now | $[CDate(Data:StartDate)|MM dd yyyy]
CDbl | Converts the data into a double precision floating point value. | 0.0 | $[CDbl(products:price)] + 5.0
CDec | Converts the data to a decimal value. | Decimal values are fixed point numbers, useful for calculation monetary values. | 0 | $[products:price] * $[CDec(Margin)]
CInt | Converts the data into a 32-bit signed integer. | 0 | $[CInt(order:quantity)]
CLng | Converts the data into a 64-bit signed integer. | 0 | $[CLng(product:serial)]
CShort | Converts the data into a 16-bit signed integer. | 0 | $[CShort(order:quantity)]
CSng | Converts the data into a single precision floating point value. | 0.0 | $[CSng(order:price)]
CStr | Converts the data to a string | empty string | $[CStr(Data:Number)]

**Type checking functions**
The following conversion function checks if data can be converted to a certain type.
All functions return **true** or **false.**

**Conversion function** | **Description** | **Default value** | **Example**
--- | :---: | ---: | ---:
IsBool | Can the data be converted into a boolean. | n/a | $[IsBool(Data source:Option1)]
IsByte | Can the data be converted into a byte. | n/a | $[IsByte(Data:SmallNumber)]
IsChar | Can the data be converted into a character. | n/a | $[IsChar(Data:Text)]
IsDate | Can the data be converted into a date/time object. | n/a | $[IsDate(Data:StartDate)]
IsDbl | Can the data be converted into a double precision floating point value. | n/a | $[IsDbl(products:price)]
IsCDec | Can the data be converted to a decimal value. | n/a | $[IsDec(Margin)]
IsInt | Can the data be converted into a 32-bit signed integer. | n/a | $[IsInt(order:quantity)]
IsLng | Can the data be converted into a 64-bit signed integer. | n/a | $[IsLng(product:serial)]
IsShort | Can the data be converted into a 16-bit signed integer. | n/a | $[IsShort(order:quantity)]
IsSng | Can the data be converted into a single precision floating point value. | n/a | $[IsSng(order:price)]
IsStr | Can the data be converted to a string. | n/a | $[IsStr(Data:Number)]

**Conversion error & default values**
If a conversion fails because the data cannot be converted, a default value is used.
You can manually specify this value or use the built-in default ones.
To specify your own default value, write it after the query in the following format:
$[CInt(Charges:Allowance, 22)]
If the **Allowance** data cannot be converted to an integer, the value **22** is used.
               
               
               
