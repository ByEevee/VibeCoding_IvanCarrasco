# 02_model_del_joc

## 1. Components principals del joc

Aquest projecte defineix un fangame de tipus RPG per torns, inspirat en Pokémon, amb un abast reduït per adaptar-lo al temps disponible del projecte. L’objectiu principal del jugador és avançar per les primeres zones del mapa fins a derrotar el primer líder de gimnàs. Aquesta meta substitueix l’objectiu complet de la Lliga per un objectiu assumible dins del MVP.

El bucle principal del joc és el següent:

**Exploració del mapa → trobada amb un esdeveniment o combat → combat per torns → resolució de l’enfrontament → retorn a l’exploració.**

Durant la partida, el joc es divideix en diverses fases o espais narratius:

- Menú inicial i selecció de dificultat.
- Poble inicial.
- Ruta 1.
- Poble del gimnàs.
- Esdeveniment imprevist que bloqueja l’accés al gimnàs.
- Desbloqueig de la zona i combat contra el líder.

També hi ha diversos estats de funcionament del joc:

- **Exploració**
- **Batalla**
- **Pausa**
- **Cutscene**
- **Derrota**
- **Victòria**

A més, dins dels combats i de l’exploració, poden aparèixer estats especials com ara verí, paràlisi o son.

## 2. Entitats identificades

Per modelar correctament el joc, s’han identificat les entitats següents:

### Pokémon
És la unitat principal de combat. Cada Pokémon pertany a una espècie concreta i pot formar part de l’equip del jugador o del d’un enemic.

### Protagonista / Player
És l’entitat controlada pel jugador. Recorre el mapa, interactua amb personatges i participa en combats.

### Trainer
Representa qualsevol entrenador amb equip de Pokémon. És una classe conceptual útil per agrupar comportaments comuns entre el protagonista, els entrenadors rivals i el líder de gimnàs.

### Líder de gimnàs
És una especialització de Trainer amb un equip definit i una recompensa concreta associada a la seva derrota.

### Enemic
És una entitat oposada al jugador en combat. Pot representar entrenadors o Pokémon salvatges segons el tipus de trobada.

### Professor
És una figura narrativa inicial que introdueix el món del joc i lliura el primer Pokémon.

### Amics del poble
Són personatges que aporten suport, diàleg o informació al jugador dins dels pobles.

### Entrenadors aleatoris
Són enemics opcionals trobats a les rutes. Permeten practicar el combat i obtenir experiència.

### Pokémon salvatges
Són criatures que apareixen fora de combats predefinits i permeten capturar nous membres per a l’equip.

### Item
Representa qualsevol objecte utilitzable, com ara Pokéballs, objectes curatius o altres recursos.

### Bag
És l’inventari del jugador. Agrupa i gestiona els objectes disponibles.

### Battle
És la unitat que encapsula un combat concret. Té inici, desenvolupament i final.

### GameState
És la representació conceptual de l’estat global del joc. Controla si el jugador està explorant, en batalla, en pausa, en cutscene, en derrota o en victòria.

### MapEvent / Trigger
És una entitat que representa una condició del mapa associada a una acció. Serveix per activar combats, cutscenes o bloquejos narratius.

### SaveData
És l’estructura encarregada de desar i restaurar l’estat de la partida.

### NuzlockeRules
És el conjunt de regles especials que s’apliquen quan el mode Nuzlocke està actiu.

### EventManager
Gestiona els triggers del mapa, els esdeveniments narratius i l’inici de combats.

### BattleManager
Orquestra el combat i coordina els torns, les condicions de victòria i derrota i l’aplicació de regles especials.

## 3. Atributs clau de cada entitat

### Pokémon
Un Pokémon no hauria de concentrar totes les dades fixes i dinàmiques dins d’un sol bloc monolític. Per això, es divideix conceptualment en parts:

- **species**: referència immutable a les dades de l’espècie.
- **level**: nivell actual.
- **exp**: experiència acumulada.
- **stats**: estructura amb `hp`, `attack`, `defense`, `spAtk`, `spDef` i `speed`.
- **status**: estructura amb el tipus d’estat alterat i els torns restants.
- **moveset**: conjunt de moviments i punts de poder actuals.
- **name**: nom personalitzat, si escau.

### SpeciesData
Conté les dades fixes i compartides entre totes les instàncies d’una mateixa espècie:

- nom
- tipus
- estadístiques base
- evolució
- moviments base

### Protagonista / Player
- nom
- aparença
- dificultat triada
- posició al mapa
- diners
- medalles
- inventari
- equip de Pokémon

### Trainer
- nom
- equip de Pokémon
- posició o context narratiu
- diàleg o identificació
- tipus d’entrenador

### Líder de gimnàs
- nom
- especialitat de tipus
- equip configurat
- medalla que atorga
- estat actual del combat

### Item
- nom
- tipus
- efecte
- quantitat disponible

### Bag
- llista d’objectes
- quantitats per objecte
- límit o capacitat, si existeix

### Battle
- combatents
- torn actual
- estat de resolució
- resultat
- registre d’accions

### GameState
- estat actual del joc
- llista de transicions vàlides
- bandera de dificultat / mode Nuzlocke

### MapEvent / Trigger
- posició al mapa
- condició d’activació
- acció associada
- estat de resolució del trigger

### SaveData
- dades del jugador
- equip actiu
- caixa o reserva de Pokémon
- banderes de progrés
- temps de joc
- dificultat triada

### NuzlockeRules
- estat d’activació
- regles de permanència
- regles de captura
- comportament davant de debilitament

## 4. Accions, mètodes o funcions principals

### Pokémon
- atacar
- rebre dany
- aplicar o perdre un estat alterat
- pujar de nivell
- ser capturat
- quedar debilitat

### Protagonista / Player
- moure’s pel mapa
- interactuar amb personatges i objectes
- obrir el menú
- canviar de Pokémon
- usar objectes
- guardar la partida

### Trainer
- iniciar combat
- seleccionar accions del seu equip
- mostrar diàleg
- lliurar recompensa si és vençut

### Líder de gimnàs
- bloquejar o permetre l’accés segons la narrativa
- iniciar el combat de gimnàs
- entregar la medalla en cas de derrota

### Item / Bag
- afegir objectes
- consumir objectes
- consultar inventari
- usar un objecte sobre un Pokémon o sobre el jugador

### Battle
- iniciar el combat
- avançar torns
- registrar accions
- determinar si hi ha victòria, derrota o fugida
- finalitzar el combat

### GameState
- guardar l’estat actual del joc
- indicar les transicions possibles
- servir de referència per al canvi de mode

### MapEvent / Trigger
- detectar condicions de mapa
- activar una cutscene
- iniciar un combat
- desbloquejar una zona
- actualitzar banderes internes

### SaveData
- serialitzar l’estat de la partida
- deserialitzar l’estat desat
- conservar el progrés

### NuzlockeRules
- comprovar si el mode està actiu
- aplicar la regla de permanència permanent quan un Pokémon es debilita
- validar restriccions especials

### BattleManager
- iniciar el combat
- decidir l’ordre dels torns
- coordinar jugador i enemic
- aplicar dany i efectes
- comprovar condicions de fi
- aplicar les regles del mode Nuzlocke

### EventManager
- detectar triggers del mapa
- decidir quan comença un combat
- gestionar cutscenes
- coordinar esdeveniments narratius

## 5. Explicació del diagrama de classes

El diagrama de classes representa l’estructura conceptual del joc i mostra quines entitats existeixen, quines dades guarden i com es relacionen entre elles. No és un diagrama decoratiu, sinó un mapa del futur codi.

Les classes essencials que hi apareixen són:

- `Trainer`
- `Player`
- `GymLeader`
- `Pokemon`
- `SpeciesData`
- `BattleManager`
- `Battle`
- `Item`
- `Bag`
- `GameState`
- `MapEvent`
- `EventManager`
- `SaveData`
- `NuzlockeRules`

### Organització de les relacions

- **Herència**: `Player` i `GymLeader` hereten de `Trainer`.
- **Composició**: `Trainer` conté una col·lecció de `Pokemon`; si el trainer desapareix, els seus Pokémon també deixen de formar part del seu equip.
- **Composició**: `Pokemon` conté `Stats`, `Moveset` i `StatusEffect`.
- **Agregació**: `SaveData` referencia el jugador i la reserva, però aquestes dades poden existir com a objectes conceptualment independents.
- **Dependència**: `BattleManager` utilitza `NuzlockeRules`.
- **Dependència**: `EventManager` utilitza `BattleManager`.
- **Associació**: `MapEvent` s’associa a una posició del mapa i a una condició d’activació.

Aquesta organització permet separar responsabilitats i evitar que una única classe concentri tota la lògica del joc.

## 6. Explicació del diagrama de comportament

S’ha triat un model amb dos nivells de comportament perquè el joc té dos fluxos diferents: el flux global i el flux intern del combat.

### Nivell 1: diagrama d’estats del joc
Aquest diagrama representa l’estat general del sistema durant tota la partida:

- **INICI**
- **EXPLORANT**
- **PAUSA**
- **CUTSCENE**
- **BATALLA**
- **DERROTA**
- **VICTÒRIA**

Les transicions es produeixen segons el context del joc:

- des d’**INICI** es passa a **EXPLORANT**
- des d’**EXPLORANT** es pot anar a **PAUSA**
- des d’**EXPLORANT** es pot entrar a **CUTSCENE** quan s’activa un esdeveniment narratiu
- des d’**EXPLORANT** es pot entrar a **BATALLA** quan hi ha una trobada
- des de **BATALLA** es torna a **EXPLORANT** si el jugador guanya o fuig
- des de **BATALLA** es passa a **DERROTA** si l’equip queda sense Pokémon
- des de **BATALLA** es pot passar a **VICTÒRIA** quan es completa l’objectiu final del projecte

Aquest diagrama reflecteix el bucle de joc des del punt de vista del jugador.

### Nivell 2: diagrama d’activitat del combat
Aquest segon diagrama representa el que passa dins d’una batalla:

1. S’inicia el combat.
2. Es determina l’ordre dels torns segons la velocitat i la prioritat.
3. El jugador tria acció:
   - atacar
   - usar un objecte
   - canviar de Pokémon
   - fugir
4. L’enemic tria la seva acció.
5. S’executen les accions en l’ordre corresponent.
6. S’apliquen els efectes de torn, com ara verí o son.
7. Es comprova l’estat dels Pokémon.
8. Si un Pokémon arriba a 0 PS:
   - si el mode Nuzlocke està actiu, es retira permanentment
   - si l’equip del jugador queda buit, hi ha derrota
9. Si l’equip enemic queda buit, s’acaba el combat amb victòria.
10. Si el combat no acaba, es torna a la fase de tria d’acció.

Aquest diagrama és útil perquè mostra el flux real de l’acció i separa clarament la lògica del torn de la lògica global del joc.

## 7. Correspondència entre els diagrames i el codi futur

El model s’ha pensat perquè es pugui traduir directament a codi Ruby dins de Pokémon Essentials, amb els canvis mínims necessaris.

### Correspondències principals

- `BattleManager` → lògica central de `PokeBattle_Battle.rb`
- `BattleManager.processTurn()` → fase de processament de torns dins del combat
- `NuzlockeRules` → script nou, per exemple `NuzlockeSystem.rb`
- `Pokemon` → classe o estructura de Pokémon del sistema
- `EventManager` → lògica d’events i trobades al mapa
- `MapEvent` → triggers de mapa i variables de control
- `SaveData` → sistema de desat i càrrega
- `GameState` → estat conceptual que es tradueix en flags, escenes i variables del motor

### Elements que no existeixen exactament a Essentials i que caldrà afegir o adaptar

- la lògica específica del mode Nuzlocke
- la gestió explícita del flag de l’imprevist
- part de la interfície associada a les regles especials
- la capa conceptual de `GameState`, encara que el motor ja tingui els seus propis estats interns

### Com es passa del model al codi
Cada classe del model es convertirà en una classe, mòdul o secció funcional del projecte. Els atributs del diagrama passaran a ser variables d’instància o estructures de dades. Les accions principals es convertiran en mètodes concrets. D’aquesta manera, el model serveix com a guia estable abans d’entrar a implementar.

## 8. Estructura inicial del repositori

L’estructura inicial del repositori ha de ser clara, simple i fàcil d’escalar. Una proposta adequada és la següent:

```text
pokemon-nexes-distopics/
├── README.md
├── docs/
│   ├── 01_idea_i_abast.md
│   └── 02_model_del_joc.md
├── diagrames/
│   ├── diagrama_classes.png
│   └── diagrama_comportament.png
├── src/
│   └── Nuzlocke_System.rb
└── assets/
    ├── sprites/
    ├── tilesets/
    └── audio/
```

### Justificació de l’estructura
- `docs/` conté la documentació del projecte.
- `diagrames/` agrupa les imatges exportades dels diagrames.
- `src/` conté el codi propi del projecte.
- `assets/` conté recursos gràfics i sonors, encara que en una primera fase pugui estar parcialment buit.

Aquesta organització anticipa una evolució neta del projecte i facilita la navegació pel repositori.

## 9. Primer commit i README inicial

El primer commit ha d’existir realment i ha de servir com a prova que el projecte ha començat correctament. Ha de deixar constància de l’estructura inicial i del primer estat de treball.

### Contingut del primer commit
- `README.md` inicial
- estructura bàsica de carpetes
- documentació inicial de disseny

### Contingut del README inicial
El README ha d’incloure, com a mínim:

- nom del projecte
- descripció breu del joc
- abast del projecte
- estat actual
- tecnologia utilitzada
- avís que es tracta d’un fangame no comercial
- indicació de què està implementat i què encara no

### Exemple de missatge útil per al primer commit
`Initial project structure and README`

Aquest primer commit no ha de contenir tota la lògica del joc, sinó només la base documental i organitzativa.

## 10. Conclusió

El model del joc és coherent amb la idea definida a la fase anterior i està prou concretat per servir de base a la implementació. Les entitats principals estan identificades, les seves responsabilitats estan separades i els diagrames representen tant l’estructura com el comportament del sistema.

Els punts més importants del model són:

- el combat està centralitzat en `BattleManager`
- els esdeveniments del mapa es gestionen amb `EventManager`
- el mode Nuzlocke s’encapsula en `NuzlockeRules`
- l’estat global del joc es representa amb `GameState`
- `Pokemon` es divideix en dades mutables i dades fixes per evitar redundàncies

En conjunt, aquest model no és decoratiu: està pensat per convertir-se en codi real amb una estructura clara, mantenible i coherent amb el joc que es vol programar.
