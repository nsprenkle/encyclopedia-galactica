# XPath

## Resources
- [XPath Introduction (W3 Schools)](https://www.w3schools.com/xml/xpath_intro.asp)

## Notes
XML documents are treated as trees of nodes, with the topmost called the root

Nodes - items in the XML hierarchy
  - element - tag
  - attribute - attribute on a tag
  - text - text within a tag
  - namespace
  - processing-instruction
  - comment - comment node
  - document node

Atomic values - nodes without children or parents, e.g. text

Items - generic term for nodes or atomic values

Ancestry
  - Parent, node immediately containing an element, nodes (except atomic values) have exactly one parent
  - Children, items which a node contains
  - Siblings, items also housed within the same node
  - Ancestors, the lineage of parent elements to a specific item
  - Descendants, opposite of ancestors

Selectors - elements are selected by using a string specifying location or properties of nodes to match, spearated by vertical pipes

Expression | Description
---------- | ---
nodename   | select node by name
/          | select from root
//         | select from any 
.          |select current node
..         | select parent of current node
@          | select attributes

Predicates - modifiers on a search selector

Expression | Description
---------- | ---
[n] | Select the nth element which matches (1 indexed!)
[last()] | Selects the last element which matches
[position()><n] | Selects elements which are >/< nth in the match
[@attr='val'] | Selects nodes with attributes having certain values
[val >/< val] | Can select nodes with a value in a certain range

Wildcards

Expression | Description
--- | ---
* | Match any element node
@* | Match any attribute
node() | Select any node

Axes, define node relations to current node (e.g. ancestor, child, following, namespace, self, etc.)

Can also do math & Boolean logic
