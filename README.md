{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 67,
   "id": "4d7261b7",
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np\n",
    "\n",
    "def monte_carlo_option_pricing(S, K, T, r, sigma, num_paths):\n",
    "    dt = T / 252  # Assuming 252 trading days in a year\n",
    "    paths = np.zeros((num_paths, int(T / dt) + 1))\n",
    "    paths[:, 0] = S\n",
    "\n",
    "    for i in range(1, int(T / dt) + 1):\n",
    "        paths[:, i] = paths[:, i - 1] * np.exp((r - 0.5 * sigma**2) * dt + sigma * np.sqrt(dt) * np.random.normal(0, 1, num_paths))\n",
    "\n",
    "    option_payoffs = np.maximum(paths[:, -1] - K, 0)\n",
    "    option_price = np.exp(-r * T) * np.mean(option_payoffs)\n",
    "\n",
    "    return option_price\n",
    "\n",
    "# Example usage\n",
    "S0 = 21150  # Initial stock price\n",
    "K = 21100   # Strike price\n",
    "T = 4/252     # Time to expiration (in years)\n",
    "r = 0.0694  # Risk-free rate\n",
    "sigma = 0.0989  # Volatility\n",
    "num_paths = 10000"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 70,
   "id": "eab8dcd3",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Monte Carlo Call Option Price: 147.42373835522676\n"
     ]
    }
   ],
   "source": [
    "call_option_price = monte_carlo_option_pricing(S0, K, T, r, sigma, num_paths)\n",
    "print(\"Monte Carlo Call Option Price:\", call_option_price)\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.11.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
