
# Industry-Style Risk Report

Synthetic examples only; not live market data.

## Portfolio Value

- Classical theoretical value: -4352.13
- Market value from sample inputs: 17400.00
- Model P&L: -21752.13
- Quantum reconstructed value: -1282.23
- Quantum minus classical value error: 3069.89

## Portfolio Greeks

- Delta: -24.7217
- Gamma: 0.031996
- Vega: 85983.05
- Theta: -527702.20
- Rho: 44012.36

## Tail Risk

- VaR 95: 34520.77
- ES 95: 41632.70
- VaR 99: 46083.87
- ES 99: 52790.51

## Largest Loss Scenarios

```text
      scenario          pnl
 time_decay_7d -9493.155214
 time_decay_3d -4251.156656
 vol_abs_-2.0% -1689.186105
 time_decay_1d -1440.928139
vol_rel_-10.0%  -981.451550
```

## Largest Vega Contributors

```text
                      label underlying option_type  strike  position_Vega
     NIFTY_ATM_LONG_PUT_30D      NIFTY         put 24000.0  204157.215276
BANKNIFTY_ITM_SHORT_PUT_60D  BANKNIFTY         put 54000.0 -163849.934826
BANKNIFTY_ATM_LONG_CALL_14D  BANKNIFTY        call 52000.0  121501.888437
   NIFTY_OTM_SHORT_CALL_30D      NIFTY        call 25000.0 -112959.918095
      NIFTY_OTM_LONG_PUT_7D      NIFTY         put 23000.0   37133.802461
```

## Limitations

This report is a research artifact. It does not claim quantum advantage, trading readiness, or live-market calibration.
