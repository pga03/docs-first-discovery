---
title: Simplest: Reordering preferences
layout: default
category: Tutorials
---

You’ve built the world’s first flying car, and of course, you want your customers to be able to set up their preferences for how it will operate. You start with the First Discovery Tool. Since the driver of a car will probably want an audio interface, you decide that the existing "show sounds" preference should be the first preference after the welcome screen.

## Quick version
1. Edit `demos/index.html` to change the order of the icons at the bottom of the screen.
2. Edit `src/html/firstDiscovery.html` to change the order of the panels.

## Detailed Instructions

1. Edit `demos/index.html` to change the order of the icons at the bottom of the screen.

    A. The `demos/index.html` file is the main HTML file for the First Discovery Tool demo. It contains [placeholders for the bits and pieces that will be rendered into the interface].

    You can see the entire file here: https://github.com/fluid-project/first-discovery/blob/master/demos/index.html

    B. In the `demos/index.html` file, find the list of icons (a `<ul>` with the class `"gpii-fd-navIcon-outer"` as described above).

    C. Find the `<li>` element that has the class name `"gpii-fd-showSounds"`.

    ```html
    <ul class="gpii-fd-navIcon-outer">
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-lang">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon-welcome">
        </li>
        <!-- some list items not shown -->
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-showSounds">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <!-- some list items not shown -->
    </ul>
    ```
    D. Move the entire `<li>` – without changing any of its content – to be the third item in the list, after the welcome icon (i.e. after the `<li>` with the class name `"gpii-fd-navIcon-welcome"`).

    ```html
    <ul class="gpii-fd-navIcon-outer">
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-lang">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon-welcome">
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-showSounds">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-volume">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-speechRate">
            <!-- some list items not shown -->
    </u>
    ```

2. Edit `src/html/firstDiscovery.html` to change the order of the panels.
    The `src/html/firstDiscovery.html` file is the main template for the preference panels. It contains placeholders elements for each preference panel.

    You can see the entire file here: https://github.com/fluid-project/first-discovery/blob/master/src/html/firstDiscovery.html

    In the `"firstDiscovery.html` file, find the `<section>` element that has the class name `"gpiic-fd-prefsEditor-panel-showSounds"`.

    ```html
    <section class="gpiic-fd-prefsEditor-panel-lang gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-lang gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-welcome gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-welcome gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-speakText gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-speakText gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-speechRate gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-speechRate gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-contrast gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-contrast gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-size gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-size gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-onScreenKeyboard gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-onScreenKeyboard gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-captions gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-captions gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-showSounds gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-showSounds gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-keyboard gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-keyboard gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-congratulations gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-congratulations gpii-fd-main"></section>
    ```

    Move the `<section>` element to be the third one, after the welcome panel (i.e. after the `<section>` element with the class name `"gpiic-fd-prefsEditor-panel-welcome"`). Don’t change any of the attributes.

    ```html
    <section class="gpiic-fd-prefsEditor-panel-lang gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-lang gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-welcome gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-welcome gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-showSounds gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-showSounds gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-speakText gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-speakText gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-speechRate gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-speechRate gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-contrast gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-contrast gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-size gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-size gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-onScreenKeyboard gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-onScreenKeyboard gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-captions gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-captions gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-keyboard gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-keyboard gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-congratulations gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-congratulations gpii-fd-main"></section>
    ```

    You want to make sure that the order of the panels (the `<section`> elements) matches the order of the icons (the `<li>` elements).
