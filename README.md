# vcvd2024_Kankainen
Alpo Kankainen
2400438002


import numpy as np
import matplotlib.pyplot as plt
import argparse

def magic_formula(kappa, D=1.0):
    return D * np.sin(1.9 * np.arctan(10 * kappa - 0.97 * (10 * kappa - np.arctan(10 * kappa))))

def compute_forces(kappa, alpha, weight, mu):
    Fz = weight / 4
    force = Fz * magic_formula(kappa, D=mu)
    return force, force * np.sin(np.radians(alpha))

def plot_forces(kappa, braking, side, alpha):
    plt.plot(kappa, braking, label='Braking Force')
    plt.plot(kappa, side, label=f'Side Force (α={alpha}°)')
    plt.xlabel('Slip (κ)')
    plt.ylabel('Force (N)')
    plt.legend()
    plt.grid()
    plt.show()

def main():
    args = argparse.ArgumentParser()
    args.add_argument("--slip", type=float, default=5)
    args.add_argument("--weight", type=float, default=1500)
    args.add_argument("--mu", type=float, default=0.8)
    args.add_argument("--alpha", type=float, default=0)
    a = args.parse_args()
    
    kappa = np.linspace(0, a.slip / 100, 100)
    braking, side = compute_forces(kappa, a.alpha, a.weight, a.mu)
    plot_forces(kappa, braking, side, a.alpha)

if __name__ == "__main__":
    main()
