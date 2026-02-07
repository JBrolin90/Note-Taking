Title: Technical Setup & Configuration Tags: #meta #setup #linux

1. Directory Structure
Ensure the root directory ~/Documents/Brain follows this layout:

/journals: Logseq daily logs (Obsidian Daily Notes).

/pages: Shared Wiki content and project notes.

/assets: Images, diagrams, and PDFs.

2. Logseq Configuration (config.edn)
Ensure these keys are set for Obsidian compatibility:

:pages-directory "pages"

:journal/file-name-format "yyyy_MM_dd"

:preferred-format :markdown

3. Obsidian Configuration
Daily Notes Plugin: Set "Date format" to YYYY_MM_DD and "New file location" to journals/.

Excluded Files: Use File Explorer++ to hide bin/, obj/, and .git/ via regex: ^(\.git|bin|obj)$.

Symlinks: Link project READMEs from source code into the vault: ln -s ~/projects/NavIntel/README.md ~/Documents/Brain/pages/NavIntel_README.md

4. Git Integration
Use the provided .gitignore to exclude workspace.json and Logseq metadata to prevent sync conflicts between devices.