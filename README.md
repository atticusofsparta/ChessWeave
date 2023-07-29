# ChessWeave
This repo is an SDK for evaluating the arweave chess-weave protocol. This functions similarly to SmartWeave, however is less extendable. ChessWeave can be combined with smartweave as it works purely in transaction tags.

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


URLs:
1. https://en.wikipedia.org/wiki/Algebraic_notation_(chess)


