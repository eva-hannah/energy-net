Battery API
===========

.. automodule:: components.battery
   :noindex:

.. autoclass:: components.battery.Battery
   :members:
   :undoc-members:
   :inherited-members:
   :show-inheritance:
   :member-order: bysource

Attributes
----------

.. rubric:: Key attributes

- ``energy_min`` (float): Minimum allowable energy (MWh).
- ``energy_max`` (float): Maximum allowable energy (MWh).
- ``charge_rate_max`` (float): Max charging power (MW).
- ``discharge_rate_max`` (float): Max discharging power (MW).
- ``charge_efficiency`` (float): Charging efficiency (0–1).
- ``discharge_efficiency`` (float): Discharging efficiency (0–1).
- ``initial_energy`` (float): Initial energy level (MWh).
- ``energy_level`` (float): Current energy level (MWh).
- ``energy_change`` (float): Delta since last action (MWh).

Usage
-----

Minimal example::

    from energy_net.energy_dynamics import EnergyDynamics
    from components.battery import Battery

    dyn = EnergyDynamics(...)          # provide your dynamics impl
    cfg = {
        "min": 0.0,
        "max": 100.0,
        "charge_rate_max": 20.0,
        "discharge_rate_max": 20.0,
        "charge_efficiency": 0.95,
        "discharge_efficiency": 0.95,
        "init": 50.0,
    }

    bat = Battery(dynamics=dyn, config=cfg)
    bat.update(time=0.25, action=10.0)  # charge at 10 MW
    level = bat.get_state()             # current MWh
