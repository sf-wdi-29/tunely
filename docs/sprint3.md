# Sprint 3

## Overview

This sprint we will:
* add an embedded model to our Album model
* change the UI to allow users to see songs in the embedded model


> Note: as we go through this if you get stuck make use of the hints, your neighbors and the solutions.

> You must complete all of the previous sprint before starting this sprint. (excludes stretch challenges)

In this step we'll be changing our Album schema to have an embedded schema that contains songs.

The data from the database will look a little like this:

```js
{ genres: [ 'new wave', 'indie rock', 'synth pop' ],
    songs:
     [ { _id: 5665ff1678209c64e51b4e6a,
         length: 240,
         trackNumber: 1,
         name: 'Swamped' },
       { _id: 5665ff1678209c64e51b4e64,
         length: 255,
         trackNumber: 7,
         name: 'Tight Rope' } ],
    _id: 5665ff1678209c64e51b4e63,
    releaseDate: '2008, November 18',
    name: 'Comalies',
    artistName: 'Lacuna Coil',
    __v: 0 },
```

* note that `songs` has been added and is an array of other records!


## Step 1: Create the new model

1. Create a `models/song.js`

1. Open the file and create a model with properties like:

```js
  name: String,
  trackNumber: Number,
  length: Number  // of seconds
```

1. Export the module and require it in `models/index.js`

1. Require `./song.js` in `./albums.js`

1. Alter the schema of Album to have a songs array that uses the `Song.schema`

## Step 2: Seeding

Let's add seeds.  Some basic data is [provided for you](/docs/assets/sprint3_song_seeds.js).
We're going to use this data for all albums for now, even though it's not accurate.

1. Copy the sample songs into `seed.js`

1. Write a `forEach` loop that adds the sample songs to each sampleAlbum in `seed.js`.  Compare your work to the sample above.

1. Add a better `console.log` to the `db.Album.create` callback.  Let's `console.log(albums)` just before exiting, that way we can see that they're all created.  

1. `node seed.js`

1. Fix any issues you encounter until you can see that it's also adding songs for each album.

## Step 3: display

Let's go back to `app.js` and our html.  If you check the output of your AJAX call, you should see that we're already retrieving songs with each album.  Double-check this before you proceed.  

We'll change the client to add another `<li>` after the ones that are already being generated for each album.  We'll list our songs in there.
For now we're just going to make this super simple and output something like:

```html
<li class="list-group-item">
  <h4 class="inline-header">Songs:</h4>
  <span>	– (1) Swamped – (2) Heaven's a Lie – (3) Daylight Dancer – (4) Humane – (5) Self Deception – (6) Aeon – (7) Tight Rope – </span>
</li>
```


1. In `app.js`, create a new function `function buildSongsHtml(songs) {}`

1. Make buildSongsHtml return the HTML shown above (or similar).  It should take in an **array of songs**.  It should return an **HTML string**.

<details><summary>Hint: making a long dash &ndash; </summary>
Use `&ndash;`
</details>

<details><summary>Hint: `function buildSongsHtml(songs) {}`</summary>
```js  
  function buildSongsHtml(songs) {
    var songText = "	&ndash; ";
    songs.forEach(function(song) {
      songText = songText + "(" + song.trackNumber + ") " + song.name + " &ndash; ";
    });
  var songsHtml  =
    "                      <li class='list-group-item'>" +
    "                        <h4 class='inline-header'>Songs:</h4>" +
    "                         <span>" + songText + "</span>" +
    "                      </li>";
    return songsHtml;
  }
```
</details>

1. Now call `buildSongsHtml` from inside `renderAlbum`. Use it to add the 4th `<li>` to each album.