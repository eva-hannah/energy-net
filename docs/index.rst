.. Energy Net documentation master file, created by
   sphinx-quickstart on Tue Aug 12 18:33:39 2025.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Energy Net documentation
========================

.. raw:: html

   <style>
   h1, h2, h3, h4, h5, h6 {
       color: #2a4d69;
       font-family: 'Segoe UI', 'Arial', sans-serif;
   }
   body {
       font-family: 'Segoe UI', 'Arial', sans-serif;
       color: #222;
       background-color: #f8f9fa;
   }
   code, pre {
       background-color: #f4f4f4;
       color: #c7254e;
       font-family: 'Fira Mono', 'Consolas', monospace;
       border-radius: 4px;
       padding: 2px 4px;
   }
   .highlight .n {
       color: #1e88e5;
   }
   .highlight .k {
       color: #43a047;
   }
   .highlight .s {
       color: #e65100;
   }
   </style>

Grid Entity
===========

The ``grid_entity`` module defines the core abstractions for all grid entities in the Energy Net simulation framework. 
It provides a consistent interface for both elementary and composite entities, enabling modular and extensible modeling of smart grid components.

**Key Classes:**

- **:class:`GridEntity`**: Abstract base class for all grid entities. Handles logging and defines the reset interface.
- **:class:`ElementaryGridEntity`**: Represents basic entities such as batteries, production units, and consumption units. Requires implementation of ``perform_action``, ``get_state``, and ``update``.
- **:class:`CompositeGridEntity`**: Manages a collection of sub-entities, allowing coordinated actions and state aggregation across multiple grid components.

**Usage Example:**

.. code-block:: python

   from energy_net.grid_entity import ElementaryGridEntity, CompositeGridEntity

   # Define a custom battery entity inheriting from ElementaryGridEntity
   class BatteryEntity(ElementaryGridEntity):
       def perform_action(self, action: float) -> None:
           # Implement battery-specific action logic
           pass
       def get_state(self) -> float:
           # Return current battery state
           return 0.0
       def update(self, time: float, action: float = 0.0) -> None:
           # Update battery state
           pass

   # Instantiate and use entities
   battery = BatteryEntity(dynamics=None, log_file="battery.log")
   composite = CompositeGridEntity([battery], log_file="composite.log")
   composite.perform_action({'BatteryEntity_0': 1.0})
   composite.update(time=0.5, actions={'BatteryEntity_0': 1.0})

.. automodule:: grid_entity
   :members:
   :undoc-members:
   :show-inheritance:

.. toctree::
   :maxdepth: 2
   :caption: Contents:

