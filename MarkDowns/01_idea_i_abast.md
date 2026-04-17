# 01_idea_i_abast

## 1. Títol provisional del joc
**Pokémon: Nexes Distòpics** (o el nom que prefereixis per a la teva regió).

## 2. Tipus de microvideojoc escollit
**RPG de col·lecció de criatures** (fangame basat en el motor de Pokémon Essentials).

## 3. Objectiu del joc
L’objectiu principal és demostrar la vàlua del jugador com a entrenador derrotant els dos primers líders de gimnàs de la regió, mentre es gestiona la supervivència de l’equip segons el mode de dificultat escollit.

## 4. Rol del jugador
El jugador controla un entrenador/a Pokémon en vista top-down. Pot interactuar amb l’entorn (NPCs, objectes), capturar criatures salvatges, gestionar el seu equip des del menú i prendre decisions tàctiques durant els combats per torns.

## 5. Regles bàsiques

- **Combats per torns:** el jugador tria atacs, objectes o canvis de Pokémon.
- **Exploració:** moviment per quadrícula en herba alta per trobar trobades aleatòries.
- **Gestió de recursos:** ús de la motxilla per a curació i captures (Pokéballs).
- **Modes de joc:**
  - **Mode Fàcil:** si l’equip és derrotat, es torna al darrer punt de control.
  - **Mode Nuzlocke:** si un Pokémon cau en combat, es considera “mort” i s’ha d’alliberar o deixar al PC permanentment.

## 6. Condicions de victòria i derrota

- **Victòria:** guanyar la medalla del segon gimnàs.
- **Derrota:**
  - **Mode Fàcil:** perdre tots els diners o quedar-se sense Pokémon actius (retorn al centre).
  - **Mode Nuzlocke:** quedar-se sense cap Pokémon disponible a l’equip ni al PC per continuar lluitant.

## 7. Bucle principal del joc

- **Exploració / narració:** parlar amb NPCs i moure’s cap al següent objectiu.
- **Combat / captura:** debilitar Pokémon per pujar de nivell o ampliar l’equip.
- **Curació / gestió:** utilitzar el “Vial de curació” o el menú per mantenir l’equip sa.
- **Repetició:** avançar fins a arribar al repte del Gimnàs.

## 8. Repte principal i dificultat
El repte principal és l’estratègia de combat i la gestió del risc, especialment en mode Nuzlocke. La dificultat es preveu mitjana, escalant ràpidament cap al segon gimnàs per obligar el jugador a entrenar.

## 9. Limitacions explícites

- **Abast geogràfic:** màxim 2 rutes, 1 poble inicial i 2 ciutats amb gimnàs.
- **Sense multijugador:** el joc és estrictament single-player.
- **Interfície:** s’utilitzaran els menús estandarditzats de Pokémon Essentials per no perdre temps en programació de UI complexa.
- **Història:** trama mínima i directa per centrar-se en el gameplay.

## 10. Riscos tècnics

- **Incompatibilitat de scripts:** afegir el sistema de Nuzlocke sobre la base d’Essentials pot generar errors de lectura en el llenguatge Ruby (RGSS).
- **Rendiment de RPG Maker XP:** el motor és antic; mapes massa grans o massa esdeveniments en paral·lel poden causar lag.
- **Alineació de sprites:** adaptar el contingut de la 5a generació (estil DS) a la resolució d’Essentials pot requerir ajustos manuals de posicionament en els combats.

## 11. Exploració amb IA (mínim 2 prompts)

**Prompt 1:** “Com implementar un interruptor global (switch) a Pokémon Essentials que activi el mode Nuzlocke (mort permanent) al script de debilitat?”

**Resposta resumida:** s’ha de modificar el mètode `pbAbilityOnPlayerParty` o la funció de debilitat al script `PokeBattle_Battle` per comprovar si el Switch X està actiu i moure el Pokémon a una caixa específica o eliminar-lo.

**Prompt 2:** “Dissenya una corba de nivells equilibrada per a 2 gimnasos en un microvideojoc de 10 hores de Pokémon.”

**Resposta resumida:** Gimnàs 1 (nivell 10-12), Gimnàs 2 (nivell 18-20). Es recomana posar un “rival” entremig per assegurar que el jugador arriba al nivell correcte.

## 12. Proposta final escollida
Es realitzarà el fangame fent servir Pokémon Essentials v21.1 (o versió similar), centrant l’esforç en el disseny de nivells (level design) i la implementació del sistema de dificultat dual.

## 13. Justificació de viabilitat
Tenint en compte que ja hi ha una base de treball prèvia i que el motor ja gestiona les mecàniques base, l’objectiu de 10 hores és viable si es reutilitzen tilesets de 5a generació i es limita el nombre de criatures disponibles (Pokédex reduïda).

## 14. Mini pla de treball

- **Hores 1-2:** configuració de scripts (Nuzlocke mode i Vial de curació).
- **Hores 3-6:** mapeig de les 2 ciutats, rutes i interiors dels gimnasos.
- **Hores 7-8:** configuració d’entrenadors, líders i esdeveniments (events).
- **Hores 9-10:** testing, correcció d’errors de Ruby i exportació.

## 15. Eines previstes i justificació

- **RPG Maker XP:** motor base obligatori per a Pokémon Essentials.
- **Pokémon Essentials:** framework que estalvia centenars d’hores de programació.
- **Piskel o Photopea/Photoshop:** per a retocs ràpids de sprites de la 5a generació.
- **Notepad++:** per a l’edició ràpida de scripts en Ruby.
