import math
def check_prime(n):
 if n <= 1:
 print(f"{n} is not prime.")
 return False
 limit = int(math.sqrt(n))
 print(f"--- Primality Test ---")
 print(f"Checking {n}. Testing divisors up to sqrt({n}) ≈ {limit}:")
 for i in range(2, limit + 1):
 if n % i == 0:
 print(f"Step: {n} is divisible by {i}. (Not Prime)")
 return False
 print(f"Step: {n} is not divisible by {i}")
 print(f"Result: {n} is PRIME!\n")
 return True
def get_gcd(a, b):
 """Calculates the Greatest Common Divisor using the Euclidean Algorithm."""
 a_orig, b_orig = a, b
 a, b = abs(a), abs(b)
 print(f"--- GCD Calculation ---")
 print(f"Finding GCD of {a} and {b}:")
 step = 1
 while b != 0:
 print(f"Step {step}: {a} = ({a // b} * {b}) + {a % b}")
 a, b = b, a % b
 step += 1
 print(f"Final GCD: {a}\n")
 return a
def get_lcm(a, b):
 """Calculates the Least Common Multiple using the GCD property."""
 print(f"--- LCM Calculation ---")
 gcd_val = get_gcd(a, b)
 lcm = abs(a * b) // gcd_val
 print(f"Calculation: (|{a} * {b}|) / {gcd_val} = {lcm}")
 print(f"Final LCM: {lcm}\n")
 return lcm
check_prime(29)
get_gcd(48, 18)
get_lcm(12, 15)
