.. _doc_introduction_to_godot:

Introduction to Godot
=====================

This article is here to help you figure out whether Godot might be a good fit
for you. We will introduce some broad features of the engine to give you a feel
for what you can achieve with it and answer questions such as "what do I need to
know to get started?".

This is by no means an exhaustive overview. We will introduce many more features
in this getting started series.

What is Godot?
--------------

Godot is a general-purpose 2D and 3D game engine designed to support all sorts
of projects. You can use it to create games or applications you can then release
on desktop or mobile, as well as on the web.

You can also create console games with it, although you either need strong
programming skills or a developer to port the game for you.

.. note:: For information about console support, see the `Godot website <https://godotengine.org/consoles/>`_.

.. admonition:: Engine context
   :class: devin-context

   Godot's platform abstraction lives in the
   `/platform/* <https://github.com/HathawayJA/godevin/tree/master/platform>`__
   directory, with dedicated backends for Android, iOS, Linux/BSD, macOS, visionOS,
   Web, and Windows. Each platform folder contains the OS-specific entry point
   and display server implementation. Platform-agnostic drivers (graphics, audio,
   input) are in
   `/drivers/* <https://github.com/HathawayJA/godevin/tree/master/drivers>`__.

What can the engine do?
-----------------------

Godot was initially developed in-house by an Argentinian game studio. Its
development started in 2001, and the engine was rewritten and improved
tremendously since its open source release in 2014.

Some examples of games created with Godot include Cassette Beasts, PVKK, and
Usagi Shima. As for applications, the open source pixel art drawing program
Pixelorama is powered by Godot, and so is the voxel RPG creator RPG in a Box.
You can find many more examples in the `Official Showcase
<https://godotengine.org/showcase/>`_.

.. figure:: img/introduction_usagi_shima.webp
   :align: center

   Usagi Shima

.. figure:: img/introduction_cassette_beasts.webp
   :align: center

   Cassette Beasts

.. figure:: img/introduction_pvkk.webp
   :align: center

   PVKK: Planetenverteidigungskanonenkommandant

.. figure:: img/introduction_rpg_in_a_box.webp
   :align: center

   RPG in a Box

How does it work and look?
--------------------------

Godot comes with a fully-fledged game editor with integrated tools to answer the
most common needs. It includes a code editor, an animation editor, a tilemap
editor, a shader editor, a debugger, a profiler, and more.

.. image:: img/introduction_editor.webp

The team strives to offer a feature-rich game editor with a consistent user
experience. While there is always room for improvement, the user interface keeps
getting refined.

.. admonition:: Engine context
   :class: devin-context

   The editor itself is built using Godot's own UI framework. Its source lives in
   `/editor/* <https://github.com/HathawayJA/godevin/tree/master/editor>`__,
   with the main entry point at
   `editor/editor_node.cpp <https://github.com/HathawayJA/godevin/blob/master/editor/editor_node.cpp>`__.
   Editor plugins, docks, and inspectors are organized into subdirectories such as
   ``editor/plugins/``, ``editor/docks/``, and ``editor/inspector/``. The editor
   is compiled conditionally via the ``TOOLS_ENABLED`` preprocessor flag, meaning
   exported games never include editor code.

Of course, if you prefer, you can work with external programs. We officially
support importing 3D scenes designed in Blender_ and maintain plugins to code in
VSCode_ and Emacs_ for GDScript and C#. We also support Visual Studio for C# on
Windows.

.. image:: img/introduction_vscode.png

Programming languages
---------------------

Let's talk about the available programming languages.

You can code your games using :ref:`GDScript <doc_gdscript>`, a
Godot-specific and tightly integrated language with a lightweight syntax, or
:ref:`C# <doc_c_sharp>`, which is popular in the games industry.
These are the two main scripting languages we support.

With the :ref:`GDExtension <doc_what_is_gdextension>` technology, you can also
write gameplay or high-performance algorithms in :ref:`C++ <doc_godot_cpp>` or
:ref:`other languages <doc_scripting_languages>` without recompiling the engine.
You can use this technology to integrate third-party libraries and other
Software Development Kits (SDK) in the engine.

Of course, you can also directly add modules and features to the engine, as it's
completely free and open source.

.. admonition:: Engine context
   :class: devin-context

   GDScript is implemented as an engine module at
   `/modules/gdscript/* <https://github.com/HathawayJA/godevin/tree/master/modules/gdscript>`__.
   C# support lives in
   `/modules/mono/* <https://github.com/HathawayJA/godevin/tree/master/modules/mono>`__.
   GDExtension — the technology that enables C++ and other language bindings without
   recompiling — is handled by the extension system in
   `/core/extension/* <https://github.com/HathawayJA/godevin/tree/master/core/extension>`__.
   All scripting languages register through the ``ScriptServer`` interface defined in
   `core/object/script_language.h <https://github.com/HathawayJA/godevin/blob/master/core/object/script_language.h>`__.

.. _doc_introduction_learning_programming:

What do I need to know to use Godot?
------------------------------------

Godot is a feature-packed game engine. With its thousands of features, there is
a lot to learn. To make the most of it, you need good programming foundations.
While we try to make the engine accessible, you will benefit a lot from knowing
how to think like a programmer first.

Godot relies on the object-oriented programming paradigm. Being comfortable with
concepts such as classes and objects will help you code efficiently in it.

If you are entirely new to programming, GDQuest's *Learn GDScript From Zero*
is a free and open source interactive tutorial for absolute beginners to
learn to program with Godot's GDScript language. It is available as a
`desktop application <https://gdquest.itch.io/learn-godot-gdscript>`__
or `in the browser <https://gdquest.github.io/learn-gdscript>`__.

We will provide you with more Godot-specific learning resources in
:ref:`doc_learning_new_features`.

In the next part, you will get an overview of the engine's essential concepts.

.. _Blender: https://www.blender.org/
.. _VSCode: https://github.com/godotengine/godot-vscode-plugin
.. _Emacs: https://github.com/godotengine/emacs-gdscript-mode
.. _official showcase videos: https://www.youtube.com/playlist?list=PLeG_dAglpVo6EpaO9A1nkwJZOwrfiLdQ8
