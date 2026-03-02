# JIGSON - A schema based JSON editor.
## Description
A json editor that is written purely in Rust with egui/eframe framework for UI. 
Compiles for native(Linux) and WebAssembly. Windows is not tested yet.

## Demo
[Link to Github pages](https://martinbjerkaas.github.io/jigson-live/)

## Workflow
 - Import data
 - Map data to schema
 - Transform data (not implemented yet)
 - Edit the data in table editor.
 - Export the data
 
## Features
**Importing data**
  - Supports json, csv and .knxproj as drag&drop file input. Data type is automatically detected by pattern matching the first bytes of the file.
  - Supports copy/pasting in raw json, csv data.
  - Validates if can be parsed to a valid json.
  
**Mapping the data**
  - Source json properties can be mapped to schema properties. Easy convert from one json structure to another.
  - Automap all properties that are exactly matching the schema properties.
  
**Editing the data**
  - Create a schema based on the loaded json properties using the builtin SchemaBuilder or import schema file.
  - Live validation of all cells against json schema.
  - Create or remove rows and columns.
  - Autofill certain columns with incremental value.
  - Advanced filtering of rows
  - Bulk edit. Edit all columns to a specific value for selected rows.
  - Templating. Apply changes to all objects that match a certain criteria. Can edit many feilds.

**Exporting the data**
  - Export as json or csv.
  - Validate on export.

## Quick and dirty TODO/notes until more complete release:

### New features/larger refactors:
- [X] Implement a Schema builder for creating, editing, importing and deleting schemas. Auto populate properties from table. 
- [ ] Implement a template builder. Autopopulate properties from table.
- [X] Create export stage/view that allows to preview final json
- [X] Implement basic json diff viewer. Load from table, drag&drop file or manual input as both source/modified. View 
- [X] Add a changelog tracking versions and main changes.
- [ ] Implement merge functionality. Maybe added as a feature in diff view.
- [ ] Implement transform data stage. needs planning. Add conditions, conversion and formules
- [ ] Create global styling / constants to make it easier to tweak. Much inline styling for now.
- [ ] Implement undo/redo functionality for commands. Especially for bulk edit.
- [ ] Add extended metadata to cells for creating columns that do calculations etc without affecting the final output.
- [ ] Rework the command pattern. As for now, all commands are defined in commands. Implement command as trait with dispatch
- [ ] Separate alot of reusable items as components. (toolbar buttons, drag and drop zones)


### Bugs / improvements
- [X] DataImporter: Add support for .csv files and csv textinput.
- [X] DataImporter: File import, only show parse/clear if textedit is not empty
- [X] DataImporter: Add an inspector for datadrop. Showing the first 200 bytes or so. Detailed data modal (bytes as ascii etc).
- [X] DataImporter: Add an option to create a new table based on just schema from the import page
- [X] DataImporter: Clear the table data on new file import.
- [X] Dataimporter: Fix bug thats cause the importer view to get stuck when trying to drop an unsupported format. Handle this better.
- [ ] Dataimporter: Make the json pattern matcing more robust. Does not match on many newline and spaces.
- [ ] DataImporter: Add support for XLSX files.
- [ ] DataImporter: Add support for copy from Excel. XML/HTML clipboard metadata
- [X] DataImporter: Add support for .knxproj files. XML parse -> traverse to project.xml+0.xml. 
- [ ] DataImporter: Fix a bug where importing a .knxproj file, then importing a json/csv, keeps the KNX meta data shown. 

- [X] Schema mapper: Add an option to each schema property in the SchemaMapper to add default data before loading to table. Or add a button that applies default value to all properties that arent map yet.
- [X] Schema mapper: Preview the first row from the source data vertically. Change so you can drag and drop headers.
- [X] Schema mapper: Change the property dots on the schema properties to blue when default value is active.
- [X] Schema mapper: Split the view into three columns making more space between source->schema.
- [X] Schema mapper: Add a "Clear all" function as a button.
- [X] Schema mapper: Divide the source chips into two so property and value is more visually separated.
- [ ] Schema mapper: Change the height of each source property chip to match the schema property chips.
- [ ] Schema mapper: Polish the view UI.

- [ ] Table editor: Fix combobox issue when using cell focusing. 
- [ ] Table editor:Fix editing data when cells are focused (only when cell focusing is active). It now just add the chararcter that breaks edit twice into the textedit. 
- [ ] Table editor: Fix an issue where reordering columns breaks the validation.
- [ ] Table editor: Add some space under the table so the horizontal scroll doesnt get focus so quickly.
- [ ] Table editor: Add the option to edit the column daata type in edit_column modal using json types.
- [ ] Table editor: Center all the checkboxes in the columns. Should be consistant when resizing column.
- [ ] Table editor: Resize all the combobox widths when resizing the columns.
- [X] Table editor: Bulk edit doesnt take account for the column data type it seems. Bools are stored as string.
- [ ] Table editor: Add metadata with enums in bulk_editor modal. Combobox for enums, booleans.
- [X] Table editor: Add an option to modify the current schema in table editor if a schema is loaded.
- [X] Table editor: Change the add row slider to an input box.
- [X] Table editor: Fix delete column. Must be able to select column, now it deletes the first index
- [X] Table editor: Fix rename column. Now it only gets the first index.
- [X] Table editor: Add a function to reorder columns på dragging the column headers.
- [ ] Table editor: Fix bug when select all -> filter, keeps all total rows selected
- [ ] Table editor: Fix bug where object editor doesnt pretty print object anymore.
- [ ] Table editor: Add option to show row numbers.
- [ ] Table editor: Implement freezing columns.

- [ ] Exporter: Add export options. CSV delimiter ++, compressed/minified json
- [ ] Exporter: Add option to copy / paste the readonly preview data.
- [ ] Exporter: Add option to parse the output json without schema. Converting string values to bool, integer, numbers.

- [ ] Schema builder: Add support for more validation rules in schemabuilder: pattern (regex), min/max, formats ++
- [X] Schema builder: Add the option to export schemas
- [ ] Schema builder: Add better handling of enums with description. Const+OneOf. (enum - const.description)
- [ ] Schema builder: Add support for type in arrays and objects.
- [ ] Schema builder: Add support for uniqueitems in array, pref. on certain properties.
- [ ] Schema builder: Implement drag and drop order of schema properties.
- [ ] Schema builder: Add an option to add metadata to the schema (extra columns excluded from the json)

- [X] General: Show progress at step progress bar if there is table data. (if settings, import, map should be green)
- [ ] General: Make light mode theme more robust. Fix header, better borders in table, better headers in table.
- [ ] General: Add detailed status / debug in the footer

- [ ] Templates: Add the option to export templates
- [ ] Diff viewer: Add an option to export diff file. Export as html table for documentation, or a json that could be used to revert changes/apply to merge.
- [ ] Diff viewer: Add an option to select a property to be used as title in diff cards.
- [ ] Diff viewer: Add filtering by change and property values.

- [ ] Other: Investigate possibility to add alias in schema. Allowing for the schema mapper to match by alias, not only propertyname.
