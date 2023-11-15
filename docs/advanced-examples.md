# Advanced usage examples

In this section of the docs you will find some advanced usage examples of modal-form-plugin

## Nesting form calls

## Modifying frontmatter with a form
Modal Forms can be used to modify existing frontmatter by way of the following snippet: 

```
<%*
const modalForm = app.plugins.plugins.modalforms.api; 
const result = await modalForm.openForm('solution feasibility');
app.fileManager.processFrontMatter(tp.config.target_file, frontmatter => { Object.assign( frontmatter, result.getData() ); }) }, 200) 
-%>
```

This method offers a way of editing/adding multiple frontmatter values to an existing note. For example


## Using Links with modal Forms
Dataview queries can be formatted to return links. The following snippet will suggest Wiki style links `[['Link Name'|'Link Alias']]`:
```
dv.pages('#tag').map(p => "[[" + p.file.name +  "|" + p.file.alias + "]]")
```
