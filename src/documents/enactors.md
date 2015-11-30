---
title: Enactors
layout: default
category: Tutorials
---

The First Discovery Tool uses [Enactors](http://docs.fluidproject.org/infusion/development/Enactors.html)
to apply the user’s preferences to the interface.
An Enactor is an Infusion component that "acts upon" a preference setting,
making whatever adjustments that are necessary to enact the preference.
For example, the First Discovery Tool uses a text-size enactor to modify the text size of the
Tool interface according to the user’s adjustments to the preference through the text-size panel.

Some preferences may relate to something that doesn’t apply to the First Discovery Tool interface.
For example, the auto-pilot preference wouldn’t have any effect on the Tool.
For these kinds of preferences, no enactor is needed; the flying car itself would need to
retrieve the preference setting and adjust accordingly.

The creation of Enactors is an advanced topic, beyond the scope of this tutorial.
To learn about Enactors, and to learn more about the Preferences Framework that underlies the
First Discovery Tool, see the
[Preferences Framework Tutorial](http://docs.fluidproject.org/infusion/development/tutorial-creatingAPreferencesEditorUsingThePreferencesFramework/CreatingAPreferencesEditorUsingThePreferencesFramework.html).
