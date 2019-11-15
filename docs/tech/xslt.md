# XSLT

## References

- [XSL Introduction (W3 Schools)](https://www.w3schools.com/xml/xsl_intro.asp)
- [XSLT Foundations, Part 1 (Pluralsight)](https://app.pluralsight.com/library/courses/xslt-foundations-part1/table-of-contents)

## Dictionary
XML - eXtensible Markup Language, for structuring documents

XSL - eXtensible Stylesheet Language, for styling XML

XSLT - XSL Transformations, programmatically transform an XML document

XSL-FO - language for formatting XML documents (discontinued, CSS3 proposed as replacement)

XPath - language for navigating XML documents

XQuery - language for querying XML documents

## What is it?
Transforms XML document into another XML document using XPath to navigate and parse the source XML

## Syntax

**Setup/Templates**

xsl:stylesheet - defines that this is a stylesheet
xsl:template match="/" - defines what path(s) of the XML document to run the template on

xsl:apply-templates - placeholder to insert later templates into, note that scope changes to template

**Value injection & looping**

xsl:value-of select="path" - gets values from an XML document
xsl:for-each select="path" - loops through each node

xsl:if test="expression" - only do the nested when true
xsl:choose, xsl:when, xsl:otherwise - if/else equivalent

**Filtering**

select="path[attribute='value']"

**Sorting**

xsl:sort select="attribute" - sort on the given attribute

**Different ways to implement**

  1. Including XSL stylesheet as a reference in the XML document
  2. Client-side - use JavaScript to load the 2 resources and transform in-browser (for browsers with an XML parser)
  3. Server-side - do the transform on the server to XHTML (e.g. PHP, ASP, pre-rendered)
