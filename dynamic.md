---
layout: post
title: test
description: test
image: assets/images/pic33.jpg
nav-menu: true
---

markdown content example


<h1 id="dynamicTitle">Welcome to my site!</h1>
<p id="dynamicDescription">This is my site where I...</p>


<script>
  // Array of catch phrases for title
  var titlePhrases = [
    "Acorn.io Artisan!",
    "Ambassador Ace!",
    "Architect Aficionado!",
    // Add all your title phrases here
  ];

  // Array of catch phrases for description
  var descriptionPhrases = [
    "Insights on my approach as an Acorn.io Artisan!",
    "Learn more about my work as an Ambassador Ace!",
    "Discover my methodology as an Architect Aficionado!",
    // Add all your description phrases here
  ];

  // Function to change the catch phrase
  function changeCatchPhrase() {
    // Get a random index for title and description
    var titleIndex = Math.floor(Math.random() * titlePhrases.length);
    var descriptionIndex = Math.floor(Math.random() * descriptionPhrases.length);

    // Get the catch phrases
    var titlePhrase = titlePhrases[titleIndex];
    var descriptionPhrase = descriptionPhrases[descriptionIndex];

    // Change the content of the title and description elements
    document.getElementById('dynamicTitle').textContent = titlePhrase;
    document.getElementById('dynamicDescription').textContent = descriptionPhrase;
  }

  // Change the catch phrase every 5 seconds
  setInterval(changeCatchPhrase, 5000);
</script>

