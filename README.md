# JIGSON - A JSON editor that loves schemas.
##Description
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
* Importing data
  - Supports json, csv and .knxproj as drag&drop file input. Data type is automatically detected by pattern matching the first bytes of the file.
  - Supports copy/pasting in raw json, csv data.
  - Validates if can be parsed to a valid json.
* Mapping the data
  - Source json properties can be mapped to schema properties. Easy convert from one json structure to another.
  - Automap all properties that are exactly matching the schema properties.
* Editing the data
  - Create a schema based on the loaded json properties using the builtin SchemaBuilder or import schema file.
  - Live validation of all cells against json schema.
  - Create or remove rows and columns.
  - Autofill certain columns with incremental value.
  - Advanced filtering of rows
  - Bulk edit. Edit all columns to a specific value for selected rows.
  - Templating. Apply changes to all objects that match a certain criteria. Can edit many feilds.

## Quick and dirty TODO until more complete release:

### New features/larger refactors:
- [X] Schema builder. Changing schema is now broken as the editor spawns in the bottom. Should be able to create from settings+table editor
- [ ] Template builder with possibility to create a template based on the table columns.
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
- [ ] Export diff file. Export as html table for documentation, or a json that could be used to revert changes/apply to merge.

### Bugs / improvements
- [X] Add an option to each schema property in the SchemaMapper to add default data before loading to table. Or add a button that applies default value to all properties that arent map yet.
- [ ] Make light mode theme more robust. Fix header, better borders in table, better headers in table.
- [ ] Fix combobox issue when using cell focusing. 
- [ ] Fix editing data when cells are focused (only when cell focusing is active). It now just add the chararcter that breaks edit twice into the textedit. 
- [ ] Fix an issue where reordering columns breaks the validation.
- [ ] Add some space under the table so the horizontal scroll doesnt get focus so quickly.
- [ ] Add export options. CSV delimiter ++, compressed/minified json
- [ ] Add the option to edit the column daata type in edit_column modal using json types.
- [ ] Center all the checkboxes in the columns. Should be consistant when resizing column.
- [ ] Resize all the combobox widths when resizing the columns.
- [X] Bulk edit doesnt take account for the column data type it seems. Bools are stored as string.
- [ ] Add metadata with enums in bulk_editor modal. Combobox for enums, booleans.
- [X] File import, only show parse/clear if textedit is not empty
- [X] Add an option to create a new table based on just schema from the import page
- [X] Show progress at step progress bar if there is table data. (if settings, import, map should be green)
- [X] Add an option to modify the current schema in table editor if a schema is loaded.
- [X] Change the add row slider to an input box.
- [X] Fix delete column. Must be able to select column, now it deletes the first index
- [X] Fix rename column. Now it only gets the first index.
- [X] Add a function to reorder columns på dragging the column headers.
- [X] Clear the table data on new file import.
- [X] Add the option to export schemas
- [ ] Add the option to export templates
- [ ] Add detailed status / debug in the footer
- [ ] Add support for more validation rules in schemabuilder: pattern (regex), min/max, formats ++
