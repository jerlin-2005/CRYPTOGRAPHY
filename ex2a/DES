def permute(bits, table):
 return "".join(bits[i - 1] for i in table)
def left_shift(bits, count):
 return bits[count:] + bits[:count]
def xor(bits1, bits2):
 return "".join('0' if b1 == b2 else '1' for b1, b2 in zip(bits1, bits2))
def sbox(bits, box):
 row = int(bits[0] + bits[3], 2)
 col = int(bits[1] + bits[2], 2)
 return format(box[row][col], '02b')
def f_k(bits, key):
 L, R = bits[:4], bits[4:]
 # Expansion
 ep_r = permute(R, EP)
 # XOR with Key
 xor_res = xor(ep_r, key)
 # S-Boxes
 s_res = sbox(xor_res[:4], S0) + sbox(xor_res[4:], S1)
 # P4 Permutation
 p4_res = permute(s_res, P4)
 # XOR with Left Half
 return xor(p4_res, L) + R
def generate_keys(key_10bit):
 print(f"\n--- Key Generation (Input: {key_10bit}) ---")
 p10_res = permute(key_10bit, P10)
 L, R = p10_res[:5], p10_res[5:]
 L1, R1 = left_shift(L, 1), left_shift(R, 1)
 K1 = permute(L1 + R1, P8)
 print(f"Subkey K1: {K1}")
 L2, R2 = left_shift(L1, 2), left_shift(R1, 2)
 K2 = permute(L2 + R2, P8)
 print(f"Subkey K2: {K2}")
 return K1, K2
def s_des(bits, k1, k2, mode="Encryption"):
 print(f"\n--- {mode} (Input: {bits}) ---")
 ip_res = permute(bits, IP)
 print(f"Initial Permutation: {ip_res}")
 r1 = f_k(ip_res, k1)
 print(f"After Round 1: {r1}")
 sw = r1[4:] + r1[:4]
 print(f"After Swap: {sw}")
 r2 = f_k(sw, k2)
 print(f"After Round 2: {r2}")
 result = permute(r2, IP_INV)
 print(f"Final Result: {result}")
 return result
print("Simplified DES (8-bit Input, 10-bit Key)")
pt = input("Enter 8-bit Plaintext (e.g., 10101010): ")
key = input("Enter 10-bit Key (e.g., 0000011011): ")
k1, k2 = generate_keys(key)
cipher = s_des(pt, k1, k2, "Encryption")
plain = s_des(cipher, k2, k1, "Decryption") 
Simplified DES (8-bit Input, 10-bit Key)
