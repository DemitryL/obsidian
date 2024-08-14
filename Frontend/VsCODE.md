#### Install vscode manjaro
```bash
sudo pacman -S code
```

##### EXTENSIONS
- Javascript Auto Backticks - автоматически конвертирует ' ' в \`${}\`
- Code Spell Checker - проверка ошибок написание слов
- colorize - для подсветки цветов
- ESLint - для работы в команде
- GraphQL: Syntax Highlighting
- GraphQL: Language Feature Support
- Live Server (Five Server) 
- Multiple cursor case preserve - Изменяет слова вне зависимости от написания
- Path Autocomplete - 
- Path Intellisense - подсказка путей
- Prettier - Code formatter - 
- Prisma - 
- Tailwind CSS IntelliSense -
- TODO Highlight v2
- Material Icon Theme -

### settings.json
```json
//Main editor settings
"editor.tabSize": 2,
"editor.folding": false,
"editor.insertSpaces": false,
"editor.smoothScrolling": true,
"editor.minimap.enabled": false,
"editor.detectIndentation": true,
"editor.suggestSelection": "first",
"editor.fontSize": 17,
"window.zoomLevel": 1,
```

```json
//Wrapping
"editor.wordWrap": "bounded",
"editor.wrappingIndent": "same",
"editor.wordWrapColumn": 80,
```

```json
//Determines whether the editor will scroll beyond the last line
"editor.scrollBeyondLastLine": true,
"editor.multiCursorModifier": "ctrlCmd",

//Rename tags
"editor.linkedEditing": true,

//Auto closing tags
"html.autoClosingTags": true,
"javascript.autoClosingTags": true,
"typescript.autoClosingTags": true,

//Determines whether the editor should display control characters
"editor.renderControlCharacters": false,
```

```json
// ==
"editor.unicodeHighlight.ambiguousCharacters": false,
"editor.quickSuggestionsDelay": 0,
"html.completion.attributeDefaultValue": "singlequotes",
```

```json
//Appearance
"editor.bracketPairColorization.enabled": false,
"editor.glyphMargin": false,
"editor.scrollbar.horizontal": "hidden",
"editor.scrollbar.vertical": "hidden",
"window.density.editorTabHeight": "compact",
"workbench.activityBar.location": "top",
"workbench.colorTheme": "Bearded Theme HC Brewing Storm",
"window.customTitleBarVisibility": "auto",
"editor.accessibilitySupport": "off",
"window.commandCenter": false,
"workbench.layoutControl.enabled": false,
```

```json
//Cursor
"editor.cursorBlinking": "expand",
"editor.cursorStyle": "line-thin",
"editor.cursorSmoothCaretAnimation": "explicit",
```

```json
//Font
"editor.fontSize": 16,
"editor.lineHeight": 25,
"editor.inlayHints.fontFamily": "PragmataPro",
```

```json
//Terminal
"terminal.integrated.tabs.enabled": false,
"terminal.integrated.fontSize": 16,

//Explorer
"explorer.confirmDelete": false,
"explorer.compactFolders": false,
"explorer.confirmDragAndDrop": false,

"workbench.editor.tabSizing": "shrink",
"workbench.startupEditor": "newUntitledFile",
```

```json
//Debug
"debug.toolBarLocation": "hidden",
"debug.focusWindowOnBreak": false,
"debug.showInlineBreakpointCandidates": false,
"debug.showBreakpointsInOverviewRuler": false,

//Emmet
"emmet.includeLanguages": {
 "blade": "html",
 "javascript": "javascriptreact"
},
"emmet.triggerExpansionOnTab": true,
```

```json
//Format
"prettier.semi": false,
"prettier.useTabs": true,
"editor.formatOnSave": true,
"prettier.singleQuote": true,
"prettier.jsxSingleQuote": true,
"editor.codeActionsOnSave": {
 "source.organizeImports": "explicit"
},
"[prisma]": {
 "editor.defaultFormatter": "Prisma.prisma"
},
// ==
"prettier.arrowParens": "avoid",
"editor.defaultFormatter": "esbenp.prettier-vscode",
// ==
"editor.inlineSuggest.enabled": true,

//Breadcrumbs
"breadcrumbs.icons": false,
"breadcrumbs.showKeys": false,
"breadcrumbs.showFiles": false,
"breadcrumbs.symbolPath": "off",
"breadcrumbs.showArrays": false,
"breadcrumbs.showEvents": false,
"breadcrumbs.showFields": false,
"breadcrumbs.showClasses": false,
"breadcrumbs.showMethods": false,
"breadcrumbs.showBooleans": false,
"breadcrumbs.showFunctions": false,
"breadcrumbs.showConstants": false,
"breadcrumbs.showEnumMembers": false,
"breadcrumbs.showConstructors": false,

//JS & TS
"javascript.updateImportsOnFileMove.enabled": "always",
"typescript.updateImportsOnFileMove.enabled": "always",
"typescript.preferences.quoteStyle": "single",
"javascript.preferences.quoteStyle": "single",
"javascript.format.semicolons": "remove",
"typescript.format.semicolons": "remove",
"js/ts.implicitProjectConfig.experimentalDecorators": true,

//Spell checker
"cSpell.language": "en,ru",
"cSpell.userWords": [],
"cSpell.enabled": true,
"cSpell.enableFiletypes": [
 "blade",
 "jsx",
 "tsx",
 "ts",
 "js",
 "scss",
 "sass",
 "vue"
],

"editor.unicodeHighlight.allowedCharacters": {
 "а": true,
 "с": true,
 "Т": true,
 "б": true,
 "е": true
},
"editor.hideCursorInOverviewRuler": true,
"git.enableSmartCommit": true,

"files.exclude": {
 "**/.expo": true,
 "**/.expo-shared": true,
 "**/.idea": true,
 "**/.next": true,
 "**/.nuxt": true,
 "**/dist": true
},

//OTHER
"files.defaultLanguage": "plaintext",
"diffEditor.ignoreTrimWhitespace": false,
"security.workspace.trust.untrustedFiles": "open",
"window.confirmBeforeClose": "keyboardOnly",
"git.openRepositoryInParentFolders": "never",
"editor.gotoLocation.multipleDefinitions": "goto",
"workbench.editor.empty.hint": "hidden"
```



