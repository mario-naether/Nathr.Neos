# Nathr.Neos
A news package for NEOS CMS

provides nodes:
* Author
* Category
* Folder
* News
* Tag

Plugins:
* listing of news
* sinlge news teaser

## 1.Installation

Installation of this package with composer:

``composer require mario-naether/nathr-news``

## 2.Configuration

News can be configure in Fusion as a basic page node:
````neosfusion
prototype(Nathr.News:News.Document) < prototype(Neos.Demo:DefaultPage) {
    bodyTag.attributes.class = 'news'
    body {
        templatePath = 'resource://...'
        content.teaser >
        content.sidebar >
        content.teaserSidebar >

        news = ${node}
        title = ${q(node).property('title')}
        teaser = ${q(node).property('teaser')}
        image = Neos.NodeTypes:Image

        prevNews = ${q(node).prev('[instanceof Nathr.News:News]').get(0)}
        nextNews = ${q(node).next('[instanceof Nathr.News:News]').get(0)}
        newsOverNode = ${q(node).parent().get(0)}

        tags = ${q(q(node).property('tags')).get()}
        newsByTagCollection = ${q(node).siblings('[instanceof Nathr.News:News]').filterByReference('tags', q(tags)).get()}

        newsLatestCollection = Nathr.News:LatestNewsListing {
            headline = 'the latest news'
        }
    }
}
````
