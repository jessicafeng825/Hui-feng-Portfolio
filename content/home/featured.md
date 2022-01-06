---
# An instance of the Featured widget.
# Documentation: https://wowchemy.com/docs/page-builder/
widget: featured

# This file represents a page section.
headless: true

# Order that this section appears on the page.
weight: 63

title: Demo Reel
subtitle: "Featured Post"

content:
  # Page type to display. E.g. post, talk, publication...
  page_type: project
  # Choose how many pages you would like to display (0 = all pages)
  count: 0
  
  # Filter on criteria
  filters:
    author: ""
    category: ""
    publication_type: ""
    tag: ""
  filter_button:
  - name: All
    tag: '*'
  - name: Computer Graphics
    tag: Computer Graphics
  - name: Unity Shader
    tag: Unity shader
  - name: Game Development
    tag: Game Development 
  - name: Tools
    tag: Tools
  - name: Unreal
    tag: Unreal
  - name: Lighting
    tag: Lighting
    
  # Page order: descending (desc) or ascending (asc) date.
  order: desc

design:
  columns: '2'
  # Choose a view for the listings:
  #   1 = List
  #   2 = Compact
  #   3 = Card
  #   4 = Citation (publication only)
  view: Card
  flip_alt_rows: false
---
