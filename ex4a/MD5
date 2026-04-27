import math
def md5_full_trace(message):
    A0, B0, C0, D0 = 0x67452301, 0xefcdab89, 0x98badcfe, 0x10325476
    
    T = [int(4294967296 * abs(math.sin(i + 1))) & 0xFFFFFFFF for i in range(64)]
    S = [7, 12, 17, 22] * 4 + \
        [5,  9, 14, 20] * 4 + \
        [4, 11, 16, 23] * 4 + \
        [6, 10, 15, 21] * 4
    msg = bytearray(message, 'utf-8')
    orig_len_bits = (8 * len(msg)) & 0xffffffffffffffff
    msg.append(0x80)
    while len(msg) % 64 != 56:
        msg.append(0)
    msg += orig_len_bits.to_bytes(8, byteorder='little')

    for offset in range(0, len(msg), 64):
        block = msg[offset:offset + 64]
        M = [int.from_bytes(block[i:i+4], byteorder='little') for i in range(0, 64, 4)]
        
        A, B, C, D = A0, B0, C0, D0
        
        print(f"\n{'='*60}")
        print(f" PROCESSING BLOCK {offset//64 + 1}")
        print(f"{'='*60}")
        print(f"Initial State: A:{A:08x} B:{B:08x} C:{C:08x} D:{D:08x}")

        for i in range(64):
            if i < 16:
                f = (B & C) | (~B & D)
                g = i
                round_name = "ROUND 1 (F)"
            elif i < 32:
                f = (D & B) | (~D & C)
                g = (5 * i + 1) % 16
                round_name = "ROUND 2 (G)"
            elif i < 48:
                f = B ^ C ^ D
                g = (3 * i + 5) % 16
                round_name = "ROUND 3 (H)"
            else:
                f = C ^ (B | ~D)
                g = (7 * i) % 16
                round_name = "ROUND 4 (I)"

            sum_val = (A + f + T[i] + M[g]) & 0xFFFFFFFF
            rotated = ((sum_val << S[i]) | (sum_val >> (32 - S[i]))) & 0xFFFFFFFF
            A, B, C, D = D, (B + rotated) & 0xFFFFFFFF, B, C
            
            print(f"Step {i:02} [{round_name}] -> A:{A:08x} B:{B:08x} C:{C:08x} D:{D:08x}")

        A0 = (A0 + A) & 0xFFFFFFFF
        B0 = (B0 + B) & 0xFFFFFFFF
        C0 = (C0 + C) & 0xFFFFFFFF
        D0 = (D0 + D) & 0xFFFFFFFF
        print(f"\nBlock Accumulation: A:{A0:08x} B:{B0:08x} C:{C0:08x} D:{D0:08x}")
    final_hex = "".join([x.to_bytes(4, 'little').hex() for x in [A0, B0, C0, D0]])
    return final_hex
user_input = input("Enter text: ")
result = md5_full_trace(user_input)
print(f"\nFinal MD5 Hash: {result}")
