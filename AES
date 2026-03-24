import sys
def print_state(label, state):
 print(f"{label}:")
 for row in state:
 print(" " + " ".join(f"{b:02x}" for b in row))
def sub_bytes(state):
 for r in range(4):
 for c in range(4):
 state[r][c] = S_BOX[state[r][c]]
def shift_rows(state):
 state[1] = state[1][1:] + state[1][:1]
 state[2] = state[2][2:] + state[2][:2]
 state[3] = state[3][3:] + state[3][:3]
def xtime(a):
 return ((a << 1) ^ 0x1B) & 0xFF if (a & 0x80) else (a << 1) & 0xFF
def mix_columns(state):
 for c in range(4):
 s0, s1, s2, s3 = state[0][c], state[1][c], state[2][c], state[3][c]
 state[0][c] = xtime(s0) ^ (xtime(s1) ^ s1) ^ s2 ^ s3
 state[1][c] = s0 ^ xtime(s1) ^ (xtime(s2) ^ s2) ^ s3
 state[2][c] = s0 ^ s1 ^ xtime(s2) ^ (xtime(s3) ^ s3)
 state[3][c] = (xtime(s0) ^ s0) ^ s1 ^ s2 ^ xtime(s3)
def add_round_key(state, key_schedule, round_num):
 for c in range(4):
 for r in range(4):
 state[r][c] ^= key_schedule[round_num * 4 + c][r]
def aes_encrypt(plaintext, key):
 # Convert input strings to 4x4 matrices
 state = [[0]*4 for _ in range(4)]
 key_matrix = [[0]*4 for _ in range(4)
 p_bytes = [ord(c) for c in plaintext.ljust(16)[:16]]
 k_bytes = [ord(c) for c in key.ljust(16)[:16]]
 for i in range(16):
 state[i%4][i//4] = p_bytes[i]
 key_matrix[i%4][i//4] = k_bytes[i]
 key_schedule = [ [key_matrix[r][c] for r in range(4)] for c in range(4) ] * 11
 print("\n--- AES-128 ENCRYPTION START ---")
 print_state("Initial State", state)
 add_round_key(state, key_schedule, 0)
 print_state("After Initial AddRoundKey", state)
 for i in range(1, 10):
 print(f"\n--- Round {i} ---")
 sub_bytes(state)
 shift_rows(state)
 mix_columns(state)
 add_round_key(state, key_schedule, i)
 print_state("End of Round", state)
 print("\n--- Final Round (No MixColumns) ---")
 sub_bytes(state)
 shift_rows(state)
 add_round_key(state, key_schedule, 10)
 print_state("Ciphertext State", state)
 cipher_hex = "".join(f"{state[r][c]:02x}" for c in range(4) for r in range(4))
 print(f"\nFinal Ciphertext (Hex): {cipher_hex}")
print("AES-128 Encryption Tool (16-char max)")
user_pt = input("Enter Plaintext (16 chars): ")
user_key = input("Enter Key (16 chars): ")
aes_encrypt(user_pt, user_key)
