# Project Andora mobile app v1 specification

Document version: 0.2.0.

## Basic information

The product is mobile app supporting iOS and Android platforms. Its functionality is simple tic-tac-toe-based game with more complex rules. The game is supposed to be played by two people on a single device, it does not support online multiplayer (at least not in v1). Basic requirements:

Description | Value
--- | ---
Supported iOS version | ≥9.0
Supported Android version | ≥4.1
Supported orientations | portrait and landscape
Tablet support | ???
Supported languages | EN and RU
Special features | none

## Game mechanics

__R1__ The game is based on tic-tac-toe and has similar rules.

__R1.1__ Game field is 3x3 grid containing mini-fields.

__R1.2__ Mini-field is 3x3 grid, each cell of which can have state: __empty__ OR marked with __X__ OR marked with __O__. Initial value is __empty__.

__R1.3__ The whole mini-field has its own state that can be: __empty__ OR marked with __X__ OR marked with __O__ OR marked with __?__. Initial value is __empty__.

__R1.4__ An option called __mini-field strategy__ defines how state of each mini-field calculated and can be: __first__ OR __any__.

__R1.4.1__ According to __first__ strategy, as soon as first horizontal or vertial or diagonal line of 3 cells marked with same sign appears on mini-field, its state is considered as marked with the sign of those cells and doesn't change after that.

__R1.4.2__ According to __any__ strategy, state of mini-field is calculated using rules (from highest to lowest priority):
* marked with __?__ if it has horizontal or vertial or diagonal line of 3 cells marked with __X__ AND horizontal or vertial or diagonal line of 3 cells marked with __O__
* marked with __X__ if it has horizontal or vertial or diagonal line of 3 cells marked with __X__
* marked with __O__ if it has horizontal or vertial or diagonal line of 3 cells marked with __O__
* __empty__ otherwise

__R1.5__ Two players participate game. One uses __X__ to mark a cell, another uses __O__. Turn by turn players put their marks on cells.

__R1.6__ Player holding __X__ mark makes first turn.

__R1.7__ Player is not allowed to mark a cell that has a state other than __empty__.

__R1.8.1__ First turn does not limit which cells can be marked.

__R1.8.2__ Following turns limits cells allowed to be marked by mini-field with coordinates equal to coordinates of last marked cell inside its mini-field.

__R1.9.1__ When a horizontal or vertical or diagonal line of 3 mini-fields marked with same sign (__?__ is considered as both __X__ and __O__ signs) appears on the field, the game stops and player holding that sign wins.

__R1.9.2__ If at current turn player can't place it's sign then the games stops and noone wins (draw is considered).

## Main screen

__R2__ Main screen contains:

R | Item
--- | ---
__R2.1__ | "Start game" button
__R2.2__ | "Options" button
 
__R2.1__ When user presses "Start game" button, a game screen (__R3__) appers modally.

__R2.1__ When user presses "Options" button, an options screen (__R4__) appears modally.

## Game screen

__R3__ When game screen appears, the game starts. Game screens contains:

R | Item
--- | ---
__R3.1__ | "Exit" button
__R3.2__ | "It's ... turn" label
__R3.3__ | Game field
__R3.4__ | "Finish turn" button

__R3.1__ When user presses "Exit" button AND the game is not ended, a dialog appears modally:

R | Item
--- | ---
__R3.1.1__ | "Are you sure to exit game" label
__R3.1.2__ | "Yes" button
__R3.1.3__ | "Cancel" button

__R3.1.1__ Static label

__R3.1.2__ When user presses "Yes" button, dialog and game screen disappear.

__R3.1.3__ When user presses "Cancel" button or use hardware back button, dialog disappears.

__R3.2__ The label shows which player's turn is current: "It's X's turn" or "It's O's turn" according to __R1*__ rules. After the game stops label shows "Game over".

__R3.3__ Game field follows __R1*__ rules and contains:

R | Item
--- | ---
__R3.3.1__ | Seprators
__R3.3.2__ | Highlighted area
__R3.3.3__ | Line across mini-fields
__R3.3.4__ | Mini-fields

__R3.3.1__ Separators are lines between mini-fields.

__R3.3.2__ The area highlights mini-fields where mark can be placed in the current turn. After game ends the area disappears.

__R3.3.3__ After any player wins, the line appears and connects victorious row of mini-fields (__R1.9.1__).

__R3.3.4__ Each mini-field contains:

R | Item
--- | ---
__R3.3.4.1__ | Separators
__R3.3.4.2__ | Status mark
__R3.3.4.3__ | Line(s) across cells
__R3.3.4.4__ | Cells

__R3.3.4.1__ Separators are lines between cells.

__R3.3.4.2__ Status mark reflects current state of mini-field: it's empty OR displays __X__ OR displays __O__ OR displays __?__.

__R3.3.4.3__ The line(s) connect victorious row(s) of cells in a mini-field and depends on __R4.4__ option:

__R3.3.4.3.1__ If __first__ mini-field strategy is used: as soon as first horizontal or vertial or diagonal line of 3 cells marked with same sign appears on mini-field according to __R1.4.1__, the line appears and connect them.

__R3.3.4.3.2__ If __any__ mini-field strategy is used (__R1.4.2__): 

__R3.3.4.3.2.1__ As soon as first horizontal or vertial or diagonal line of 3 cells marked with __X__ appears on mini-field, a line appears and connects them.

__R3.3.4.3.2.2__ As soon as first horizontal or vertial or diagonal line of 3 cells marked with __O__ appears on mini-field, a line appears and connects them.

__R3.3.4.4__ Cells are 9 buttons placed in 3x3 grid:

__R3.3.4.4.1__ Cell displays it's current state: it's empty OR displays __X__ OR displays __O__.

__R3.3.4.4.2__ Button can't be pressed if:

__R3.3.4.4.2.1__ The game ended.

__R3.3.4.4.2.2__ Cell has a state other than __empty__.

__R3.3.4.4.2.2__ Mark can't be placed in it in the current turn.

__R3.3.4.4.3__ When user presses a button: see __R3.5.3__.

__R3.4__ The "Finish turn" button presents only if "Confirm turn" options is on (__R4.6__).

__R3.5__ Game logic follows __R1*__:

__R3.5.1__ Current turn and game end status is displayed via __R3.2__

__R3.5.2__ Current state of field is displayed via __R3.3__

__R3.5.3__ To make a turn:

__R3.5.3.1__ If "Confirm turn" options is off (__R4.6__) then player has to press a cell button, after that cell is marked with player's sign and player's turn is ended.

__R3.5.3.1__ If "Confirm turn" options is on (__R4.6__) then player has to press a cell button, after that cell is marked with player's sign. However player can press another empty cells any times, then previously pressed cell's state is reset to __empty__. To confirm his choice player needs to press __R3.4__, until that new __R3.3.3__ and __R3.3.4.3__ do not appear. 

__R3.5.4__ If after a turn game ends and any players wins then a dialog appears modally:

R | Item
--- | ---
__R3.5.4.1__ | "... won" label
__R3.5.4.2__ | "Close" button

__R3.5.4.1__ | The label shows a winner: "X won" or "O won".

__R3.5.4.2__ | When user presses "Close" or hardware back button, dialog dismisses.

__R3.5.5__ If after a turn game ends and noone wins then a dialog appears modally:

R | Item
--- | ---
__R3.5.5.1__ | "It's a draw" label
__R3.5.5.2__ | "Close" button

__R3.5.5.1__ | Static label.

__R3.5.5.2__ | When user presses "Close" or hardware back button, dialog dismisses.

## Options screen

__R4__ Options screen contains:

R | Item
--- | ---
__R4.1__ | "Back" button
__R4.2__ | "Options" label
__R4.3__ | "Save" button
__R4.4__ | Mini-field strategy picker
__R4.5__ | "Confirm turn" label
__R4.6__ | Switch

__R4.1__ When user presses "Back" or hardware back button, screen dismisses.

__R4.2__ Static label.

__R4.3__ When user presses "Save" button, app saves current option and screen dismisses.

__R4.4__ Picker is used to pick mini-field strategy (__R1.4__) and contain corresponding value: "First player with 3-in-line captures mini-field" and "Any player with 3-in-line captures mini-field" values. Default value: "First player with 3-in-line captures mini-field".

__R4.5__ Static label.

__R4.6__ Switch is used to confirm turns on the game screen (__R3.5.3__). Default value: off.
