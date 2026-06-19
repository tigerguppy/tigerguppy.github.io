# Endpoint Forge v8.0.0

Endpoint Forge v8.0.0 is a breaking data-model reset that moves the project toward a portable project-container workflow.

## Major changes

- Introduced the `.eforge` portable project container.
- Reduced the active project model to one project file instead of separate catalog/state/log JSON files.
- Removed browser recovery/autosave storage from the intended workflow.
- Added explicit `Saved` / `Unsaved` state tracking.
- Added Save Project buttons across configurable pages and workflows.
- Added first-class Clients, Profiles, Endpoints, Item Repository, Checklists, Generated Outputs, and Settings workflows.
- Added endpoint tracking with profile assignment, endpoint-level include/exclude overrides, and endpoint history.
- Added first-class Item Actions: precheck, install, configure, verify, repair, remediate, update, uninstall, offboard, rollback, audit, and manual.
- Renamed the main item area to Item Repository while keeping individual records as Items.
- Replaced Artifact Kind / duplicate Type language with Item Type.
- Added global settings for Operating Systems, Script Types, Phases, Item Types, Categories, and Tags.
- Added script type file-extension management.
- Added per-item OS settings for Manual Process and Disabled for this Item.
- Added generated output previews and ZIP export.
- Added global and client checklist support, including auto-generated checklists based on repository item criteria.
- Added Contoso Ltd and Fabrikam Inc sample data.

## Storage model

Endpoint Forge v8 saves a single `.eforge` project file. The file is an unencrypted ZIP-style container containing:

```text
manifest.json
project.json
```

The current v8 project file includes catalog data, client data, profiles, endpoints, checklist state, secrets, settings, and logs in the project payload.

## Important security note

The v8 `.eforge` container is **not encrypted**. Do not publish or share real client secrets in a project file.

The current hosted app does not use network calls and includes a restrictive Content Security Policy. User-generated data is rendered as escaped text wherever practical.

## Save model

- Changes remain in memory until Save Project is used.
- If the browser supports the File System Access API, Save Project can write back to the selected `.eforge` file after user permission.
- If the browser does not support writable file handles, Save Project downloads a new `.eforge` file.
- Browser localStorage/sessionStorage is not used for project autosave in v8.

## Blank Slate and sample data

- Blank Slate resets all current in-memory project data after two confirmations, including a typed `BLANK SLATE` confirmation.
- Load Sample Data explicitly loads demo data using Microsoft demo company names.

## AGPL-3.0-or-later notes

This build is marked with `SPDX-License-Identifier: AGPL-3.0-or-later` and includes an in-app legal notice. When publishing the project, include the complete corresponding source and a full copy of the GNU Affero General Public License v3.0 in the public repository.

## No migration layer

Per the v8 request, this build does not include v7-to-v8 schema migration. v8 is intended to start fresh.


## GitHub Pages deployment filenames

This package uses stable repository filenames so updates are easier:

```text
index.html
README.md
docs/AGPL-COMPLIANCE-NOTES.md
samples/endpoint-forge-sample.eforge
```

For future releases, the outer downloadable ZIP may include the version number, but the deployable files inside the ZIP should keep these stable names. Updating the hosted site should normally be a file overwrite instead of renaming versioned HTML files.
