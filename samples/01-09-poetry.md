---
title: "Poetry"
---

## Poetry

First, a bit of background about how we like to mark up poetry. This will help you understand what you're looking at when we get to the samples below.

Also see the official [docs on poetry](https://electricbookworks.github.io/electric-book/docs/editing/poetry.html).

Encoding poetry can be tricky. Usually, poetry in HTML is structured by tagging each stanza as a paragraph, with line breaks after each line. You can do this by adding markdown line breaks (with double spaces or `\\` at the end of each line) and tagging the paragraph with `{:.verse}`. However, this structure makes it impossible to have browsers, ereaders and PDF engines correctly indent runover lines (because there is no [`nth-line` selector](https://css-tricks.com/a-call-for-nth-everything/) in CSS, unless you resort to [a Javascript method](https://github.com/davatron5000/Lettering.js#letters-words-lines-and-more) that will bloat your code and won't run on many ereaders).

> Tech note: Some text and code editors (e.g. Atom) strip out spaces at the ends of lines automatically. So use `\\` for line breaks, not double-spaces.
{:.box}

We prefer another approach: the poem is an unordered list (`ul`) and each line (including each blank line between stanzas) is a list item (`li`). We just hide any list markers (bullets) with `list-style-type: none`. This way, we can control indents on runover lines. This is a non-semantic use of HTML, since a poem is technically not a list. But it's a healthy hack with universal browser and ereader support.

Our convention is to mark each line of a stanza with a hyphen `-`, and tag the list with `{:.verse}`:

~~~
-   I wandered lonely as a cloud
-   That floats on high o'er vales and hills,
-   When all at once I saw a crowd,
-   A host, of golden daffodils;
-   Beside the lake, beneath the trees,
-   Fluttering and dancing in the breeze.
{:.verse}
~~~

This gives us:

-   I wandered lonely as a cloud
-   That floats on high o'er vales and hills,
-   When all at once I saw a crowd,
-   A host, of golden daffodils;
-   Beside the lake, beneath the trees,
-   Fluttering and dancing in the breeze.
{:.verse}

We can also indent individual lines, where the poet wanted indents, by tagging individual list items.

~~~
-   Alas for man! day after day may rise,
-   {:.indent-3}Night may shade his thankless head,
-   He sees no God in the bright, morning skies
-   {:.indent-3}He sings no praises from his guarded bed.
{:.verse}
~~~

The `2` in `{:.indent-2}` refers to the number of em spaces to indent by. Our CSS allows for indents from 1 (`{:.indent-1}`) to 30 (`{:.indent-30}`).

This gives us:

-   Alas for man! day after day may rise,
-   {:.indent-3}Night may shade his thankless head,
-   He sees no God in the bright, morning skies
-   {:.indent-3}He sings no praises from his guarded bed.
{:.verse}

Big gaps between words in a line must be created with spaces or space entities like `&emsp;` in the poem text.

## Centering poems

But wait, there's more! Best practice for poetry layout is that – in print – a poem should be centered on its longest line. That is *not* centering the lines of poetry, but placing the left-justified poem in the horizontal middle of the page. Put another way, the poem should be indented till its longest line is centered on the page.

To achieve this, put the entire poem, including its title, in a blockquote, by adding `> ` to the start of each line. Tag the whole blockquote as `{:.verse}`, too. Finally, decide how wide you want the poem to as a percentage of the page width. That is, if you reckon this poem's longest line reaches across 90 per cent of the page, use `.width-90`.

~~~
> - ### To One Who Has Been Long in City Pent
> - To one who has been long in city pent,
> - {:.indent-2}'Tis very sweet to look into the fair
> - {:.indent-2}And open face of heaven,—to breathe a prayer
> - Full in the smile of the blue firmament.
> - Who is more happy, when, with heart's content,
> - {:.indent-2}Fatigued he sinks into some pleasant lair
> - {:.indent-2}Of wavy grass, and reads a debonair
> - And gentle tale of love and languishment?
> -    
> - Returning home at evening, with an ear
> - {:.indent-2}Catching the notes of Philomel,—an eye
> - Watching the sailing cloudlet's bright career,
> - {:.indent-2}He mourns that day so soon has glided by:
> - E'en like the passage of an angel's tear
> - {:.indent-2}That falls through the clear ether silently.
> {:.verse}
{:.verse .width-80}
~~~

In verse structured as a list like this, our CSS preserves white space. That is, if you type, say, three spaces you get three spaces. Normally, HTML collapses multiple spaces into one – which is great *except* when you want to deliberately use extra spaces, as some poets do. However, this doesn't work at the start of lines, where markdown strips leading spaces. There you must use HTML space entities (like `&emsp;`) or our indent tags explained above.

**However**, the `whitespace: pre-wrap` CSS we use for this is not currently supported on Kindle. If that's important, it's best to stick to using HTML space entities like `&emsp;`.

Here's that poem rendered:

> - #### To One Who Has Been Long in City Pent
> - To one who has been long in city pent,
> - {:.indent-2}'Tis very sweet to look into the fair
> - {:.indent-2}And open face of heaven,—to breathe a prayer
> - Full in the smile of the blue firmament.
> - Who is more happy, when, with heart's content,
> - {:.indent-2}Fatigued he sinks into some pleasant lair
> - {:.indent-2}Of wavy grass, and reads a debonair
> - And gentle tale of love and languishment?
> - 
> - Returning home at evening, with an ear
> - {:.indent-2}Catching the notes of Philomel,—an eye
> - Watching the sailing cloudlet's bright career,
> - {:.indent-2}He mourns that day so soon has glided by:
> - E'en like the passage of an angel's tear
> - {:.indent-2}That falls through the clear ether silently.
> {:.verse}
{:.verse .width-80}

Here's a long poetry example.

> - #### Gerontion
> - {:.indent-1}Thou hast nor youth nor age
> - {:.indent-1}But as it were an after dinner sleep
> - {:.indent-1}Dreaming of both.
> - 
> - Here I am, an old man in a dry month,
> - Being read to by a boy, waiting for rain.
> - I was neither at the hot gates
> - Nor fought in the warm rain
> - Nor knee deep in the salt marsh, heaving a cutlass,
> - Bitten by flies, fought.
> - My house is a decayed house,
> - And the jew squats on the window sill, the owner,
> - Spawned in some estaminet of Antwerp,
> - Blistered in Brussels, patched and peeled in London.
> - The goat coughs at night in the field overhead;
> - Rocks, moss, stonecrop, iron, merds.
> - The woman keeps the kitchen, makes tea,
> - Sneezes at evening, poking the peevish gutter.
> - 
> - {:.indent-8}I an old man,
> - A dull head among windy spaces.
> - 
> - Signs are taken for wonders. "We would see a sign":
> - The word within a word, unable to speak a word,
> - Swaddled with darkness. In the juvescence of the year
> - Came Christ the tiger
> - 
> - In depraved May, dogwood and chestnut, flowering Judas,
> - To be eaten, to be divided, to be drunk
> - Among whispers; by Mr. Silvero
> - With caressing hands, at Limoges
> - Who walked all night in the next room;
> - By Hakagawa, bowing among the Titians;
> - By Madame de Tornquist, in the dark room
> - Shifting the candles; Fraulein von Kulp
> - Who turned in the hall, one hand on the door. Vacant shuttles
> - Weave the wind. I have no ghosts,
> - An old man in a draughty house
> - Under a windy knob.
> - 
> - After such knowledge, what forgiveness? Think now
> - History has many cunning passages, contrived corridors
> - And issues, deceives with whispering ambitions,
> - Guides us by vanities. Think now
> - She gives when our attention is distracted
> - And what she gives, gives with such supple confusions
> - That the giving famishes the craving. Gives too late
> - What's not believed in, or if still believed,
> - In memory only, reconsidered passion. Gives too soon
> - Into weak hands, what's thought can be dispensed with
> - Till the refusal propagates a fear. Think
> - Neither fear nor courage saves us. Unnatural vices
> - Are fathered by our heroism. Virtues
> - Are forced upon us by our impudent crimes.
> - These tears are shaken from the wrath-bearing tree.
> - 
> - The tiger springs in the new year. Us he devours. Think at last
> - We have not reached conclusion, when I
> - Stiffen in a rented house. Think at last
> - I have not made this show purposelessly
> - And it is not by any concitation
> - Of the backward devils.
> - I would meet you upon this honestly.
> - I that was near your heart was removed therefrom
> - To lose beauty in terror, terror in inquisition.
> - I have lost my passion: why should I need to keep it
> - Since what is kept must be adulterated?
> - I have lost my sight, smell, hearing, taste and touch:
> - How should I use it for your closer contact?
> - 
> - These with a thousand small deliberations
> - Protract the profit of their chilled delirium,
> - Excite the membrane, when the sense has cooled,
> - With pungent sauces, multiply variety
> - In a wilderness of mirrors. What will the spider do,
> - Suspend its operations, will the weevil
> - Delay? De Bailhache, Fresca, Mrs. Cammel, whirled
> - Beyond the circuit of the shuddering Bear
> - In fractured atoms. Gull against the wind, in the windy straits
> - Of Belle Isle, or running on the Horn,
> - White feathers in the snow, the Gulf claims,
> - And an old man driven by the Trades
> - To a sleepy corner.
> - 
> - {:.indent-8}Tenants of the house,
> - Thoughts of a dry brain in a dry season.
> {:.verse}
{:.verse}
