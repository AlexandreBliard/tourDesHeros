### memento Angular

# commande ng
```
  ng new angular-tour-of-heroes
```
permet de créer un nouveau projet angular

```
  ng serve --open
```
permet de builder l'app, de démarrer le serveur, lire les fichiers soucres et de rebuild si nous apportons un changement. --open permet de l'ouvrir de suite dans un navigateur

```
ng generate component heroes
```
CLI va créer un composant héros et créer un dossier avec 4 fichiers (.html, .scss, .spec.ts et .ts)

# faire communiquer les pages
Nous avons notre page principal qui est app.component.html
Nous avons un component heros dans lequel nous avons dans le fichier html
```<p>heroes works!</p>```
pour le voir dans notre page il suffit de mettre dans le fichier html de app.component.html```<app-heroes></app-heroes>``` et le tour est joué.

# utiliser une interface
dans le dossier app créer un fichier .ts puis utiliser ceci```export interface Hero {
  id: number;
  name: string;
}``` ainsi nous avons un Héro qui a un id et un nom

il faut ensuite l'importer dans la heroes.component.ts ```import {Hero} from "../hero";``` en haut de la fenêtre puis le configurer dans la classe HeroesComponent ```hero: Hero = {
    id: 1,
    name: 'Windstorm'
  };``` puis ensuite dans le fichier heroes.component.html il faut spécifier où doivent aller les infos, en effet HTML ne sait pas lire des objets ```<h2>{{hero.name}} Details</h2>
<div><span>id : </span>{{hero.id}}</div>
<div><span>name : </span>{{hero.name}}</div>``` et voilà

# le Two-ways binding
il permet à ce qu'un champ de saisie soit à la fois un champ *display* et un champ *update*

```
<div>
  <label>name:
    <input [(ngModel)]="hero.name" placeholder="specify name"/>
  </label>
</div>
```
à mettre dans le html.
dans app.module.ts il faut ensuite importer FormsModule 
```
import {FormsModule} from "@angular/forms";
```
puis le marquer dans les imports
```
  imports: [
    BrowserModule,
    FormsModule
  ],
```

# importer des données et les afficher
nous avons un tableau qui reprend notre interface de Hero. Ce tableau s'appelle mock-heroes et le tableau HEROES (oui c'est une constante). Nous devons l'importer dans notre heroes.component.ts 
```
import {HEROES} from "../mock-heroes";
//dans la classe
heroes = HEROES;
```
puis dans le fichier heroes.component.html
```
<ul class="heroes">
  <li *ngFor="let hero of heroes">
    <span class="badge">{{hero.id}}</span> {{hero.name}}
  </li>
</ul>
```
cela reprend heroes (heroes = HEROES) puis devient hero et on n'a plus qu'à récupérer à chaque itération l'info désiré (hero.name)
on peut aussi ajouter  ceci :
```
  *ngFor="let hero of heroes" (click)="onSelect(hero)"
```
il faut ensuite aller dans le fichier .ts pour paramétrer la fonction onSelect(hero)
```
selectedHero: Hero;
  onSelect(hero: Hero): void {
    this.selectedHero = hero;
  }
```
mais par conséquent notre code avec la sélection qui fonctionnait avec hero.id ne fonctionne plus, il faut le définir comme selectedHero.id
et rajouter un ``` *ngIf="selectedHero"``` pour vérifier si un héros est ou non sélectionné. Dès que nous chargerons la page, iol n'existera pas, mai spar conséquent Angular se chargera de cacher cette partie là.

