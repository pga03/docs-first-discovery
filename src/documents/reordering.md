---
title: Simplest: Reordering preferences
layout: default
category: Tutorials
---

You’ve built the world’s first flying car, and of course, you want your customers to be able to set up their preferences for how it will operate. You start with the First Discovery Tool. Since the driver of a car will probably want an audio interface, you decide that the existing "Show Sounds" preference should be the first preference after the welcome screen.

## Quick version
1. Edit `src/html/firstDiscovery.html` to change the order of the panels.
2. Edit `src/html/confirmTemplate.html` to change the order of preferences in the preferences table on the confirm panel.
3. Edit `src/html/confirmTemplate.html` to change the order of "tts" strings read allowd for the preferences table on the confirm panel.

## Detailed Instructions

1. Edit `src/html/firstDiscovery.html` to change the order of the panels.
    
    The `src/html/firstDiscoveryPreferencesServerIntegration.html` file is the main template for the preference panels. It contains placeholders elements for each preference panel.

    A. In the `"firstDiscoveryPreferencesServerIntegration.html` file, find the `<section>` for the "Show Sounds" element that has the class name `"gpiic-fd-prefsEditor-panel-showSounds"`.

    ```html
    <section class="gpiic-fd-prefsEditor-panel-showSounds gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-showSounds gpii-fd-main"></section>
    ```

    B. Move the "Show Sounds" `<section>` element to be the third one, after the "Welcome" panel. (i.e. after the `<section>` element with the class name `"gpiic-fd-prefsEditor-panel-welcome"`). Don’t change any of the attributes.

    ```html
    <section class="gpiic-fd-prefsEditor-panel-lang gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-lang gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-welcome gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-welcome gpii-fd-main" id="open"></section>
    <section class="gpiic-fd-prefsEditor-panel-showSounds gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-showSounds gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-speakText gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-speakText gpii-fd-main"></section>
    
    //more content not shown here
    ```

    Now that the panels display the preferences with the "Show Sounds" as the second preference (third panel, after the "Welcome" panel), you'll want to update the preferences table on the confirm panel so that it displays the preferences in the same order.

2. Edit `src/html/confirmTemplate.html` to change the order of preferences in the preferences table on the confirm panel.

    A. Find the preferences table declaration with the class name `"gpii-fd-confirm-table"`, and find the `<tr>` section for the "Show Sounds" preference. It has two `<td>` elements that hold a span, one with the "id" of `"showSoundsLabel"`, and the other `"showSoundsConfirmation"`.
    
    ```html
    <tr class="showSounds">
        <td class="gpii-fd-confirm-table-name"><span class="gpii-confirm-label "></span></td>
        <td class="gpii-fd-confirm-table-value"><span class="gpii-confirm-value "></span><span class="gpii-confirm-unit "></span></td>
    </tr>
    ```
    B. Remove the entire "Show Sounds" `<tr>` section, and place it in the second preference position (after "Language", before "Speak").
    
    ```html
    <table class="gpii-fd-confirm-table">
        <tr class="language">
            <td class="gpii-fd-confirm-table-name"><span class="gpii-confirm-label "></span></td>
            <td class="gpii-fd-confirm-table-value"><span class="gpii-confirm-value "></span><span class="gpii-confirm-unit "></span></td>
        </tr>
        <tr class="showSounds">
            <td class="gpii-fd-confirm-table-name"><span class="gpii-confirm-label "></span></td>
            <td class="gpii-fd-confirm-table-value"><span class="gpii-confirm-value "></span><span class="gpii-confirm-unit "></span></td>
        </tr>
        <tr class="speak">
            <td class="gpii-fd-confirm-table-name"><span class="gpii-confirm-label "></span></td>
            <td class="gpii-fd-confirm-table-value"><span class="gpii-confirm-value "></span><span class="gpii-confirm-unit "></span></td>
        </tr>
    ```    
    Now when you run the tool, the "Show Sounds" preference will appear second on the preferences table on the confirm panel, in the same order they appear to the user in the tool.
    
    But, now that the order of the preferences has changed in the table, you'll need to make sure that the voicing for the table is in the same order as well. You will need to change the order of the tts strings.
    
3. Edit `src/html/confirmTemplate.html` to change the order of "tts" strings read allowd for the preferences table on the confirm panel.

    A. Find the `<p>` declaration for the "Show Sounds" preference, with the class `"showSounds-tts"` on the end.
    
    ```html
    <p class="gpii-fd-hidden-accessible gpiic-fd-panel-content-tts showSounds-tts"></p>
    ```    
    B. Remove the entire "Show Sounds" `<p>` section, and place it in the second preference position (after "Language", before "Speak").

    ```html
    <p class="gpii-fd-hidden-accessible gpiic-fd-panel-content-tts language-tts"></p>
    <p class="gpii-fd-hidden-accessible gpiic-fd-panel-content-tts showSounds-tts"></p>
    <p class="gpii-fd-hidden-accessible gpiic-fd-panel-content-tts speak-tts"></p>
    
    //more content not shown
    ```
    
    Now when you get to the confirm panel, the show sounds preference will be voiced in the same order as the preferences appear in the preferences table.