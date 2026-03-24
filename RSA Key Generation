import math
def is_prime(n):
    if n < 2: return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0: return False
    return True

def get_gcd(a, b):
    while b:
        a, b = b, a % b
    return a

def mod_inverse(e, phi):
    """Extended Euclidean Algorithm to find d where (e * d) % phi == 1"""
    old_r, r = e, phi
    old_s, s = 1, 0
    while r != 0:
        quotient = old_r // r
        old_r, r = r, old_r - quotient * r
        old_s, s = s, old_s - quotient * s
    return (old_s % phi + phi) % phi

def run_rsa(p, q, msg):

    if not (is_prime(p) and is_prime(q)):
        return "Both p and q must be prime."
    if p == q:
        return "p and q must be different."

    n = p * q
    phi = (p - 1) * (q - 1)
    
    if not (0 < msg < n):
        return f"Message must be between 1 and {n-1}"

    e = 3
    while e < phi:
        if get_gcd(e, phi) == 1:
            break
        e += 2
    else:
        return "Could not find a valid e."

    d = mod_inverse(e, phi)
    ciphertext = pow(msg, e, n)
    decrypted_msg = pow(ciphertext, d, n)

    print(f"--- RSA Parameters ---")
    print(f"Primes: p={p}, q={q}")
    print(f"n (p*q): {n}")
    print(f"phi (p-1)*(q-1): {phi}")
    print(f"Public Key (e, n): ({e}, {n})")
    print(f"Private Key (d, n): ({d}, {n})\n")

    print(f"--- Process ---")
    print(f"Original Message: {msg}")
    print(f"Encrypted (Ciphertext): {ciphertext}")
    print(f"Decrypted Message: {decrypted_msg}")
    
    if msg == decrypted_msg:
        print("\nSuccess: Message recovered correctly! ✅")
            
run_rsa(p=61, q=53, msg=65)
