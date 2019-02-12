# Introduction aux modules
Les modules Angular, sont similaires aux modules JS, mais ils y ajoutent des fonctionnalités. Ils s'agit de modules NgModules. Ce sont des containers contenant le code relatif à un domaine, un WorkFlow ou une fonctionnalité. Ils peuvent contenir des composants, ou des services, ainsi que d'autres fichiers de code, des l'instant qu'ils sont définit dans le scope du NgModule, ils peuvent également importer et exporter des fonctionnalités depuis ou vers d'autres modules.

Toute application Angular a au moins 1 module Angular, la racine : AppModule dans *app.module.ts*. L'application Angular se lance par ce module.

## NgModule metadata
Un NgModule est défini par un décorateur de class ==@NgModule( )==, ce décorateur prend un objet de métadata avec les propriétés suivante :

- declarations: les components, directives et pipes relatif au NgModule.
- exports: éléments du module qui doivent être accessible depuis les templates d'autres modules.
- imports: les components dont à besoin le module.
- providers: liste des services fournit par le module, il est souvent préférable de définir les services au niveau du composant.
- bootstrap: la vue principale de l'application, seul le composant root définit  cette propriété.

exemple :

```ts
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
@NgModule({
  imports:      [ BrowserModule ],
  providers:    [ Logger ],
  declarations: [ AppComponent ],
  exports:      [ AppComponent ],// not needed in root module
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```
Un composant peut utiliser plusieurs éléments provenant de différent modules, et les assembler dans une seul et même vue : ![enter image description here](https://angular.io/generated/images/guide/architecture/view-hierarchy.png)

A la création d'un composant, il est associé à une vue qui s'appelle host view, cette vue peut être le root d'une hiérarchie de plusieurs vues, et ainsi embarqué des vues qui sont les host view d'autres composant. Ces vues peuvent provenir du même module, ou d'autres modules. Elles peuvent ainsi s'imbriquer autant que nécessaire.

## Angular librairies
![enter image description here](https://angular.io/generated/images/guide/architecture/library-module.png)
Les modules Angular sont en quelque sorte une collection de modules JS, ont peu les voir comme une librairie. Les librairies angular commencent toujours par ==@angular==

exemple :
```ts
import { Component } from '@angular/core';
```

Importation dans l'objet métadata du NgModule:
```ts
imports:      [ BrowserModule ],
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbODc2NTcwMzI3XX0=
-->