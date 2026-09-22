
[[C++ Basic]]

`UObject` → base of every UE class, GC'd, not placeable in a level
`AActor` → UObject that can be placed / spawned in a level

	AActor
	↳ APawn → possessable, receives input
		↳ ACharacter → Pawn + capsule + CharacterMovement
	↳ AController
		↳ APlayerController → possesses a Pawn, owns input & UI
		↳ AAIController
	↳ AInfo → no transform
		↳ AGameModeBase → rules, server only, spawns players
		↳ AGameStateBase → match state replicated to all clients
		↳ APlayerState → per-player state (score, name), replicated

Per match: GameMode (server only) → GameState (all clients)
Per player: PlayerController → Pawn / Character, + PlayerState
