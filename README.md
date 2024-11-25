# sahavision-test

Здравствуйте, тестовое задание выполнено с использованием Vue 3, TS и Composition API.
Компонент App: корневой компонент, в нём описаны тестовые данные и вывод id выбранной папки, вызывается Modal.
Компонент Modal: модальное окно с интуитивным понятным дизайном и кнопками. Тут же вызывается компонет дерева FolderTree.
Компонент FolderTree: само дерево папок.
Компонент FolderNode: "лист" нашего дерева.

В файле types.ts описаны поля папок.

Id выбранной папки выводится в консоль и в интерфейс.

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
