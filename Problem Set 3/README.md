# Scrabble-like Word Game with Wildcards

A complete word game where players form words from dealt letter hands for points. Features wildcard support, hand substitution, and multi-hand game orchestration using dictionary-based hand management.

## Implementation

- `get_word_score()` — two-component scoring formula: sum of letter values multiplied by max(word-length-based bonus, 1)
- `deal_hand()` — deals random letters with a guaranteed vowel ratio, modified to include one wildcard `*` replacing a vowel slot
- `update_hand()` — returns a new hand dictionary with used letters removed, without mutating the original
- `is_valid_word()` — validates words against both the word list and the current hand. Handles the wildcard `*` by trying all 5 vowel substitutions
- `play_hand()` — interactive loop for playing a single hand, tracking score and remaining letters
- `substitute_hand()` — allows replacing one letter in the hand with a random unused letter (one-time use per game)
- `play_game()` — multi-hand game orchestrator with substitute and replay options

The wildcard `*` is added to `SCRABBLE_LETTER_VALUES` with a value of 0.
