# Rock_Paper_Scissors

def player(prev_play, opponent_history=[]):
    # Keep track of opponent's moves
    if prev_play:
        opponent_history.append(prev_play)

    # Default to Rock for first few moves
    if len(opponent_history) < 5:
        return "R"

    # Build a sequence of last 3 moves
    last_3 = "".join(opponent_history[-3:])
    plays = ["R", "P", "S"]
    defeats = {"R": "P", "P": "S", "S": "R"}

    # Count occurrences of 3-move sequences
    guess = "R"
    sequence_counts = {}

    for i in range(len(opponent_history) - 3):
        seq = "".join(opponent_history[i:i+3])
        next_move = opponent_history[i+3]
        if seq not in sequence_counts:
            sequence_counts[seq] = {"R": 0, "P": 0, "S": 0}
        sequence_counts[seq][next_move] += 1

    if last_3 in sequence_counts:
        most_likely = max(sequence_counts[last_3], key=sequence_counts[last_3].get)
        guess = defeats[most_likely]

    return guess
