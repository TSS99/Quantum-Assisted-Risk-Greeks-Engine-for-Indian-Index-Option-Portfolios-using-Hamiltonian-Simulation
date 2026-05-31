# Methods Notes

The Black-Scholes PDE is transformed with `S = exp(x)` and `tau = T - t`, giving a forward-time evolution in log-price. With `p_hat = -i partial/partial x`, the Hamiltonian is `H_BS = i sigma^2/2 p_hat^2 - (sigma^2/2 - r) p_hat + i r I`. The Hermitian component is `-(sigma^2/2 - r) p_hat`; the anti-Hermitian component is `i(sigma^2 p_hat^2/2 + r I)`. Under constant volatility these diagonal momentum-space terms commute.

The QFT-style transform moves the payoff state into momentum space. The Hermitian part contributes a phase, while the anti-Hermitian part contributes a diagonal contraction. A one-ancilla unitary dilation embeds a diagonal non-unitary operator `O` using the block matrix `[O, sqrt(I-O^2); sqrt(I-O^2), -O]` after safe scaling when needed. Ancilla post-selection on `0` recovers the contracted branch, and the notebook tracks post-selection probability and reconstruction scale.

Price curves are reconstructed by inverse QFT and payoff-normalization rescaling. Greeks are computed from reconstructed curves and finite differences across volatility, maturity, and rate perturbations. Portfolio risk metrics aggregate position-level prices and Greeks, run deterministic stress scenarios, and estimate Monte Carlo P&L, VaR, and Expected Shortfall.
