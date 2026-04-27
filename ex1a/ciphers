class Cipher:
 def __init__(self):
 self.alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
 def _to_n(self, char):
 return ord(char.upper()) - 65
 def _to_c(self, n):
 return chr((n % 26) + 65)
 def _get_inverse(self, a, m=26):
 for x in range(1, m):
 if (a * x) % m == 1:
 return x
 return None
 def shift_cipher(self, text, key, encrypt=True):
 mode = "Encryption" if encrypt else "Decryption"
 print(f"\n--- Shift Cipher {mode} (K={key}) ---")
 result = ""
 actual_key = key if encrypt else -key
 for char in text.upper():
 if char in self.alphabet:
 p_n = self._to_n(char)
 res_n = (p_n + actual_key) % 26
 char_res = self._to_c(res_n)
 op = '+' if encrypt else '-'
 print(f"{char}({p_n}) {op} {key} = {res_n} ({char_res})")
 result += char_res
 print(f"Result: {result}")
 return result
 def vigenere_cipher(self, text, key, encrypt=True):
 mode = "Encryption" if encrypt else "Decryption"
 print(f"\n--- Vigenere Cipher {mode} (Key='{key}') ---")
 result = ""
 key = key.upper()
 for i, char in enumerate(text.upper()):
 if char in self.alphabet:
 p_n = self._to_n(char)
 k_char = key[i % len(key)]
 k_n = self._to_n(k_char)
 res_n = (p_n + k_n) % 26 if encrypt else (p_n - k_n) % 26
 char_res = self._to_c(res_n)
 op = '+' if encrypt else '-'
 print(f"Pos {i}: {char}({p_n}) {op} {k_char}({k_n}) = {res_n} ({char_res})")
 result += char_res
 print(f"Result: {result}")
 return result
 def hill_cipher(self, text, matrix, encrypt=True):
 mode = "Encryption" if encrypt else "Decryption"
 print(f"\n--- Hill Cipher {mode} ---")
 text = text.upper().replace(" ", "")
 if encrypt and len(text) % 2 != 0:
 text += "X"
 print("Padding 'X' added to make length even.")
 m = matrix
 if not encrypt:
 # Determinant = (ad - bc) mod 26
 det = (m[0][0] * m[1][1] - m[0][1] * m[1][0]) % 26
 inv_det = self._get_inverse(det)
 if inv_det is None:
 print(f"Error: Matrix determinant ({det}) has no inverse mod 26.")
 return None
 # Inverse Matrix = inv_det * [[d, -b], [-c, a]] mod 26
 m = [
 [(matrix[1][1] * inv_det) % 26, (-matrix[0][1] * inv_det) % 26],
 [(-matrix[1][0] * inv_det) % 26, (matrix[0][0] * inv_det) % 26]
 ]
 print(f"Calculated Decryption Matrix: {m}")
 result = ""
 for i in range(0, len(text), 2):
 p1, p2 = self._to_n(text[i]), self._to_n(text[i+1])
 c1 = (m[0][0] * p1 + m[0][1] * p2) % 26
 c2 = (m[1][0] * p1 + m[1][1] * p2) % 26
 r1, r2 = self._to_c(c1), self._to_c(c2)
 print(f"[{text[i]}{text[i+1]}] -> ({m[0][0]}*{p1} + {m[0][1]}*{p2}) mod 26 = {c1}({r1}) | "
 f"({m[1][0]}*{p1} + {m[1][1]}*{p2}) mod 26 = {c2}({r2})")
 result += r1 + r2
 print(f"Result: {result}")
 return result
c = CipherSuite()
msg = "HELLOWORLD"
enc_s = c.shift_cipher(msg, 11, encrypt=True)
dec_s = c.shift_cipher(enc_s, 11, encrypt=False)
enc_v = c.vigenere_cipher(msg, "KEY", encrypt=True)
dec_v = c.vigenere_cipher(enc_v, "KEY", encrypt=False)
# Hill Demo
mat = [[3, 3], [2, 5]]
enc_h = c.hill_cipher(msg, mat, encrypt=True)
dec_h = c.hill_cipher(enc_h, mat, encrypt=False
