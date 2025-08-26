ISO Environment
==============

Overview
--------
The ISO (Independent System Operator) environment provides a simulation framework for power grid operations and market interactions at the ISO level.

Configuration
------------
The ISO environment can be configured through the following parameters:

* ``num_nodes``: Number of nodes in the power network
* ``time_horizon``: Simulation time horizon in hours
* ``market_clearing_interval``: Interval for market clearing operations (in minutes)
* ``transmission_constraints``: Boolean flag to enable/disable transmission constraints

Usage Examples
-------------
Basic usage of the ISO environment::

    import energynet
    
    # Initialize environment
    env = energynet.make('iso-v0')
    
    # Configure parameters
    env.configure(
        num_nodes=5,
        time_horizon=24,
        market_clearing_interval=60
    )

Advanced Features
---------------
Transmission System
^^^^^^^^^^^^^^^^^
The ISO environment includes a detailed transmission system model with:

* Power flow constraints
* Line capacity limits
* Node voltage levels

Market Operations
^^^^^^^^^^^^^^^
Supported market mechanisms include:

* Day-ahead market
* Real-time market
* Ancillary services


