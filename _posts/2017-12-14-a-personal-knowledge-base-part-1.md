---
layout: post
title: "A Personal Knowledge Base - part 1"
categories: projects
author: "Mangala Kodagoda"
meta: "Personal Knowledgebase"
---

A personal knowledge base (PKB) is useful to capture, record and access personalized information on demand. Being a knowledge worker, I needed a PKB to record bits of knowledge I learn from various sources and access that knowledge from (almost) anywhere. I do want to make a distinction about generic information, and learned knowledge (i.e. concepts, theories, techniques etc.) here. Because I've been using [Evernote](https://www.evernote.com/) for some time now, and it has served me very well to keep personal notes and access them from multiple devices. But I find wiki to be the ideal solution to interlink multiple 'concepts' and combining them to build complex ideas.

I found [this post](http://www.acuriousmix.com/2014/09/03/designing-a-personal-knowledgebase/) by Alex to be a valuable discussion on what a good PKB should support. Inspired by that post I came up with a set of requirements for a PKB that suites me. Following are those high level objectives:

- Repository to record, categorize and search information.
   - Should be able to create content with multiple formats like text, image, video etc.

- Ability to link multiple pages in such a way that it is easy to browse related information.
  - Categorize pages with tags, and ability to search content given the tag(s).

- Public read-only access from anywhere, any device.
  - Repository should be open to public for reading, so I can share content with friends, colleagues etc.

- Authorized write access from anywhere, any device.
  - Only authorized personal should be able to edit the repository. Furthermore, I personally use number of devices in my learning process. May it be the personal computer, office laptop, smartphone or the Kindle; it should be easy to record new information I just learned from those devices.

If you've read Alex's blog post I mentioned earlier, you will agree with his emphasis on needing *minimal effort to capture* content. Along the lines of this I wanted the support to record content from a Kindle at some point in time. For example: I want to send highlighted text and/or notes from my Kindle to the PKB as new content along with references and tags. But since that device is for content consumption and not for content creation, I will probably need a mediator to handle the request to the PKB. This seemed a complex enough problem of its own, so I've decided to handle that at a later time.

Last but not least, I didn't want to commit to a commercial product; thus limited the search to free or cheap options :-).

After considering multiple options, I've finally settled with [TiddlyWiki](https://tiddlywiki.com/) as the core of the solution. TiddlyWiki is a non-linear notebook for capturing, organizing and sharing information. Being a wiki, it already can interlink related content and access from any device with a web browser and an internet connection (Unless blocked by a firewall of course). There are primarily two flavors of TiddlyWiki. 'TiddlyWiki5' (TW5) runs on nodejs while 'TiddlyWiki Classic' is a single HTML file solution. It seemed the single file solution might suffer in load and response time when the amount of content grow. Therefore I've favored the nodejs version.

Following is an excerpt from TiddlyWiki's [philosophy declaration](https://tiddlywiki.com/#Philosophy%20of%20Tiddlers).

> The purpose of recording and organising information is so that it can be used again. The value of recorded information is directly proportional to the ease with which it can be re-used.
>
> The philosophy of tiddlers is that we maximise the possibilities for re-use by slicing information up into the smallest semantically meaningful units with rich modelling of relationships between them. Then we use aggregation and composition to weave the fragments together to present narrative stories.

Ideally a 'tiddler' is a bite size semantically meaningful knowledge unit. Multiple tiddlers can be opened in the same view instead of replacing the existing page or opening a new browser tab. I assume this is what they mean by: *'use aggregation and composition to weave the fragments together to present narrative stories'*.

Setting up a local TiddlyWiki5 server is pretty straight forward. TiddlyWiki site contains generous amount of information on that. Information on hosting it publicly to make it accessible from any device, however was little confusing. Multiple sources have discussed these various options and I've listed down few of those sources that are worth mentioning.

- [Expected workflow for self-hosting a TiddlyWiki5](https://groups.google.com/forum/#!topic/tiddlywiki/spmnlUycjSo)
- [Hosting Via nodejs Or store.php?](http://tobibeer.github.io/tb5/#Hosting%20Via%20node.js%20Or%20store.php%3F)
- [Reddit - TiddlyWiki5 hosting](https://www.reddit.com/r/TiddlyWiki5/wiki/index/hosting)

Following is summarization of those options along with their pros and cons from my perspective.

1. Personal nodejs server with tiddlers saved on cloud (e.g. Dropbox, OneDrive etc.)
2. Public nodejs hosting
3. A hybrid of personal nodejs server and static HTML hosting.

Option 1 requires the viewing device to run nodejs and have access to the cloud storage. This is not possible in some office computers due to restrictions on software installation and cloud share. Therefore, this wasn't really an option for me since I want my PKB to be accessible by office computers also.

Option 2 doesn't have this problem since the server itself is publicly hosted. But the current version of TW5 doesn't support authentication for read-only vs. edit access. There are couple of tickets to track this feature requirement (i.e. [Issue 1276](https://github.com/Jermolene/TiddlyWiki5/issues/1276), [Issue 1213](https://github.com/Jermolene/TiddlyWiki5/issues/1213)). Without this I didn't find a way to support the last two high level objectives. Furthermore, nodejs hosting doesn't come cheap. But there is a good [tutorial](https://ericmiao.github.io/blog/2014/04/05/setup-personal-tiddlywiki-on-openshift/) on setting up a TW5 in OpenShift's free pricing category. Anyhow, I decided to let go of this option until I find a way to support authentication in TW5. This left me with option 3.

Option 3 is a compromise. The solution is to have a local TW5 server where you can edit the wiki. Then export a snapshot of the wiki to a static HTML file and upload that to a hosting site like [GitHub Pages](https://pages.github.com/). This have few drawbacks. As I mentioned previously, the single HTML file size will grow along with your wiki content and might result in increased the loading time. But since I need to start somewhere I ignored this potential drawback for the moment. This option doesn't support *authorized write access from anywhere* also. However, you can edit the wiki online and save a local copy as an HTML page. But to update your editable TW5 with those changes, you might need to do some copy-pastings on your pc running the nodejs server. The good news is that without access to the hosting server nobody can edit your wiki.

I also want to share the details of how the option 3 solution was implemented. But this deserves a post on its own. Therefore, I will do a follow up post on that. You can visit my current PKB at: [manga.la/wiki](http://manga.la/wiki/).
