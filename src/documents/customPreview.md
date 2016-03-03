---
title: Advanced: Adding A Custom Preview
layout: default
category: Tutorials
---

## What is the preview?

The preview for the First Discovery Tool is a sub-component of the prefsEditor in the firstDiscoveryEditor.js file. The goal of the preview is to have self contained preview content pages that allow for customizable and (mostly) non-interactive ways to show the users of the First Discovery Tool how their preferences selections would look on different types of web pages. The initial purpose of the multiple different preview content pages was to help facilitate user familiarity during usability testing. 

This guide is written primarily for technical individuals with some exposure to Web Development (HTML/CSS, JQuery and JSON), but will be structured so that anyone could potentially follow along. The guide will consist of several sections, each of which will be built off of the last. Additionally, I will provide a link to the final version of the code to aid in any debugging issues that you might come across.

__NOTE:__ You need to have already set up your local development space for the First Discovery Tool and need to be running your First Discovery Server to be able to complete this tutorial. 

![First Discovery Tool with highlighted preview content to illustrate what a preview is.](images/customPreview1.png)

## Creating the web page preview in HTML/CSS

In this part of the tutorial we will be creating an html/css content page to display in our First Discovery Tool preview. We will be creating a very basic html page with an internal style sheet, a few text strings and a picture. The goal is emphasize the process of how to set up a new preview, not to make another one entirely.

__NOTE:__ While the example here is basic to save time, the First Discovery Tool utilizes Foundation 5 for some of its formatting and styling. This means that any practices and techniques found on their website can be used for your preview content page, as long as, you include the correct files. For a basic idea of how to use foundation check out this tutorial on their website. https://scotch.io/tutorials/getting-started-with-foundation-5-by-zurb

__STEP 1:__ Create a new file in __first-discovery\src\html__ called __examplePreview.html__

__STEP 2:__ Copy the following text into the __examplePreview.html__ file.

__examplePreview.html__
```html
<!DOCTYPE html>
<!--[if IE 9]>
<html class="lt-ie10" lang="en"> <![endif]-->
<html class="no-js" lang="en">
<head>
    <meta charset="utf-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Foundation 5</title>

    <!-- Foundation CSS links -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/foundation/5.5.3/css/normalize.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/foundation/5.5.3/css/foundation.min.css">
    <link rel="stylesheet" href="../../src/lib/foundation/css/foundation-icons/foundation-icons.css" />
    
    <!-- CSS required for the Prefs Editor -->
    <link rel="stylesheet" type="text/css" href="../../src/lib/infusion/src/framework/preferences/css/Enactors.css"/>
    <link rel="stylesheet" type="text/css" href="../../src/lib/infusion/src/framework/preferences/css/PrefsEditor.css"/>
    <link rel="stylesheet" type="text/css" href="../../src/css/style.css"/>
    
    <!-- Internal Style Sheet -->
    <style type="text/css">
        body { 
            padding-top:50px;
        }
        #searchResults {
            background-image:url('../images/searchresult.png');
            height: 4em;
        }
        .fl-theme-bw #searchResults { background-image:url('../images/searchresult_bw.png'); }
        .fl-theme-wb #searchResults { background-image:url('../images/searchresult_wb.png'); }
    </style>
</head>

<body>
<div class="row">
  <div class="small-4 columns">  
    <ul class="pricing-table">
      <li class="title">Standard</li>
      <li class="price">$29.99</li>
      <li class="description">An awesome description</li>
      <li class="bullet-item">1 Database</li>
      <li class="bullet-item">5GB Storage</li>
      <li class="bullet-item">20 Users</li>
      <li class="cta-button"><a class="button radius" href="#">Buy Now</a></li>
    </ul>
  </div>
  <div class="small-4 columns">  
    <ul class="pricing-table">
      <li class="title">Medium</li>
      <li class="price">$49.99</li>
      <li class="description">An awesome description</li>
      <li class="bullet-item">5 Database</li>
      <li class="bullet-item">10GB Storage</li>
      <li class="bullet-item">40 Users</li>
      <li class="cta-button"><a class="button radius" href="#">Buy Now</a></li>
    </ul>
  </div>
  <div class="small-4 columns">
    <ul class="pricing-table">
      <li class="title">Premium</li>
      <li class="price">$99.99</li>
      <li class="description">An awesome description</li>
      <li class="bullet-item">Unlimited Database</li>
      <li class="bullet-item">Unlimited Storage</li>
      <li class="bullet-item">Unlimited Users</li>
      <li class="cta-button"><a class="button success round" href="#">Buy Now</a></li>
    </ul>
  </div>
  
  </div>
</div>
<!-- Calls to the foundation Javascript files -->
<script src="https://code.jquery.com/jquery-2.1.4.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/foundation/5.5.3/js/foundation.min.js"></script>
<script>
    $(document).ready(function () {
        // Start infusion
        $(document).foundation();
    });
</script>
</body>

</html>
```

__STEP 3: Navigate to__ your __examplePreview.html__ file and open it with a web browser. It should look something like the image below.

![example Preview html screenshot showing some pricing displays with text and buttons.](images/customPreview2.png)

The big take away for anyone looking to customize their own preview content page is that you will need the following lines from the code above (in some form) to have foundation working on the preview content page and to have the preferences affect it. The reference links to the normalize.min.css, foundation.min.css, jquery.min.js and foundation.min.js can all be replaced with calls to internal files, if you have them available.
```html
<!-- Foundation CSS links -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/foundation/5.5.3/css/normalize.min.css">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/foundation/5.5.3/css/foundation.min.css">
<link rel="stylesheet" href="../../src/lib/foundation/css/foundation-icons/foundation-icons.css" />

<!-- CSS required for the Prefs Editor -->
<link rel="stylesheet" type="text/css" href="../../src/lib/infusion/src/framework/preferences/css/Enactors.css"/>
<link rel="stylesheet" type="text/css" href="../../src/lib/infusion/src/framework/preferences/css/PrefsEditor.css"/>
<link rel="stylesheet" type="text/css" href="../../src/css/style.css"/>
```
```html
<!-- Calls to the foundation Javascript files -->
<script src="https://code.jquery.com/jquery-2.1.4.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/foundation/5.5.3/js/foundation.min.js"></script>
<script>
    $(document).ready(function () {
        // Start infusion
        $(document).foundation();
    });
</script>
```

## Route Setup

Its nice to see what our preview will look like in the web browser, but now we need to get it into the preview of the First Discovery Tool.  To do this we will need to go into the firstDiscoveryEditor.js file and find the gpii.firstDiscovery.getPreviewUrl function and add an additional else if statement to handle our new preview content page. 

__STEP 1: Navigate to__ your __firstDiscoveryEditor.js__ file and open it. Make the __following changes__ to the getPreviewUrl function.

__firstDiscoveryEditor.js__

```javascript
gpii.firstDiscovery.getPreviewUrl = function (that, languageCode) {
    var baseurl = "../../src/html/";
    var previewname = gpii.firstDiscovery.getPreviewName();
    var previewpage = "searchpreview.html"; //default
    if (previewname === "search") {
        previewpage = "searchpreview.html";
    } else if (previewname === "electron") {
        previewpage = "electronpreview.html";
    } else if (previewname === "example") {
        previewpage = "examplePreview.html";
    }

    //unsupported languages will return english preview.
    //TODO: create previews for remaining languages, de-DE, nl-NL, sv-SE
    if(languageCode == "de-DE"){
        languageCode = "en-US";
    }
    if(languageCode == "nl-NL"){
        languageCode = "en-US";
    }
    if(languageCode == "sv-SE"){
        languageCode = "en-US";
    }

    var previewQueryString = "?lang=" + languageCode;

    return encodeURI(baseurl + previewpage + previewQueryString);
};
```

__STEP 2: Start up your first-discovery-server__ by navigating to your local repository and __run :
node index.js__

![Command Prompt demonstrating successful startup of local first discovery server](images/customPreview3.png)

__STEP 3:__ Navigate to your __Chrome browser__ and navigate to http://localhost:8088/demos/prefsServerIntegration/index.html?preview=example

![The first Discovery Tool with the new custom preview html that we created earlier](images/customPreview4.png)

As you can see, we now have a route to our First-Discovery-Tool Preview. The First Discovery Tool allows the users to change to a specific preview content page by editing the end of the url to any of those specified in the getPreviewUrl function that we changed. This includes __electron__, __search__ and now __example__.

SEARCH: http://localhost:8088/demos/prefsServerIntegration/index.html?preview=search

ELECTRON: http://localhost:8088/demos/prefsServerIntegration/index.html?preview=electron

EXAMPLE: http://localhost:8088/demos/prefsServerIntegration/index.html?preview=example

## Extracting and Storing the Page Content

The First Discovery Tool supports multiple languages, so the next step is to extract all of the words that could be translated into a separate message file (JSON file) that is easily translated and maintained, as opposed to several whole html pages in different languages.

__STEP 1:__ Add the following functions to script tag that the $(document).foundation(); call is made.

__examplePreview.html__
```javascript
<script>
    $(document).ready(function () {
        // populate the preview's text.
        fetch_and_insert_text();
        // Start infusion
        $(document).foundation();
    });
    
    // Parses the query string and returns an object container key-value pairs from
    // decoded querystring variables
    function getQueryStringKeys() {
        var queryKvps = {};
        var kvps = window.location.search.substring(1).split("&");
        for (var i = 0; i < kvps.length; i++) {
            var kvp_pieces = kvps[i].split("=");
            queryKvps[decodeURIComponent(kvp_pieces[0])] = decodeURIComponent(kvp_pieces[1]);
        }
        return queryKvps;
    }

    // Parses the "lang" variable out of the querystring, returning the languageCode to use
    // for the page text
    function getLanguageCode() {
        var languageCode = "en-US"; //default to english
        var queryKvps = getQueryStringKeys();
        if (queryKvps.lang && queryKvps.lang != "undefined") {
            languageCode = queryKvps["lang"];
        }
        return languageCode;
    }

    // Fetch the language text file based on lang Query String variable, and pass
    // the returned json data to the function that will place strings in the UI
    function fetch_and_insert_text() {
        var langaugeCode = getLanguageCode();
        var url = '../messages/examplePreview_' + langaugeCode + ".json";
        $.ajax({
            type: 'GET',
            url: url,
            dataType: 'json',
            success: function (data) {
                insertText(data);
            },
            error: function (jqXHR, textStatus, errorThrown) {
                console.log("error occured: " + textStatus);
            }
        });
    }

    // Place strings into the UI from the given json data in arg 0
    function insertText(search_preview_text) {

    }
</script>
```

These functions are the helper functions that we will use to read the text from the JSON file that we will create and use to insert the text into the html file. The __fetch_and_insert_text()__ function is the most important to understand to make use of the language preference of the First Discovery Tool. This function makes a call to the __getLanguageCode()__ to get the __language code__ that has been set on the document. This language code is used to select the correct language message file by concatenating the language code into the name of the JSON file.

__examplePreview.html__ - reference
```javascript
    function fetch_and_insert_text() {
        var langaugeCode = getLanguageCode();
        var url = '../messages/examplePreview_' + langaugeCode + ".json";
```
After the url is created an ajax call is made to get the data from the file and pass it to the insertText(data) function. 

```javascript
        $.ajax({
            type: 'GET',
            url: url,
            dataType: 'json',
            success: function (data) {
                insertText(data);
            },
```
__STEP 2: Create a file__ called __examplePreview_en-US.json__ in __src/messages__ and __copy__ the following code into it.

__examplePreview_en-US.json__
```JSON
    {
  "headings": [
    {
      "text": "Standard",
      "tts": "Standard"
    },
    {
      "text": "Medium",
      "tts": "Medium"
    },
    {
      "text": "Premium",
      "tts": "Premium"
    }
  ],
  "prices": [
    {
      "text": "$29.99",
      "tts": "Twenty-Nine Ninety-Nine"
    },
    {
      "text": "$49.99",
      "tts": "Forty-Nine Ninety-Nine"
    },
    {
      "text": "$99.99",
      "tts": "Ninety-Nine Ninety-Nine"
    }
  ],
  "descriptions": [
    {
      "text": "An awesome description",
      "tts": "An awesome description"
    },
    {
      "text": "An awesome description",
      "tts": "An awesome description"
    },
    {
      "text": "An awesome description",
      "tts": "An awesome description"
    }
  ],
  "databases": [
    {
      "text": "1 Database",
      "tts": "1 Database"
    },
    {
      "text": "5 Databases",
      "tts": "5 Databases"
    },
    {
      "text": "Unlimited Databases",
      "tts": "Unlimited Databases"
    }
  ],
  "data": [
    {
      "text": "5GB Storage",
      "tts": "Five Gigabyte Storage"
    },
    {
      "text": "10GB Storage",
      "tts": "Ten Gigabyte Storage"
    },
    {
      "text": "Unlimited Storage",
      "tts": "Unlimited Storage"
    }
  ],
  "users": [
    {
      "text": "20 Users",
      "tts": "Twenty Users"
    },
    {
      "text": "40 Users",
      "tts": "Forty Users"
    },
    {
      "text": "Unlimited Users",
      "tts": "Unlimited Users"
    }
  ],
  "buttons": [
    {
      "text": "Buy Now",
      "tts": "Buy Now"
    },
    {
      "text": "Buy Now",
      "tts": "Buy Now"
    },
    {
      "text": "Buy Now",
      "tts": "Buy Now"
    }
  ]
}

```

By setting up an English language message file containing all of the text for our new examplePreview, we have set the stage to allow our preview to respond to changes to the language preference without the need for excessive changes to our previewExample.html document. In the next section we will remove the text from the actual examplePreview.html file and insert references to our new message file.

Once we have the data from the ajax get statement, we can access it in our insertText(data) function in the following manner.  

```javascript
$("#heading0").text(example_preview_text.headings[0].text);
```

__#heading0__ references an id that we will assign to an html element. __.text()__ will set the text of that element to string that is inside the function. __example_preview_text__ is what we call the json data in the insertText(example_preview_text) function. Once we have that json data object we can access it by using the __data.key[].key__ format. The one above would be __example_preview_text.headings[0].text__  which would return __"Standard"__.

__STEP 3: Update customPreview.html__ with id's to match what the example above shows and delete the text. You can use the following code.

__examplePreview.html__
```html
<body>
<div class="row">
  <div class="small-4 columns">  
    <ul class="pricing-table">
      <li id="heading0" class="title"></li>
      <li id="price0" class="price"></li>
      <li id="description0" class="description"></li>
      <li id="database0" class="bullet-item"></li>
      <li id="data0" class="bullet-item"></li>
      <li id="user0" class="bullet-item"></li>
      <li class="cta-button"><a id="button0" class="button radius" href="#"></a></li>
    </ul>
  </div>
  <div class="small-4 columns">  
    <ul class="pricing-table">
      <li id="heading1" class="title"></li>
      <li id="price1" class="price"></li>
      <li id="description1" class="description"></li>
      <li id="database1" class="bullet-item"></li>
      <li id="data1" class="bullet-item"></li>
      <li id="user1" class="bullet-item"></li>
      <li class="cta-button"><a id="button1" class="button radius" href="#"></a></li>
    </ul>
  </div>
  <div class="small-4 columns">
    <ul class="pricing-table">
      <li id="heading2" class="title"></li>
      <li id="price2" class="price"></li>
      <li id="description2" class="description"></li>
      <li id="database2" class="bullet-item"></li>
      <li id="data2" class="bullet-item"></li>
      <li id="user2" class="bullet-item"></li>
      <li class="cta-button"><a id="button2" class="button success round" href="#"></a></li>
    </ul>
  </div>
</div>
<!-- Calls to the foundation Javascript files -->
<script src="https://code.jquery.com/jquery-2.1.4.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/foundation/5.5.3/js/foundation.min.js"></script>
```

__STEP 4: Populate the insertText(example_preview_text)__ with calls to get the text from the JSON data object based on the id's we just added to the html elements.

__examplePreview.html__
```javascript
// Place strings into the UI from the given json data in arg 0
    function insertText(example_preview_text) {
        //headers
        $("#heading0").text(example_preview_text.headings[0].text);
        $("#heading1").text(example_preview_text.headings[1].text);
        $("#heading2").text(example_preview_text.headings[2].text);
        
        //prices
        $("#price0").text(example_preview_text.prices[0].text);
        $("#price1").text(example_preview_text.prices[1].text);
        $("#price2").text(example_preview_text.prices[2].text);
        
        //descriptions
        $("#description0").text(example_preview_text.descriptions[0].text);    
        $("#description1").text(example_preview_text.descriptions[1].text);    
        $("#description2").text(example_preview_text.descriptions[2].text); 
        
        //databases
        $("#database0").text(example_preview_text.databases[0].text); 
        $("#database1").text(example_preview_text.databases[1].text);      
        $("#database2").text(example_preview_text.databases[2].text);

        //data storage
        $("#data0").text(example_preview_text.data[0].text); 
        $("#data1").text(example_preview_text.data[1].text); 
        $("#data2").text(example_preview_text.data[2].text); 
        
        //users
        $("#user0").text(example_preview_text.users[0].text); 
        $("#user1").text(example_preview_text.users[1].text); 
        $("#user2").text(example_preview_text.users[2].text); 
        
        //buttons
        $("#button0").text(example_preview_text.buttons[0].text); 
        $("#button1").text(example_preview_text.buttons[1].text);  
        $("#button2").text(example_preview_text.buttons[2].text);  
    }
```

Reload your Chrome browser to see the results of all of the sweeping changes we just made. Don't worry, it will all make sense in the next section when we start translating the text into different languages.

![After all of that work, the preview content seems to be the same.](images/customPreview5.png)

## Translating the Web Page Content

One of the key features of the First Discovery Tool is its ability to help individuals of all needs discover the preference settings that work best for him/her. Without the ability to read and understand the First Discovery Tool, it becomes useless to its users. This is why the first preference that you set is the language preference. You may have noticed that our changes didn't really seem to do anything. Think again! 

__STEP 1: Change your preferred language from English to French.__  You will see something very surprising (see below).

![The French version of the preview has no text!.](images/customPreview6.png)

If you recall, we removed the actual text and placed them in a message file called __examplePreview_en-US.json.__ The __fetch_and_insert_text()__ function in __examplePreview.html__ looks for the language code that the document has (whatever is selected on the First Discovery Tool) and concatenates it to the name of the file to see which message file its supposed to use. This would explain the odd occurrence in the picture above.  The next step is to add the translated message files for French and Spanish.

__STEP 2: Create a new file__ in __src/messages__ called __examplePreview_es-MX.json__ and __copy the following__ code into it. (This is a __translated version__ of the English one).

__examplePreview_es-MX.json__

```json
{
  "headings": [
    {
      "text": "Estándar",
      "tts": "Estándar"
    },
    {
      "text": "Medio",
      "tts": "Medio"
    },
    {
      "text": "Prima",
      "tts": "Prima"
    }
  ],
  "prices": [
    {
      "text": "$29.99",
      "tts": "Veintinueve Noventa y Nueve"
    },
    {
      "text": "$49.99",
      "tts": "Cuarenta y nueve noventa y nueve"
    },
    {
      "text": "$99.99",
      "tts": "Noventa y nueve noventa y nueve"
    }
  ],
  "descriptions": [
    {
      "text": "Una descripción impresionante",
      "tts": "Una descripción impresionante"
    },
    {
      "text": "Una descripción impresionante",
      "tts": "Una descripción impresionante"
    },
    {
      "text": "Una descripción impresionante",
      "tts": "Una descripción impresionante"
    }
  ],
  "databases": [
    {
      "text": "1 Base de datos",
      "tts": "Uno Base de datos"
    },
    {
      "text": "5 Bases de datos",
      "tts": "Cinco Bases de datos"
    },
    {
      "text": "Bases de datos ilimitadas",
      "tts": "Bases de datos ilimitadas"
    }
  ],
  "data": [
    {
      "text": "5GB de almacenamiento",
      "tts": "Cinco Gigabyte de almacenamiento"
    },
    {
      "text": "10GB de almacenamiento",
      "tts": "Diez Gigabyte de almacenamiento"
    },
    {
      "text": "Almacenamiento ilimitado",
      "tts": "Almacenamiento ilimitado"
    }
  ],
  "users": [
    {
      "text": "20 usuarios",
      "tts": "veinte usuarios"
    },
    {
      "text": "40 usuarios",
      "tts": "cuarenta Usuarios"
    },
    {
      "text": "Sin límite de usuarios",
      "tts": "Sin límite de usuarios"
    }
  ],
  "buttons": [
    {
      "text": "Compra ahora",
      "tts": "Compra ahora"
    },
    {
      "text": "Compra ahora",
      "tts": "Compra ahora"
    },
    {
      "text": "Compra ahora",
      "tts": "Compra ahora"
    }
  ]
}
```

If you save and switch the language preferences to Spanish, you should see that we managed to fix our issue! Compare with the image below. 

![Spanish Language text for the example Preview is now displaying.](images/customPreview7.png)

Now let's do the same thing for the French language preference.

__STEP 3: Create a new file__ in __src/messages__ called __examplePreview_fr-FR.json__ and __copy the following__ code into it. (This is a __translated version__ of the English one).

__examplePreview_fr-FR.json__

```json
{
  "headings": [
    {
      "text": "Standard",
      "tts": "Standard"
    },
    {
      "text": "Moyen",
      "tts": "Moyen"
    },
    {
      "text": "Prime",
      "tts": "Prime"
    }
  ],
  "prices": [
    {
      "text": "$29.99",
      "tts": "Vingt- neuf Quatre-vingt- neuf"
    },
    {
      "text": "$49.99",
      "tts": "Quarante- neuf Quatre-vingt- neuf"
    },
    {
      "text": "$99.99",
      "tts": "Un Hundren"
    }
  ],
  "descriptions": [
    {
      "text": "Une description impressionnante",
      "tts": "Une description impressionnante"
    },
    {
      "text": "Une description impressionnante",
      "tts": "Une description impressionnante"
    },
    {
      "text": "Une description impressionnante",
      "tts": "Une description impressionnante"
    }
  ],
  "databases": [
    {
      "text": "1 Base de données",
      "tts": "une base de données"
    },
    {
      "text": "5 Bases de données",
      "tts": "cinq bases de données"
    },
    {
      "text": "Bases de données illimités",
      "tts": "Bases de données illimités"
    }
  ],
  "data": [
    {
      "text": "5GB de stockage",
      "tts": "Cinq Gigabyte Stockage"
    },
    {
      "text": "10GB de stockage",
      "tts": "Dix Gigabyte Stockage"
    },
    {
      "text": "Stockage illimité",
      "tts": "Stockage illimité"
    }
  ],
  "users": [
    {
      "text": "20 utilisateurs",
      "tts": "Vingt utilisateurs"
    },
    {
      "text": "40 utilisateurs",
      "tts": "Quarante utilisateurs"
    },
    {
      "text": "utilisateurs illimités",
      "tts": "utilisateurs illimités"
    }
  ],
  "buttons": [
    {
      "text": "Acheter maintenant",
      "tts": "Acheter maintenant"
    },
    {
      "text": "Acheter maintenant",
      "tts": "Acheter maintenant"
    },
    {
      "text": "Acheter maintenant",
      "tts": "Acheter maintenant"
    }
  ]
}
```

If you save and switch the language preferences to French, you should see that we managed to fix our issue! Compare with the image below. 

![French Language text for the example Preview is now displaying.](images/customPreview8.png)


## Adding Self Voicing Functionality

Self voicing is another key aspect of the First Discovery Tool's functionality. As far as the preview is concerned, just about any or all parts of it can be voiced through the use of a combination of jquery focus/mouse events and the use of tab index on the desired elements. If you were curious to what those "tts": "value" lines in the language message files were for, they stand for "text to speech" and basically allow us to define whatever we want to be spoken similarly to how the text field was what we wanted to display.

__NOTE:__ You do not need to voice everything individually, if you want to have all of the information spoken about the deal package when the user tabs to the title of the package, you can just include everything that you want it to say in that elements "tts" field in the message file. Don't worry we will go through an example of each below.  First, lets do some prep work and set up some tab stops on the preview.

__STEP 1: Add tabindex="0"__ to the __heading elements__ in the body of __examplePreview.html.__ You can copy the code below. 

__examplePreview.html__

```html
<body>
<div class="row">
  <div class="small-4 columns">  
    <ul class="pricing-table">
      <li id="heading0" class="title" tabindex="0"></li>
      <li id="price0" class="price"></li>
      <li id="description0" class="description"></li>
      <li id="database0" class="bullet-item"></li>
      <li id="data0" class="bullet-item"></li>
      <li id="user0" class="bullet-item"></li>
      <li class="cta-button"><a id="button0" class="button radius" href="#"></a></li>
    </ul>
  </div>
  <div class="small-4 columns">  
    <ul class="pricing-table">
      <li id="heading1" class="title" tabindex="0"></li>
      <li id="price1" class="price"></li>
      <li id="description1" class="description"></li>
      <li id="database1" class="bullet-item"></li>
      <li id="data1" class="bullet-item"></li>
      <li id="user1" class="bullet-item"></li>
      <li class="cta-button"><a id="button1" class="button radius" href="#"></a></li>
    </ul>
  </div>
  <div class="small-4 columns">
    <ul class="pricing-table">
      <li id="heading2" class="title" tabindex="0"></li>
      <li id="price2" class="price"></li>
      <li id="description2" class="description"></li>
      <li id="database2" class="bullet-item"></li>
      <li id="data2" class="bullet-item"></li>
      <li id="user2" class="bullet-item"></li>
      <li class="cta-button"><a id="button2" class="button success round" href="#"></a></li>
    </ul>
  </div>
  
  </div>
<!-- Calls to the foundation Javascript files -->
<script src="https://code.jquery.com/jquery-2.1.4.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/foundation/5.5.3/js/foundation.min.js"></script>
```

This allows for users who make use of keyboard navigation to stop at these three specific elements as they go through the preview. These are the headings and will serve as our outlet to speaking the rest of the information that doesn't necessarily need to be stopped at. It is important to note that any html element that is made up of an attribute tag will also have a tab stop by design. This allows the keyboard navigators to stop at buttons and links easily.  Next, we'll need to include our __setupTts(text)__ function and include it in our __ajax__ call in the __fetch_and_insert_text()__ function.

__NOTE:__ if you need to remove a tab stop from an element, use __tabindex="-1"__

__STEP 2:  Add the setupTts(text)__ function to __examplePreview.html__ below the __insertText(electron_preview_text)__ function.

__examplePreview.html__

```javascript
    // Attach events to page elements so they can self voice when navigated to
    function setUpTts(text) {
        // The parent window contains a self voicing function from the First Discovery Tool that
        // the preview can hook into to voice itself
        var speechQueueFunction = window.parent.fluid.queryIoCSelector(window.parent.fluid.rootComponent, "gpii.firstDiscovery.selfVoicing")[0].queueSpeech;

    }
```

Basically, the First Discovery Tool has self voicing capabilities, and the preview doesn't. This means we need to make a call to the window parent to get the queueSpeech function for our uses here in the preview. We save it to a variable to save us some time when we start adding the speech cases.  Next, we need to add this functions call to the ajax success area in the __fetch_and_insert_text() function.__

__STEP 3:  Add a call to the setupTts(text) function to the fetch_and_insert_text() function under the ajax call for success. This is right after the call to insertText(data);__

__examplePreview.html__

```javascript
    // the returned json data to the function that will place strings in the UI
    function fetch_and_insert_text() {
        var langaugeCode = getLanguageCode();
        var url = '../messages/examplePreview_' + langaugeCode + ".json";
        $.ajax({
            type: 'GET',
            url: url,
            dataType: 'json',
            success: function (data) {
                insertText(data);
                setUpTts(data);
            },
            error: function (jqXHR, textStatus, errorThrown) {
                console.log("error occured: " + textStatus);
            }
        });
    }
```

__STEP 4:  Update the heading tts key:value pairs in examplePreview_en-US.json with all of the information that you want to be spoken when the user navigates to the heading.__

__examplePreview_en-US.json__

```json
  "headings": [
    {
      "text": "Standard",
      "tts": "Standard. Twenty-Nine Ninety-Nine. An awesome description. 1 Database Five Gigabyte Storage. Twenty Users."
    },
    {
      "text": "Medium",
      "tts": "Medium. Forty-Nine Ninety-Nine. An awesome description. 5 Databases. Ten Gigabyte Storage. Forty Users."
    },
    {
      "text": "Premium",
      "tts": "Premium. Ninety-Nine Ninety-Nine. An awesome description. Unlimited Databases. Unlimited Storage. Unlimited Users."
    }
  ],
```

__STEP 5:  Update the heading tts key:value pairs in examplePreview_es-MX.json with all of the information that you want to be spoken when the user navigates to the heading in Spanish.__

__examplePreview_es-MX.json__

```json
  "headings": [
    {
      "text": "Estándar",
      "tts": "Estándar. Veintinueve noventa y nueve. Una descripción impresionante. 1 Base de datos Cinco Gigabyte de almacenamiento . Veinte usuarios ."
    },
    {
      "text": "Medio",
      "tts": "Medio. Cuarenta y nueve noventa y nueve. Una descripción impresionante. 5 bases de datos . Diez Gigabyte de almacenamiento . Cuarenta usuarios ."
    },
    {
      "text": "Prima",
      "tts": "Prima. Noventa y nueve noventa y nueve. Una descripción impresionante. Bases de datos ilimitadas . Almacenamiento ilimitado. Usuarios ilimitados."
    }
  ],
```
__STEP 6:  Update the heading tts key:value pairs in examplePreview_fr-FR.json with all of the information that you want to be spoken when the user navigates to the heading in French.__

__examplePreview_fr-FR.json__

```json
  "headings": [
    {
      "text": "Standard",
      "tts": "Standard . Vingt-neuf Quatre-vingt- neuf . Une description impressionnante . 1 Base de données Cinq Gigabyte Storage . Vingt utilisateurs ."
    },
    {
      "text": "Moyen",
      "tts": "Moyen. Quarante- neuf Quatre-vingt- neuf . Une description impressionnante . 5 bases de données . Ten Gigabyte Storage . Quarante utilisateurs ."
    },
    {
      "text": "Prime",
      "tts": "Prime. Quatre-vingt- neuf Quatre-vingt- neuf . Une description impressionnante . Bases de données illimités. Stockage illimité . Utilisateurs illimités."
    }
  ],
```
__STEP 7:  Populate the setuptts(text) function using the speechQueueFuction that we setup earlier to set up jquery focus functions for the heading and the buttons on our examplePreview.html__

```javascript
    // Attach events to page elements so they can self voice when navigated to
    function setUpTts(text) {
        // The parent window contains a self voicing function from the First Discovery Tool that
        // the preview can hook into to voice itself
        var speechQueueFunction = window.parent.fluid.queryIoCSelector(window.parent.fluid.rootComponent, "gpii.firstDiscovery.selfVoicing")[0].queueSpeech;

        //Headings
        $("#heading0").focus(function () {
            speechQueueFunction(text.headings[0].tts);
        });
        $("#heading1").focus(function () {
            speechQueueFunction(text.headings[1].tts);
        });
        $("#heading2").focus(function () {
            speechQueueFunction(text.headings[2].tts);
        });
        
        //buttons
        $("#button0").focus(function () {
            speechQueueFunction(text.buttons[0].tts);
        });
        $("#button1").focus(function () {
            speechQueueFunction(text.buttons[1].tts);
        });
        $("#button2").focus(function () {
            speechQueueFunction(text.buttons[2].tts);
        });
        
        //highlight based on focus
        $("[tabindex='0']").focus(function () {
            $(this).addClass("highlighted");
        });
        $("[tabindex='0']").blur(function () {
            $(this).removeClass("highlighted");
        });
    }
```

__STEP 8:  Add a css class called highlighted to the style tag at top of the examplePreview.html page so that when  an object gets focused in our preview, that it is easier to see.__

__examplePreview.html__

```javascript
    <!-- Internal Style Sheet -->
    <style type="text/css">
        .highlighted {
            border: 5px solid yellow;
        }        
        body { 
            padding-top:50px;
        }
        #searchResults {
            background-image:url('../images/searchresult.png');
            height: 4em;
        }
        .fl-theme-bw #searchResults { background-image:url('../images/searchresult_bw.png'); }
        .fl-theme-wb #searchResults { background-image:url('../images/searchresult_wb.png'); }
    </style>
```

__STEP 9:  Turn self voicing on (on the First Discovery Tool) and then tab through or click the headings and buttons of the preview. When Activated the headings should have a large yellow border and should voice everything about the deal. The buttons should behave similarly, but without the yellow border. Compare to the image below.__

![First Dicovery Tool with highlighted preview heading with correct self voicing.](images/customPreview9.png)

## Congratulations! You Have Finished the Preview!