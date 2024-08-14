#### Комбинации nvim

```bash
Ctrl + j - open terminal
Ctrl + [ - step back
Ctrl + ] - step up
Ctrl + arrows - перемещенире по файлу

```

#### Расширения :
```
- editorconfig for vs code
- eslint
- github theme
- live server
- material icon theme
- path autocomplete
- prettier - code formatter
- sass(.sass only)
- stylelint
- vscode neovim
```

#### Вставляем в файл settings.json :

```json
{
	"editor.fontFamily": "JetBrains Mono",
	"editor.parameterHints.enabled": false,
	"editor.hover.enabled": false,
	"editor.renderWhitespace": "boundary",

	"editor.lineHeight": 23,
	"editor.fontSize": 18,
	"terminal.integrated.fontSize": 16,

	"security.workspace.trust.enabled": false,
	"editor.insertSpaces": false,
	"explorer.confirmDelete": false,

	"editor.formatOnPaste": true,
	"editor.defaultFormatter": "esbenp.prettier-vscode",
	"prettier.useTabs": true,
	"prettier.semi": false,
	"prettier.jsxSingleQuote": true,
	"prettier.singleQuote": true,
	"prettier.arrowParens": "avoid",

	"breadcrumbs.icons": false,
	"breadcrumbs.showKeys": false,
	"breadcrumbs.showFiles": false,
	"breadcrumbs.symbolPath": "off",
	"breadcrumbs.showArrays": false,
	"breadcrumbs.showBooleans": false,
	"breadcrumbs.showClasses": false,
	"breadcrumbs.showConstants": false,
	"breadcrumbs.showConstructors": false,
	"breadcrumbs.showEnumMembers": false,
	"breadcrumbs.showEvents": false,
	"breadcrumbs.showFields": false,
	"breadcrumbs.showEnums": false,
	"breadcrumbs.showFunctions": false,
	"breadcrumbs.showInterfaces": false,
	"breadcrumbs.showMethods": false,
	"breadcrumbs.showModules": false,
	"breadcrumbs.showNamespaces": false,
	"breadcrumbs.showNull": false,
	"breadcrumbs.showNumbers": false,
	"breadcrumbs.showObjects": false,
	"breadcrumbs.showOperators": false,
	"breadcrumbs.showPackages": false,
	"breadcrumbs.showProperties": false,
	"breadcrumbs.showStrings": false,
	"breadcrumbs.showStructs": false,
	"breadcrumbs.showTypeParameters": false,
	"breadcrumbs.showVariables": false,

	"editor.minimap.renderCharacters": false,
	"editor.minimap.enabled": false,

	"editor.wordWrap": "on",
	"editor.unicodeHighlight.ambiguousCharacters": false,
	"explorer.confirmDragAndDrop": false,
	"editor.tabSize": 2,
	"editor.formatOnSave": true,
	"explorer.compactFolders": false,
	"editor.smoothScrolling": true,

	"workbench.list.smoothScrolling": true,
	"workbench.tree.renderIndentGuides": "none",
	"workbench.sideBar.location": "right",
	"workbench.startupEditor": "none",
	"workbench.tips.enabled": false,

	"terminal.integrated.smoothScrolling": true,
	"editor.cursorBlinking": "solid",
	"terminal.integrated.cursorBlinking": true,

	"editor.glyphMargin": false,
	"editor.linkedEditing": true,
	"editor.padding.top": 15,

	"emmet.includeLanguages": {
		"javascript": "javascriptreact",
		"typescript": "typescriptreact"
	},

	"http.proxySupport": "fallback",

	"material-icon-theme.hidesExplorerArrows": true,
	"workbench.iconTheme": "material-icon-theme",

	"editor.guides.indentation": false,
	"editor.renderLineHighlight": "none",
	"editor.scrollbar.vertical": "hidden",
	"editor.overviewRulerBorder": false,

	"path-autocomplete.pathMappings": {
		"@img": "${folder}/src/img",
		"@scss": "${folder}/src/scss",
		"@js": "${folder}/src/js"
	},
	"extensions.experimental.affinity": {
		"asvetliakov.vscode-neovim": 1
	},
	"workbench.colorTheme": "GitHub Dark"
}
```