# ChessWeave
This repo is an SDK for evaluating the arweave chess-weave protocol. This functions similarly to SmartWeave, however is less extendable. ChessWeave can be combined with smartweave as it works purely in transaction tags.

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

## Evaluator Software
The evaluation software for ChessWeave uses the FEN (Forsyth-Edwards Notation) string representation of the game's current state. The FEN string of the standard start position is the default state. This software essentially validates the sequence of moves made in a game of chess.

The process works as follows:

The software starts with the initial game state as represented by the default FEN string.

It fetches all transactions associated with the game in chronological order.

For each transaction with the 'Action' tag set to 'Move', it checks if the 'Move' tag (which should contain a move in SAN - Standard Algebraic Notation) represents a legal move in the current game state.

To perform this validation, the software simulates the move on the internal representation of the chess board. If the move is legal (according to the rules of chess), the internal game state is updated to reflect the move, and the software proceeds to the next transaction.

If the move is not legal, the move is ignored and does not update the game state. The software then waits for the player's next move. If the player's move time runs out without a legal move being made, the player may be declared to have lost the game due to exceeding the time limit.

Other types of transactions (like 'Resign', 'DrawOffer', etc.) are handled based on their specific semantics in the game of chess.

This approach ensures that only legal moves, as per the rules of chess, can alter the game state. It enforces the game rules and maintains the integrity of the game as it's played out on the Arweave blockchain.

Please note that the implementation of the evaluation software requires a sophisticated understanding of chess rules and a comprehensive chess library to validate moves and manage game states.



URLs:
1. https://en.wikipedia.org/wiki/Algebraic_notation_(chess)
2. https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation


