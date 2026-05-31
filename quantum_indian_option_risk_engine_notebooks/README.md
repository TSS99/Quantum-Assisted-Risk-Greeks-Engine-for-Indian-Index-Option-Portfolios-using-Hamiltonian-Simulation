# Quantum Assisted Risk and Greeks Engine for Indian Index Option Portfolios using Non-Hermitian Hamiltonian Simulation

This is a notebook-only research project that connects non-Hermitian quantum Hamiltonian simulation of Black-Scholes dynamics with industry-facing risk outputs for Indian index option portfolios. The project is intentionally framed as a feasibility and benchmarking study, not as a claim of quantum advantage or a production trading system.

## Motivation

Most quantum finance examples stop at pricing one European option. Industry risk desks care about portfolios, Greeks, stress P&L, volatility sensitivity, VaR, Expected Shortfall, data quality, calibration, reproducibility, and limitations. This repository builds a complete research workflow around those outputs while keeping every line of implementation code inside Jupyter notebooks.

## Indian Index Option Context

The workflow focuses on NIFTY 50 and Bank NIFTY index options, with FINNIFTY as an optional extension. Listed Indian index options are treated here as European-style at expiry. Black-Scholes is the baseline model, with synthetic Indian-style option chains and optional user-provided NSE-style CSV inputs. Synthetic data is clearly labeled and should not be interpreted as live market data.

## Mathematical Background

The baseline Black-Scholes PDE is

```text
partial V / partial t + r S partial V / partial S + 1/2 sigma^2 S^2 partial^2 V / partial S^2 = r V.
```

Using `S = exp(x)`, time reversal `tau = T - t`, and momentum operator `p_hat = -i partial/partial x`, the notebook workflow studies the non-Hermitian Black-Scholes Hamiltonian

```text
H_BS = i sigma^2/2 p_hat^2 - (sigma^2/2 - r) p_hat + i r I.
```

For constant volatility, the Hermitian and anti-Hermitian diagonal momentum-space components commute. The workflow uses QFT-style momentum-space diagonalization, non-unitary evolution through one-ancilla unitary dilation, ancilla post-selection, and reconstruction of price curves and Greeks.

## Why This Is Not Just Toy Pricing

The notebooks include classical validation, NSE-style data cleaning, synthetic Indian option-chain generation, portfolio construction, finite-difference PDE benchmarking, stress testing, Monte Carlo P&L simulation, VaR, Expected Shortfall, volatility-surface interpolation, local-volatility discussion, quantum price reconstruction, quantum Greeks reconstruction, portfolio-level quantum-versus-classical error analysis, boundary duplication studies, post-selection probability studies, and resource scaling through 40 grid qubits.

## Notebook Structure

Run notebooks in numerical order from `notebooks/00_project_setup_and_shared_functions.ipynb` through `notebooks/20_final_research_summary.ipynb`. Shared functions live only in notebook `00`; every later notebook reuses it with:

```python
%run 00_project_setup_and_shared_functions.ipynb
```

## Installation

Use Python 3.10 or newer.

```bash
cd quantum_indian_option_risk_engine_notebooks
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

Qiskit is used only for a small optional circuit prototype. The core classical and matrix/statevector quantum notebooks are designed to run even when Qiskit-specific functionality is unavailable.

## Data Modes

1. **Real CSV input mode:** place NSE-style option-chain CSV files in `data/raw`. Expected columns may include `symbol`, `expiry`, `strike`, `option_type`, `underlying_price`, `last_price`, `bid`, `ask`, `implied_volatility`, `open_interest`, `volume`, and `timestamp`. Missing optional columns are handled gracefully.
2. **Synthetic Indian market mode:** notebooks generate realistic but synthetic NIFTY and Bank NIFTY option chains with smile-like IV, bid-ask spread, volume, and open interest.
3. **Manual config mode:** edit `config/sample_portfolio.yaml` to specify a portfolio directly.

## Reproducing Figures And Tables

Notebook outputs are written to:

- `results/figures`
- `results/tables`
- `results/reports`
- `results/notebook_outputs`

Notebook `19_paper_figures_and_tables.ipynb` collects publication-style figures and tables, while notebook `20_final_research_summary.ipynb` summarizes the research workflow and generated outputs.

## Interpreting Results

The main quantities are price RMSE, maximum absolute error, relative error, ATM/ITM/OTM error, Greeks RMSE, post-selection probability, portfolio value error, portfolio Greeks error, stress P&L error, VaR error, Expected Shortfall error, runtime estimates, memory estimates, qubit counts, grid point counts, QFT gate estimates, and small-circuit depth estimates.

## Limitations

No quantum advantage is claimed. Black-Scholes constant volatility is only a baseline. State preparation can dominate costs. Large statevector simulation requires enormous memory. A 40-qubit statevector is estimated, not allocated. Real hardware implementation is limited by circuit depth, noise, and state-preparation overhead. Finance usefulness depends on market calibration and careful benchmarking; European option pricing alone is not enough for industry relevance.

## Publication Plan

The intended framing is suitable for venues such as IEEE Quantum Week / IEEE QCE, IEEE Transactions on Quantum Engineering, Quantum Information Processing, EPJ Quantum Technology, and, with stronger finance benchmarking, Journal of Computational Finance. The strongest claim is that this is a reproducible notebook workflow connecting non-Hermitian quantum Hamiltonian simulation to portfolio Greeks, stress P&L, VaR, and Expected Shortfall for Indian index option portfolios.
