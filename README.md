# ChessWeave
This repo is an SDK for evaluating the arweave chess-weave protocol. This functions similarly to SmartWeave, however is less extendable. ChessWeave can be combined with smartweave as it works purely in transaction tags.

Below are the descriptions of various actions that can be performed in a chess game and the corresponding Arweave transaction tag structure.

| Chess-Action        | App-Name | GameID |    Action   |    Move    | Player Address  |
|---------------------|----------|--------|-------------|------------|-----------------|
| Game Initialization | Chess    | [UID]  | Initialize  | N/A        | [White and Black player identifiers] |
| Normal Move         | Chess    | [UID]  |    Move     | SAN        | [player making the move] |
| Castling            | Chess    | [UID]  |    Move     | [SAN of the move (O-O for kingside, O-O-O for queenside)] | [player making the move] |
| Capture             | Chess    | [UID]  |    Move     | [SAN of the move (x denotes capture)] | [player making the move] |
| Check               | Chess    | [UID]  |    Move     | [SAN of the move (+ denotes check)] | [player making the move] |
| Checkmate           | Chess    | [UID]  |    Move     | [SAN of the move (# denotes checkmate)] | [player making the move] |
| Player Resigns      | Chess    | [UID]  |   Resign    | N/A        | [player resigning] |
| Draw Offer          | Chess    | [UID]  |  DrawOffer  | N/A        | [player offering draw] |
| Draw Accepted       | Chess    | [UID]  |  DrawAccept | N/A        | [player accepting draw] |
| Draw Declined       | Chess    | [UID]  | DrawDecline | N/A        | [player declining draw] |
| Game Termination    | Chess    | [UID]  |  Terminate  | N/A        | [result of the game] |



URLs:
1. https://en.wikipedia.org/wiki/Algebraic_notation_(chess)


