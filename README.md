# 'First Contact' story downloader/processor

## What's this about?

If you're not familiar with [HFY](https://old.reddit.com/r/HFY/), you're missing out. I'll let r/HFY introduce itself:

> We're a writing focused subreddit welcoming all media exhibiting the awesome potential of humanity, known as HFY or "Humanity, Fuck Yeah!"
> We welcome sci-fi, fantasy, and all other stories with a focus on humans being awesome!

The 'First Contact' HFY stories by `u/Ralts_Bloodthorne`, which started on 25th Feb 2020 with a quirky story about an alien who likes ice cream has developed through a phenomenal output, sometimes 4 stories a day, into a huge corpus of 721 stories and 2,034,125 words (at the time of writing). 

There's at least 100 characters and over 25 races in the First Contact universe and it can be difficult keeping up. That's one reason for making this tool. Another one is that it's crystal clear from the comments that `ralts`'s work has helped some people get through some extraordinarily difficult times, and I don't think it's an exaggeration to say that the stories have saved some lives.

The tool works in tandem with the [Obsidian](https://obsidian.md) knowledge base, which is sometimes touted as a 'second brain'. Obsidian is extensible through a vibrant third-party plugins and theming community which has made some exceptional plugins.

## What does it do?

The tool downloads stories written by `u/Ralts_Bloodthorne` and processes them into [Markdown](https://en.wikipedia.org/wiki/Markdown) files which have been marked up to allow for easy linking of stories, characters, races and other items and events of interest. An example might help, this block of text:

> Herod watched as Victor stood perfectly still for a long moment, his eyes closed. Herod could see dozens of VR versions of the human moving at high speed through the VR spaces of  the Black Box and knew that the thousands of clones of Victor/Dhruv were working hard even as Legion stood stock still in the middle of the room with his eyes closed.

is converted into this:

>[[Herod]] watched as [[Legion|Victor]] stood perfectly still for a long moment, his eyes closed. [[Herod]] could see dozens of VR versions of the human moving at high speed through the VR spaces of  the Black Box and knew that the thousands of clones of [[Legion|Victor]]/[[Legion|Dhruv]] were working hard even as [[Legion]] stood stock still in the middle of the room with his eyes closed.

The `[[Herod]]` code 's the Obsidian method of linking to a page called 'Herod' and the `[[Legion|Victor]]` code means that the word 'Victor' is shown as the link text, whilst the link is going to the page called 'Legion'. You might ask "who's this guy Legion and why is he known by so many names?". Well, that would be telling...

This is what it looks like in Obsidian, the underlined text goes to pages about the characters:
![Herod and Legion/Victor/Dhruv](assets/herod_and_legion.png)

Talking of screenshots...

## What does the output look like?

### All stories

This page shows all the stories that have been processed.

![all stories](assets/all_stories.png)

### A single story
With a character, 'Speaks' highlighted, showing that there's more information available about them. You can navigate between the previous and next story quite easily, and as you can see from the text, there's a *lot* of action in 'First Contact' stories.
![single-story](assets/story_overview.png)

### Detailed information
The 'Information about this story....' block links to the main characters in this particular story, along with races present, and the races of those characters.
![story detail](assets/story_detail.png)

There's also a lot of metadata in a story, and part of that is shown below. It's particularly useful when used in conjunction with Obsidian.
![metadata](assets/metadata.png)

### Character detail
We clicked on 'Daxin' from the last screen. Here's some background information on him, and what stories he's either in, or mentioned in. For Daxin, that's a lot.
![Daxin detail](assets/daxin.png)

### Themes, themes, themes...
[Obsidian](https://obsidian.md) has a huge theme collection, the screenshots above are the 'Dracula' theme, this is the default Obsidian light theme.

It's also extensively configurable, so you're bound to find something you like. If you find one that works better for 'First Contact', please share it!
![default light theme](assets/default_theme.png)

## I'm sold, gimme!

As they used to say on the box, there's _some assembly required_. 

Here's the output of the `./ralts.py -h` command:

```
-> ./ralts.py -h
Process Ralts_Bloodthorne stories (primarily the r/HFY posts)

Builds an Obsidian (https://obsidian.md) 'vault' which makes it much easier to
wander around the marvellous "First Contact" multiverse created by 
https://www.reddit.com/user/Ralts_Bloodthorne/

Characters such as 'Daxin' are expanded out to [[Daxin]] so that Obsidian can 
create a web of stories and interactions.
If a character is referred to by an alias, eg 'Luke', this is also expanded so
that the alias is shown, but the link refers to the canonical name, eg [[Legion|Luke]].

This expansion is done for races and the members of those races too, so that if
'Vuxten' appears in a story he's made linkable, as [[Vuxten]], flagged as a main
character and then it's noted that a [[Telkan]] is in the story.

You can then find all the stories where 'Vuxten' appears or where 'Terrans'
or 'Atrekna' are mentioned - that's all done within Obsidian, using a 
plugin called 'dataview'.

It's also done for key phrases, such as 'LARP', 'Precursor' and
'Wrathful Mercury'.

The characters, races etc. are all extensible in the 'datastructs.py' file.

Usage:
    ralts.py suds [--all | --storycount=<ns> | --search=str] [-d] [--config=file]
    ralts.py cloud [-d] [--config=file]
    ralts.py mattrans [--all | --storycount=<ns>] [-d] [--config=file]
    ralts.py blueberries [-d] [--config=file]
    ralts.py (-h | --help)
    ralts.py --version

Commands:
    suds            Process stories and add Obsidian features ([[ ]] etc)
    cloud           Synchronise local Obsidian files with your cloud provider folder
    mattrans        Download posts by u/Ralts_Bloodthorne from Reddit. Not just from HFY!
    blueberries     Gets the last 5 stories, processes them and copies them to your cloud folder

Options:
    -all                Process/Download all stories [default: False]
    --storycount=<ns>   Number of stories to process/download
    --search=str        Only process stories whose title matches str (case sensitive)
    --config=file       Load this configuration file [default: config/config.yml]
    -h --help           Show this screen
    -d --debug          Show some debug information [default: False]
    --version           Show version [default: __version__]
```

If you've read the 'First Contact' stories you'll understand why I've chosen `suds`, `mattrans` and `blueberries` for commands, if you haven't then it's something else to look forward to.