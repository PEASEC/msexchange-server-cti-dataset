# msexchange-server-cti-dataset

This repository hosts the new specialized CTI dataset annotated by three experts and based on the 2021 Microsoft Exchange Server data breach.

Further explanations contains the paper Multi-Level Fine-Tuning, Data Augmentation, and Few-Shot Learning for Specialized Cyber Threat Intelligence [1].

1: Bayer, Frey and Reuter (2022) Multi-Level Fine-Tuning, Data Augmentation, and Few-Shot Learning for Specialized Cyber Threat Intelligence,

If you want to make use of the dataset, please cite the following paper.

# Citing

```
@misc{https://doi.org/10.48550/arxiv.2207.11076,
  doi = {10.48550/ARXIV.2207.11076},
  url = {https://arxiv.org/abs/2207.11076},
  author = {Bayer, Markus and Frey, Tobias and Reuter, Christian},
  keywords = {Cryptography and Security (cs.CR), Computation and Language (cs.CL), FOS: Computer and information sciences, FOS: Computer and information  sciences},
  title = {Multi-Level Fine-Tuning, Data Augmentation, and Few-Shot Learning for Specialized Cyber Threat Intelligence},
  publisher = {arXiv},
  year = {2022},
  copyright = {arXiv.org perpetual, non-exclusive license}
}
```
# Dataset explanation
The dataset was split into a full and few-shot training set and development set. The splits (train, dev) consist of 1800 and 600 instances for the full set and 32 and 32 instances for the few-shot set, respectively. The test set is the same in both cases and consists of 601 instances.

![Dataset_split_counted](https://user-images.githubusercontent.com/47971884/229718175-c8a241c4-bb0c-4bf2-9434-8e155d006fbf.png)


We used the Twitter APIv2 to gather Tweets in March that fulfill the query “Microsoft Exchange” OR “MS Exchange” OR “CVE-2021-26855” OR “CVE- 2021-26857” OR “CVE-2021-26858” OR “CVE-2021-27065”. For these Tweets we resolved the links that were shortened by Twitter, as the full URLs might be an important indicator in the context of CTI.\
The labeling process of the data was performed by three cybersecurity experts guided by a codebook. The guidelines, which provide clear guidance on when to mark a contribution as relevant or irrelevant, were updated iteratively by the annotation leader. A first draft was developed using the CTI concept (McMillan, 2013):
```
Threat intelligence is referred to as the task
of gathering evidence-based knowledge, including
context, mechanisms, indicators, implications,
and actionable advice, about an existing
or emerging menace or hazard to assets that can
be used to inform decisions regarding the subject’s
response to that menace or hazard.
```

In the directory external is also the dataset from the following paper included: CySecAlert: An Alert Generation System for Cyber Security Events Using Open Source Intelligence Data [1].

1: Riebe, Wirth, Bayer, Kühn, Kaufhold, Knauthe, Guthe and Reuter (2021) CySecAlert: An Alert Generation System for Cyber Security Events Using Open SourceIntelligence Data, Proceedings of 23rd International Conference, ICICS 2021, Chongqing, China.

# Labeling

The codebook for the labeling process was iteratively developed (more can be read on this in the paper). The following codebook was finally used for the labeling:


> ## Annotation Guidelines
> Put yourself in the role of a cybersecurity expert who has received initial information about a Microsoft Exchange incident. Since the information is relatively new, you want to gain further insight by looking at some Twitter posts. You search Twitter with some keywords regarding Microsoft Exchange. As you notice that many posts are not insightful you start to annotate the posts in terms of their relevance to you.
> #### Do not only consider the text but also the referenced websites.
> - - -
> What is labeled as **Relevant**?
> * Timely information that might be good to know for cybersecurity experts
> * Specific information about the vulnerabilites, how to perform them, how to mitigate them, what an attacker can do with exploiting the vulnarability ..
> * Expliticly mentioned numbers, methods, proof of concepts, code, fixes
> * Tweets that include IOCs (IPs, Hash values, usw.), or exploits (DearCry)
> * Relevant information is more valuable than irrelevant information - if a post contains both relevant and irrelevant information, it is to be labeled as relevant
>     * For example "As of March 8, over 30K servers in the US have been hit by the recent Exchange #zero-day attack, which leaves behind a web shell that allows hackers to access the server to steal data & install malware" -> Relevant
>     
> What is labeled as **Not Relevant**?
> * Information that is too general
> * Information regarding the scope (which authorities, business branches and how many)
>     * This then includes posts about how many servers have not been patched yet, for example, or the following: „Microsoft Exchange Server attacks: 'They're being hacked faster than we can count', says security company“
>     * Likewise this refers to posts like „The European Banking Authority said it had been a victim of a cyberattack targeting its Microsoft Exchange Servers” -> Not relevant
>     * But on the other hand, a post like "RT Researchers have acquired a list of 86,000 IP addresses of MS Exchange servers infected worldwide by the mass compromises" is still relevant, as the IP list would be of interest.
> * If a post only links to a page without really providing information, it should be marked as not relevant, even if the linked page contains important information. Above all, a post should be marked as not relevant if it is not exactly clear what to expect on the page. Otherwise, when, for example, the text says that it is IOC info or a security advisory, you can consider it relevant (or check the page again). Please still consider the following examples:
>     * “GovInfoSecurity \| Analysis: Microsoft Exchange Server Hacks https://bit\.ly/2QgZb9P” \-\> not relevant \(too inaccurate\)
>     * “Chile's bank regulator shares IOCs after Microsoft Exchange hack https://ift.tt/3lrnfm3” -> Relevant (IOCs are very interesting for security experts)
>     * “Here's what we know so far about the massive Microsoft Exchange hack https://www.wxii12.com/article/here-s-what-we-know-so-far-about-the-massive-microsoft-exchange-hack/35793771?utm\_campaign=snd-autopilot” -> not Relevant (really no information in the text; too vague what to expect on the page)
>     * "RT How the Microsoft Exchange hack could impact your organization https://tek.io/2Oieqi5(https://t.co/un4YdQkbA3)" -> Not Relevant (too inaccurate)
>     * “CISA Updates Microsoft Exchange Advisory to Include China Chopper https://dlvr.it/RvhdjL” -> Relevant (You know what to expect on the site; besides, CISA is a major player)
>     * “At Least 10 Hacking Groups Are Exploiting Microsoft Exchange Server Flaws [PCMag] https://best.photography/articles/543893/at-least-10-hacking-groups-are-exploiting-microsoft-exchange-server-flaws/” -> Not Relevant (sounds relevant at first, because possibly the 10 hacking groups are mentioned and they are possibly known. However, the link is not trustworthy and also not callable) – relevant would have been fine here too, especially if the link was not strange.
>     * „It really was only a matter of time https://www.bleepingcomputer.com/news/security/new-dearcry-ransomware-is-targeting-microsoft-exchange-servers/” – Not Relevant (looks like an exciting link, but in the post there is no information about the link - you don't know what to expect) – relevant would also have been fine
> * Information that seems to be spam
> * Information that is highly politicly motivated
> * Information for general public (non experts)
> * Information that is speculative
> * "Casual news" for the general public
> * General cybersecurity advises (for the general public)
> * Podcasts, Interviews or personal opinions are to be marked as not relevant
> * Smaller service companies that report that their systems are updated and safe
> * News aggregations with several other news are not relevant
>     * "RT Read this week's digest to find out the latest updates in the #Microsoft Exchange vulnerabilities as well as how #hackers were able to breach 150,000 surveillance cameras from inside hospitals, jails and Tesla."
> **When in doubt -> Not Relevant**


# Contributions

Markus Bayer \
Alexej Strassheim \
Frank Walter \
Christian Reuter
