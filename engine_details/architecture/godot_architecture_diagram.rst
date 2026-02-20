.. _doc_godot_architecture_diagram:

Godot's architecture overview
=============================

The following diagram describes the most important aspects of Godot's architecture.
It's not designed to be exhaustive, with the purpose of just giving a high-level overview of
the main components and their relationships to each other.

.. figure:: img/godot-architecture-diagram.webp
   :alt: Diagram of Godot's Architecture; divided into three layers (from top to bottom: Scene layer, Server layer, and Drivers & Platform interface layer), with Core and Main separated on the right side since they interact with all layers.

   Credit: `Hendrik Brucker <https://github.com/Geometror/godot-architecture-diagram>`__

Scene Layer
~~~~~~~~~~~

The Scene layer is the highest level of Godot's architecture, providing the scene system, which is the main way to build and structure your applications or games.
See :ref:`class_SceneTree` / :ref:`doc_scene_tree` and :ref:`class_Node` for more information.

Corresponding source code: `/scene/* <https://github.com/HathawayJA/godevin/tree/master/scene>`__

.. admonition:: Engine context
   :class: devin-context

   The Scene layer is organized into subdirectories by domain:
   ``scene/2d/`` and ``scene/3d/`` for spatial nodes, ``scene/gui/`` for the
   Control-based UI toolkit, ``scene/animation/`` for animation players and
   tweens, and ``scene/main/`` for the tree infrastructure itself
   (``SceneTree``, ``Node``, ``Viewport``, ``Window``). Node callbacks like
   ``_process()`` and ``_physics_process()`` are dispatched by
   `scene/main/scene_tree.cpp <https://github.com/HathawayJA/godevin/blob/master/scene/main/scene_tree.cpp>`__
   during the main loop iteration.

Server Layer
~~~~~~~~~~~~

Server components implement most of Godot's subsystems (rendering, audio, physics, etc.). They are singleton objects initialized at engine startup.

`Why does Godot use servers and RIDs? <https://godotengine.org/article/why-does-godot-use-servers-and-rids>`__

Corresponding source code: `/servers/* <https://github.com/HathawayJA/godevin/tree/master/servers>`__

.. admonition:: Engine context
   :class: devin-context

   Key server singletons include ``RenderingServer``
   (`servers/rendering_server.cpp <https://github.com/HathawayJA/godevin/blob/master/servers/rendering_server.cpp>`__),
   ``PhysicsServer3D``
   (`servers/physics_server_3d.cpp <https://github.com/HathawayJA/godevin/blob/master/servers/physics_server_3d.cpp>`__),
   and ``AudioServer``
   (`servers/audio_server.cpp <https://github.com/HathawayJA/godevin/blob/master/servers/audio_server.cpp>`__).
   The scene layer communicates with servers through RIDs (Resource IDs) —
   opaque handles that let the server own and manage resources on its own
   thread without exposing internal pointers. Servers are registered during
   engine startup in
   `servers/register_server_types.cpp <https://github.com/HathawayJA/godevin/blob/master/servers/register_server_types.cpp>`__.

Drivers / Platform Interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This layer abstracts low-level platform-specific details, containing drivers for graphics APIs, audio backends and operating system interfaces
(all platform-specific :ref:`class_OS` and :ref:`class_DisplayServer` implementations).

Corresponding source code: `/drivers/* <https://github.com/HathawayJA/godevin/tree/master/drivers>`__ and `/platform/* <https://github.com/HathawayJA/godevin/tree/master/platform>`__

.. admonition:: Engine context
   :class: devin-context

   Each supported platform has its own directory under ``platform/`` containing
   an OS subclass and a ``DisplayServer`` implementation. For example,
   `platform/linuxbsd/ <https://github.com/HathawayJA/godevin/tree/master/platform/linuxbsd>`__
   provides ``OS_LinuxBSD`` and Wayland/X11 display servers.
   The ``drivers/`` directory holds cross-platform backend implementations for
   Vulkan
   (`drivers/vulkan/ <https://github.com/HathawayJA/godevin/tree/master/drivers/vulkan>`__),
   OpenGL
   (`drivers/gles3/ <https://github.com/HathawayJA/godevin/tree/master/drivers/gles3>`__),
   and audio output (ALSA, PulseAudio, CoreAudio, WASAPI).

Core
~~~~

The Engine's core contains essential functionality and data structures used throughout the engine,
like :ref:`class_Object` and :ref:`class_ClassDB`, :ref:`memory management <doc_core_types>`, :ref:`containers <doc_core_types>`, file I/O, :ref:`Variant <doc_variant_class>`, and :ref:`other utilities <doc_common_engine_methods_and_macros>`.

Corresponding source code: `/core/* <https://github.com/HathawayJA/godevin/tree/master/core>`__

.. admonition:: Engine context
   :class: devin-context

   Core is subdivided into several key areas:
   ``core/object/`` houses the ``Object`` base class, ``ClassDB``, and the
   method-binding macros that expose C++ to scripting.
   ``core/variant/`` contains the ``Variant`` tagged-union type that underpins
   all scripting interop.
   ``core/io/`` provides file access, resource loading/saving, and networking.
   ``core/templates/`` holds the custom container types (``Vector``,
   ``HashMap``, ``List``, etc.) that replace STL throughout the codebase.
   ``core/string/`` implements ``String`` (UTF-32) and ``StringName``
   (interned strings for fast comparison).

Main
~~~~

The Main component is responsible for initializing and managing the engine lifecycle, including startup, shutdown, and the main loop. See :ref:`class_MainLoop` for more details.

Corresponding source code: `/main/* <https://github.com/HathawayJA/godevin/tree/master/main>`__

.. admonition:: Engine context
   :class: devin-context

   `main/main.cpp <https://github.com/HathawayJA/godevin/blob/master/main/main.cpp>`__
   contains the ``Main::setup()`` and ``Main::start()`` functions that
   initialize every engine subsystem in order: OS, core types, servers,
   modules, scene types, and the editor (when running with ``tools``). The
   main loop is typically a ``SceneTree`` instance whose ``process()`` and
   ``physics_process()`` methods are called each iteration of the game loop.

