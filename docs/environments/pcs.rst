PCS Environment
=============

Overview
--------
The PCS (Power Control System) environment provides a specialized wrapper for training reinforcement learning agents in power control scenarios. It is designed to work seamlessly with the RL-Baselines3-Zoo framework.

Environment Factory
-----------------
The main entry point is the ``make_pcs_env_zoo`` factory function, which creates a properly configured PCS environment instance.

Configuration Parameters
^^^^^^^^^^^^^^^^^^^^^^
The environment can be customized with the following parameters:

* ``norm_path`` (str, optional): Path to saved normalization statistics
* ``iso_policy_path`` (str, optional): Path to a pre-trained ISO policy model
* ``log_dir`` (str): Directory for saving monitoring logs (default: "logs")
* ``use_dispatch_action`` (bool): Enable/disable dispatch in ISO action space (default: False)
* ``dispatch_strategy`` (str): Strategy for dispatch when not agent-controlled (default: "PROPORTIONAL")
* ``monitor`` (bool): Enable environment monitoring (default: True)
* ``seed`` (int, optional): Random seed for reproducibility

Usage Example
------------
Basic usage of the PCS environment::

    from energy_net.envs.pcs_env import make_pcs_env_zoo

    # Create environment with default settings
    env = make_pcs_env_zoo(
        log_dir="training_logs",
        use_dispatch_action=True,
        dispatch_strategy="PROPORTIONAL"
    )

    # Create environment with pre-trained ISO policy
    env = make_pcs_env_zoo(
        iso_policy_path="path/to/iso_model.zip",
        monitor=True,
        seed=42
    )

Supported Features
----------------
ISO Policy Integration
^^^^^^^^^^^^^^^^^^
The environment supports loading pre-trained ISO policies:

* Compatible with PPO and TD3 algorithms
* Automatic algorithm detection based on filename
* Error handling for policy loading failures

Monitoring and Logging
^^^^^^^^^^^^^^^^^^^
Built-in support for:

* Episode statistics tracking
* Performance monitoring
* Automated log directory creation

API Reference
------------
.. autofunction:: energy_net.envs.pcs_env.make_pcs_env_zoo

See Also
--------
* :doc:`iso`
* :doc:`energynet`
