Environment Registration
======================

Overview
--------
The environment registration module handles the registration of all EnergyNet environments with the Gymnasium framework, making them available through the standard ``gym.make()`` interface.

Registered Environments
---------------------

EnergyNetEnv-v0
^^^^^^^^^^^^^^
The base environment implementing core power system dynamics:

* **ID**: ``EnergyNetEnv-v0``
* **Entry Point**: ``energy_net.env.energy_net_v0:EnergyNetV0``

ISO-RLZoo-v0
^^^^^^^^^^^
Environment optimized for ISO-level control with RL-Zoo compatibility:

* **ID**: ``ISO-RLZoo-v0``
* **Entry Point**: ``energy_net.env.iso_env:make_iso_env_zoo``
* **Max Episode Steps**: 48 (representing 24-hour simulation with 30-minute intervals)

PCS-RLZoo-v0
^^^^^^^^^^^
Power Control System environment with RL-Zoo integration:

* **ID**: ``PCS-RLZoo-v0``
* **Entry Point**: ``energy_net.env.pcs_env:make_pcs_env_zoo``
* **Max Episode Steps**: 48 (representing 24-hour simulation with 30-minute intervals)

Usage
-----
To use any of the registered environments::

    import gymnasium as gym
    import energy_net.envs  # This triggers environment registration

    # Create base environment
    env = gym.make('EnergyNetEnv-v0')

    # Create ISO environment with RL-Zoo compatibility
    iso_env = gym.make('ISO-RLZoo-v0')

    # Create PCS environment with RL-Zoo compatibility
    pcs_env = gym.make('PCS-RLZoo-v0')

Configuration
------------
The environments can be configured through their respective factory functions. See:

* :doc:`environments/base`
* :doc:`environments/iso`
* :doc:`environments/pcs`

API Reference
------------
.. automodule:: energy_net.envs.register_envs
    :members:
    :undoc-members:
    :show-inheritance:


