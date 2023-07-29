# ChessWeave
This repo is an SDK for evaluating the arweave chess-weave protocol. This functions similarly to SmartWeave, however is less extendable. ChessWeave can be combined with smartweave as it works purely in transaction tags.

Sure, below are the descriptions of various actions that can be performed in a chess game and the corresponding Arweave transaction tag structure.

| Chess-Action      | App-Name | GameID    | MoveNumber | Action     | Move | Player  |
|-------------------|-------------|-----------|------------|------------|------|---------|
| Game Initialization | Chess       | [unique game ID] | 0          | Initialize | N/A  | [White and Black player identifiers] |
| Normal Move        | Chess       | [unique game ID] | [Move Number] | Move   | [SAN of the move] | [player making the move] |
| Castling (kingside or queenside)  | Chess       | [unique game ID] | [Move Number] | Move   | [SAN of the move (O-O for kingside, O-O-O for queenside)] | [player making the move] |
| Capture           | Chess       | [unique game ID] | [Move Number] | Move   | [SAN of the move (x denotes capture)] | [player making the move] |
| Check             | Chess       | [unique game ID] | [Move Number] | Move   | [SAN of the move (+ denotes check)] | [player making the move] |
| Checkmate         | Chess       | [unique game ID] | [Move Number] | Move   | [SAN of the move (# denotes checkmate)] | [player making the move] |
| Player Resigns    | Chess       | [unique game ID] | [Move Number] | Resign | N/A  | [player resigning] |
| Draw Offer        | Chess       | [unique game ID] | [Move Number] | DrawOffer | N/A | [player offering draw] |
| Draw Accepted     | Chess       | [unique game ID] | [Move Number] | DrawAccept | N/A | [player accepting draw] |
| Draw Declined     | Chess       | [unique game ID] | [Move Number] | DrawDecline | N/A | [player declining draw] |
| Game Termination  | Chess       | [unique game ID] | [Move Number] | Terminate | N/A | [result of the game] |

Remember that the 'MoveNumber' and 'Move' tags would need to be incremented and updated with each move. For the 'Player' tag, use the identifier of the player making the move or performing the action.

This protocol allows for a full record of a chess game using Arweave transaction tags.

URLs:
1. https://en.wikipedia.org/wiki/Algebraic_notation_(chess)
2. https://docs.arweave.org/info/architecture

