Battery
=======

.. automodule:: components.battery
   :noindex:

.. autoclass:: components.battery.Battery
   :members:
   :undoc-members:
   :inherited-members:
   :show-inheritance:
   :member-order: bysource

.. _battery-attributes:

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

.. _battery-usage:

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

.. _battery-dynamics:

Battery Dynamics
----------------

The **DeterministicBattery** class models predictable charging and discharging 
behavior of a battery, applying fixed efficiencies and handling natural decay.
This class is a subclass of ``ModelBasedDynamics`` and provides deterministic
energy state updates for a battery in the smart grid simulation.

**Key responsibilities:**
- Apply charge and discharge efficiencies.
- Enforce min/max energy limits.
- Ensure charging/discharging rates do not exceed configured maximums.
- Allow modeling of exponential decay losses via the ``exp_mult`` method.

Initialization
~~~~~~~~~~~~~~
The constructor requires a ``model_parameters`` dictionary containing:

- ``charge_efficiency`` (*float*): Efficiency for charging (0 < value ≤ 1).
- ``discharge_efficiency`` (*float*): Efficiency for discharging (0 < value ≤ 1).
- ``lifetime_constant`` (*float*): Constant for decay rate (> 0).

Example:
^^^^^^^^
.. code-block:: python

    from dynamics.battery_dynamics_det import DeterministicBattery

    params = {
        "charge_efficiency": 0.95,
        "discharge_efficiency": 0.9,
        "lifetime_constant": 1000
    }
    dynamics = DeterministicBattery(params)

Methods
~~~~~~~
**get_value(**\*\*kwargs\*\*)  
    Calculates new energy level based on action, current state, and constraints.

**exp_mult(x, lifetime_constant, current_time_step)**  
    Applies exponential decay to a given value.

Example Usage
^^^^^^^^^^^^^
.. code-block:: python

    new_energy = dynamics.get_value(
        time=0.5,
        action=2.0,
        current_energy=50.0,
        min_energy=10.0,
        max_energy=100.0,
        charge_rate_max=5.0,
        discharge_rate_max=5.0
    )

    decayed_value = DeterministicBattery.exp_mult(
        x=100.0,
        lifetime_constant=1000,
        current_time_step=10
    )
