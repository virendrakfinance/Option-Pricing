import numpy as np

def monte_carlo_option_pricing(S, K, T, r, sigma, num_paths):
    dt = T / 252  # Assuming 252 trading days in a year
    paths = np.zeros((num_paths, int(T / dt) + 1))
    paths[:, 0] = S

    for i in range(1, int(T / dt) + 1):
        paths[:, i] = paths[:, i - 1] * np.exp((r - 0.5 * sigma**2) * dt + sigma * np.sqrt(dt) * np.random.normal(0, 1, num_paths))

    option_payoffs = np.maximum(paths[:, -1] - K, 0)
    option_price = np.exp(-r * T) * np.mean(option_payoffs)

    return option_price

# Example usage
S0 = 21150  # Initial stock price
K = 21100   # Strike price
T = 4/252     # Time to expiration (in years)
r = 0.0694  # Risk-free rate
sigma = 0.0989  # Volatility
num_paths = 10000
call_option_price = monte_carlo_option_pricing(S0, K, T, r, sigma, num_paths)
print("Monte Carlo Call Option Price:", call_option_price)
Monte Carlo Call Option Price: 147.42373835522676
