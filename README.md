# ChessWeave
This repo is an SDK for evaluating the ChessWeave protocol. This functions similarly to SmartWeave, however is less extendable. ChessWeave can be combined with smartweave as it works purely in transaction tags.

## Tag's

Below are the descriptions of various actions that can be performed in a chess game and the corresponding Arweave transaction tag structure.

| Description         | App-Name | Game-ID |    Action   |  Move  |  White-Address       |  Black-Address       |
|---------------------|----------|---------|-------------|--------|----------------------|----------------------|
| Game Initialization | Chess    | [UID]   | Initialize  |  N/A   | [Creator or blank]   | [Creator or blank]   | 
| Join                | Chess    | [UID]   |    Join     |  N/A   | [Address or blank]   | [Address or blank]   |
| Move                | Chess    | [UID]   |    Move     |  SAN   |         N/A          |          N/A         |
| Resign              | Chess    | [UID]   |   Resign    |  N/A   |         N/A          |          N/A         |
| Draw Offer          | Chess    | [UID]   |  DrawOffer  |  N/A   |         N/A          |          N/A         |
| Draw Accepted       | Chess    | [UID]   |  DrawAccept |  N/A   |         N/A          |          N/A         |
| Draw Declined       | Chess    | [UID]   | DrawDecline |  N/A   |         N/A          |          N/A         |
| Game Termination    | Chess    | [UID]   |  Terminate  |  N/A   |         N/A          |          N/A         |

### Game Initialization

Initial transaction to start a new game on Arweave. This generates a game ID as a UUID, with the creators address being put in either black or white address tag.

### Join

Transaction to join an existing game by UID. Joins as whatever is the available color.

### Move

Transaction to perform a move in the game.

### Resign

Transaction to surrender/resign from the game.

### Draw Offer

This transaction is used to offer a draw to the opponent. It must be followed by either a 'Draw Accepted' or 'Draw Declined' transaction.

### Draw Accepted

This transaction is a response to the 'Draw Offer' transaction, indicating that the opponent agrees to end the game in a draw.

### Draw Declined

This transaction is a response to the 'Draw Offer' transaction, indicating that the opponent declines the offer and wishes to continue the game.

### Game Termination

Transaction to terminate the game, executable only by the games creator.

## ChessWeave Evaluation Software

The ChessWeave evaluation software utilizes the FEN (Forsyth-Edwards Notation) string to represent the game's current state. By default, the FEN string of the standard start position is the initial game state. The main purpose of the software is to validate the sequence of moves made in a chess game.

### Process Overview

1. The software initializes with the default FEN string representing the initial game state.
2. It fetches all transactions associated with the game in chronological order.
3. For each 'Move' action transaction, the software verifies if the move (represented in SAN - Standard Algebraic Notation) is legal for the current game state.
   - The validation is performed by simulating the move on the internal representation of the chess board.
   - If the move is legal (as per the rules of chess), the internal game state is updated to reflect the move, and the software proceeds to the next transaction.
   - If the move is not legal, the move is ignored, and the game state remains unchanged. The software then awaits the player's next move. If no legal move is made before the player's time runs out, the player is considered to have lost the game due to time overrun.

### Handling Other Transaction Types

Apart from the 'Move' actions, there are several other transaction types (like 'Resign', 'DrawOffer', etc.) that the software handles based on their specific semantics in the game of chess:

- **Resignation :** Upon detecting a 'Resign' transaction, the software immediately ends the game and declares the other player the winner.

- **Draw Offer :** A 'DrawOffer' transaction puts the game in a state where the other player can accept or decline the draw offer. The game remains in this state until a 'DrawAccept' or 'DrawDecline' transaction is encountered.

- **Draw Acceptance :** A 'DrawAccept' transaction, following a 'DrawOffer', ends the game immediately with the result recorded as a draw.

- **Draw Declination :** A 'DrawDecline' transaction, following a 'DrawOffer', allows the game to proceed normally.

This approach ensures that only legal moves, in accordance with the rules of chess, alter the game state. It enforces the rules of the game and upholds the integrity of the game as it unfolds on the Arweave blockchain.

> Note: The implementation of the evaluation software requires a nuanced understanding of chess rules and a comprehensive chess library to validate moves and manage game states.




URLs:
1. https://en.wikipedia.org/wiki/Algebraic_notation_(chess)
2. https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation


