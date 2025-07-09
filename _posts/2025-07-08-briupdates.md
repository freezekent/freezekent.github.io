---
title: BRI Projects
date: 2025-07-08
categories: [China, Data]
tags: [shiny, china, data] 
---

# Belt and Road Initiative Project Updates

Visit the dashboard of [BRI Project Updates](https://shiny.freezethe.day/briupdates/).  You can also [download the spreadsheet](https://docs.google.com/spreadsheets/d/1nhk9WOpAjfOsKnnl98NJXa6mK0g_9RsaNtz16gyxjOI/edit?usp=sharing) of projects used in the dashboard if you prefer.

Despite the prominence of the Belt and Road Initiative (BRI), details of the scope and nature of China's signature foreign policy initiative remain opaque.  The BRI itself has no clear definition, giving Beijing latitude to tailor and market the initiative as it sees fit.  This strategic ambiguity is a feature, not a bug, and it remains unlikely that China will produce any centralized accounting for all BRI programs in the foreseeable future.

Beginning in early 2021, however, China began to publish weekly BRI project updates through its online BRI portal at [yidaiyilu.gov.cn](https://www.yidaiyilu.gov.cn/), "run by the China Economic Information Service and the State Information Center, under the guidance of China's National Development and Reform Commission and Xinhua News Agency."  These weekly updates, largely pulled from company press releases and social media accounts, do not present a complete accounting of BRI projects, and do not contain a large amount of detail.  However, they do provide a glimpse into projects that the Chinese government deems to be part of the BRI, as well as very timely information on updates in the status of the projects.

## How is the database pulled together?

New project updates are published weekly in Chinese to [this site](https://www.yidaiyilu.gov.cn/list/w/xmzb), which I then scrape and clean into a database of projects.  Each weekly update is organized into three sections:

1. Signing/Winning a Bid (签约/中标): Refers to a new contract for a project, or where a Chinese company successfully won a bid for a project.
2. Under Construction/Start of Work (在建/开工): The update refers to the start of formal construction on the project, or a construction milestone for the project has been reached.
3. In operation/Completed (运营/完成): This is a final update for the project, indicated that the project has been formally completed and is in operation.  A typical update of this type often involves a handover ceremony.

The nature of the project updates indicate the portal (and the BRI)'s focus on hard infrastructure investments and contracts, coming from both state-owned and private enterprises.  Not included in the database are any technical assistance, training programs, humanitarian assistance/donations, or other forms of "soft" support.

After scraping the projects, I used ChatGPT's api to quickly "code" them so that the projects can be mapped and parsed by end users.  These include the following variables:

1. Latitude and Longitude of the project.
2. Country where the project is located.
3. Whether the project is a power plant, and if so, the type of power plant (Solar, Hydro, Wind, Natural Gas, Coal, Geothermal, or Other).
4. Whether the project was a transportation infrastructure project, and if so, the type of transportation project (Railway, Roads, Ports/Shipyards, Public Transit, Airport, or Other).
5. Whether the project was to construct a sports facility.
6. Whether the project was to construct an educational facility such as a school or university building.
7. Whether the project was to construct a health facility or hospital.
8. Whether the project was to construct water supply or sanitation infrastructure.

Finally, I used the Google Translate function in Google Sheets to translate the project title, subtitle (if provided), and description into English.

## Limitations of the Database and Appropriate Use Cases

Limitations include:

1. This is not a complete accounting of all BRI projects, but just what has been selected to be included in weekly updates.  Accordingly, these projects may be viewed as a form of state propaganda - there are only "positive" updates included in the database (winning bids, starting construction, project completions).
2. Political sensitivities may also limit the projects which are included.  For example, there are zero project updates included in the database in Iran, despite the fact that Chinese enterprises and investments have been very active in the country.
3. Project updates do not contain a lot of detail other than title of the project and where it is located.  It is very rare that the description contains any dollar value for the project. 
4. I have relied on generative AI to make the database easier to search -- these are often "best guesses" and should be interpreted as such.  Map locations, in particular, may not be accurate - you should always click on the project and read through the description to check details on any particular project.
5. The English titles, subtitles, and descriptions have been Google translated.  This can sometimes lead to confusing results.  To give one example, one project from the week of June 21, 2025 in Vanuatu references "Antigua and Barbuda", which might make you think that the project is actually in the Caribbean island nation of the same name.  But the original Chinese is "安巴", which is how they chose to transliterate "Ambae" Island, which just happens to also be the shorthand term for Antigua and Barbuda.  In other words, translations are not perfect.

With those limitations in mind, the database can be used to access very recent (within the past week) updates in Chinese financed or supported infrastructure projects around the world.  These can be used to help identify projects both in particular countries or locations, as well as the types of projects (eg. where are Chinese-supported power projects located?).  

## Navigating the Site

I built the site using R Shiny, and host the site on a free AWS instance.  Occasionally the site may run slow as a result since I am too cheap to upgrade the server.

![briprojects](/assets/img/2025-07-08-briupdates/briprojsite.png) 

When you first load the site, you should see a display something like the above image.  On the left hand side are all possible filters that you can use - including an open Keyword search (both Chinese and English searches work), project type filters (power generation, transportation, sports facility, education facility, health facilities), and week of the project update.  You can also choose the language (translated English or original Chinese) for the project labels.  To view project details click on a project.

Note that all possible values for all filters are selected by default (that is, it will map all projects).  To map just a subset of projects, you would delete any criteria for projects you don't wish to include: for example, if I wanted to just see solar power projects, I would remove the "Not Power", "Hydro", "Wind", "Natural Gas", "other", "Coal", and "Geothermal" options from the Power Generation Projects dropdown, and only keep "Solar".  


 