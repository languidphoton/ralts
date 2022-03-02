# Ralts - a 'First Contact' story downloader/processor

> This page is a 'trial balloon' set up for people on the Discord server

## What's this about?

This tool downloads and processes the _First Contact_ stories from `r/HFY`.

If you're not familiar with [HFY](https://old.reddit.com/r/HFY/), you're missing out. I'll let r/HFY introduce itself:

> We're a writing focused subreddit welcoming all media exhibiting the awesome potential of humanity, known as HFY or "Humanity, Fuck Yeah!"
> We welcome sci-fi, fantasy, and all other stories with a focus on humans being awesome!

The 'First Contact' HFY stories by `u/Ralts_Bloodthorne`, started on 25th Feb 2020 with a single quirky story about an alien who likes ice cream through to a huge corpus of 721 stories and 2,034,125 words (at the time of writing). Ralts' output has been phenomenal, sometimes posting 4 stories a day, and in the process occasionally triggering some Reddit spam filters! 

There's at least 100 characters and over 25 races in the _First Contact_ universe and it can be difficult keeping up. That's one reason for making this tool. Another one is that it's crystal clear from the comments that `ralts`'s work has helped many people get through some extraordinarily difficult times, and I don't think it's an exaggeration to say that the stories and community built up around them have saved some lives. Hopefully this tool helps that community wander through the _First Contact_ universe more easily.

The tool works in tandem with the increasingly popular [Obsidian](https://obsidian.md) knowledge base, which is sometimes touted as a 'second brain'. Obsidian hosts all files locally, is free to use and is extensible through a vibrant third-party plugins and theming community which has made some exceptional plugins.

## What does it do?

The tool downloads stories written by `u/Ralts_Bloodthorne` and processes them into [Markdown](https://en.wikipedia.org/wiki/Markdown) files which have been marked up to allow for easy linking of stories, characters, races and other items and events of interest. An example might help, this block of text:

> Herod watched as Victor stood perfectly still for a long moment, his eyes closed. Herod could see dozens of VR versions of the human moving at high speed through the VR spaces of  the Black Box and knew that the thousands of clones of Victor/Dhruv were working hard even as Legion stood stock still in the middle of the room with his eyes closed.

is converted into this:

>[[Herod]] watched as [[Legion|Victor]] stood perfectly still for a long moment, his eyes closed. [[Herod]] could see dozens of VR versions of the human moving at high speed through the VR spaces of  the Black Box and knew that the thousands of clones of [[Legion|Victor]]/[[Legion|Dhruv]] were working hard even as [[Legion]] stood stock still in the middle of the room with his eyes closed.

The `[[Herod]]` code is the Obsidian method of linking to a page called 'Herod' and the `[[Legion|Victor]]` code means that the word 'Victor' is shown as the link text, whilst the link is going to the page called 'Legion'. You might ask "who's this guy Legion and why is he known by so many names?". Well, that would be telling...

This is what it eventally looks like in Obsidian, the underlined text goes to pages about the characters, the 'Herod' link goes to one page, and the 'Victor', 'Dhruv' and 'Legion' links all go the same page, 'Legion':

![Herod and Legion/Victor/Dhruv](assets/herod_and_legion.png)

Talking of screenshots...

## What does the output look like?

### Story listing

This page shows all the stories that have been processed. It's based on the `dataview` plugin of Obsidian, which has some SQL-like properties which can use metadata from each story, such as the story 'Score', 'Wordcount' and the date the story was 'Published' to create dynamic lists as shown below.

![all stories](assets/all_stories.png)

### Reading a single story
The character 'Speaks' is highlighted, showing that there's more information available about them, such as all the stories they appear in. You can navigate between the previous and next story quite easily, and as you can see from the text, there's a *lot* of action in _First Contact_ stories.
![single-story](assets/story_overview.png)

### Detailed information about a story
The 'Information about this story....' block links to the main characters in this particular story, along with races present, and the races of those characters.
![story detail](assets/story_detail.png)

There's also a lot of metadata in a story, and part of that is shown below. It's particularly useful when used in conjunction with Obsidian and the `dataview` plugin in particular.
![metadata](assets/metadata.png)

### Character detail
We clicked on 'Daxin' from the last screen. Here's some background information on him, and what stories he's either in, or mentioned in. For Daxin, that's a lot.
![Daxin detail](assets/daxin.png)


### Themes, themes, themes...
[Obsidian](https://obsidian.md) has a huge theme collection, the screenshots above are the 'Dracula' theme, this is the default Obsidian light theme.

It's also extensively configurable, so you're bound to find something you like. If you find one that works better for _First Contact_, please share it!
![default light theme](assets/default_theme.png)

## I'm sold, gimme!

As they used to say on the box, there's _some assembly required_. 

The code is written in python3, and you'll need to install some additional libraries to make it work.

### Installing

Clone this repository into a folder, you'll end up with this
```
README.md
assets
ralts.py
datastructs.py
novaspark.py
```

The main program is `ralts.py`, and you'll interact with this most of the time. `datastructs.py` holds definitions of who is a main character, their aliases if they have any, what race they are a part of, planets and other objects of interest. `novaspark.py` is optional, but it's very helpful to create (and delete) stub files for the over 100 characters ralts has created, as well as races and objects of interest. It's called `novaspark.py` to warn you it has some power...



```
% python3 pip install -r requirements.txt

# or you can install the modules separately
% python3 pip install pathlib docopt PyYAML rich bdfr
```

The `bdfr` module is a multi-purpose Reddit post downloader, and loads in quite a few other modules. 

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
    blueberries     Gets the last <storycount> stories, processes them and copies them to your cloud folder

Options:
    -all                Process/Download all stories [default: False]
    --storycount=<ns>   Number of stories to process/download
    --search=str        Only process stories whose title matches str (case sensitive)
    --config=file       Load this configuration file [default: config/config.yml]
    -h --help           Show this screen
    -d --debug          Show some debug information [default: False]
    --version           Show version [default: __version__]
```

If you've read the _First Contact_ stories you'll understand why I've chosen `suds`, `mattrans` and `blueberries` for commands, if you haven't then it's something else to look forward to.

An initial run might look something like:

```
# download the posts from Reddit

% ./ralts.py mattrans --all
This is the first time running ralts.py. 
Setting up a default configuration in config/config.yml. Change parameters to your
liking and re-run.
Configuration file config/config.yml newly written. Exiting...

# now the config file is created
% ./ralts.py mattrans --all
Reading from config file: config/config.yml
You're going to download 700+ stories, sure? [y/n]: 

```