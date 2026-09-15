# Energy Calculator

**TESTED** · [Live demo](https://yasar101.github.io/software-engineering-portfolio/demos/energy-calculator.html) · [Portfolio](https://github.com/Yasar101/software-engineering-portfolio)

A pure calculation of electricity use, cost and estimated carbon emissions.

## Purpose and engineering skills

Keep domain units, input checks and rounding policy explicit.

## Structure

energy.py exposes estimate_energy and the immutable EnergyEstimate result. [Source](energy.py).

## Run

From this directory with Python 3.11+, run this offline example using `python3` (no dependencies or credentials):

```python
from decimal import Decimal
from energy import estimate_energy
result = estimate_energy(Decimal("1000"), Decimal("2"), 30, Decimal("0.30"))
assert result.cost == Decimal("18.00")
print(result)
```

## Test

```sh
python3 -m compileall -q .
python3 - <<'PY'
from decimal import Decimal
from energy import estimate_energy
result = estimate_energy(Decimal("1000"), Decimal("2"), 30, Decimal("0.30"))
assert result.kwh == Decimal("60.000")
assert result.cost == Decimal("18.00")
try:
    estimate_energy(Decimal("1"), Decimal("25"), 1, Decimal("1"))
except ValueError:
    print("impossible hours rejected")
PY
```

The full regression suite (failure paths, README examples and demo checks) runs in the [portfolio repository](https://github.com/Yasar101/software-engineering-portfolio).

## Complete and remaining

**Complete:** Decimal calculations, non-negative-input checks, daily-hour bounds and explicit output rounding.

**Remaining / limitations:** An estimate, not a billing or emissions authority. No UI; caller supplies appropriate tariff/intensity. The default intensity is illustrative, not live-sourced.

## Learning takeaway

Units and rounding choices belong in the domain contract, not just display code.

## Command-line demonstration
Run a transparent local estimate (this is an estimate from supplied values, not a supplier integration):

```bash
python3 -m energy --watts 850 --hours 3.5 --days 30 --tariff 0.28
```