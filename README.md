# "Travel from your couch" hackathon

Howdy, wilders! Remember, those are just a few usage tips and examples for the Windy&MET APIs, and as always, you should **read the docs**!

![Morpheus: read the docs](https://innovation.enova.com/wp-content/uploads/2019/06/what-if-i-told-you-that-if-you-read-our-documentation-there-would-be-no-issue.jpg)

* [API docs](#api-docs)

    * [1. Windy API](#1-windy-api)

        * [1.1. Setup](#11-setup)
        * [1.2. Usage](#12-usage)
    * [2. MET API](#2-met-api)

## API docs

### 1. Windy API

#### 1.1. Setup

The Windy API offers several services. We'll focus on the _Webcams API_.

First you have to [create an account](https://community.windy.com/register).

Then you can [login](https://community.windy.com/login).

Then you can [manage your API keys](https://api.windy.com/keys): on this page, you get a list of your API keys. Click _Create a new API key_. Leave "Domains restriction" empty; under "Project identification", you may set an URL, or more simply, a "dummy" identifier, e.g. *MyHackathonProject*.

#### 1.2. Usage

First, head to the [Webcams API documentation](https://api.windy.com/webcams/docs#/list/country).

It offers many "endpoints" (URLs) as you can see.

You probably will need to explore two types of endpoints:

* endpoints that give a list of webcams, e.g. (in the following URLs, replace `YOUR_API_KEY` by your own key):

    * by country; for example, to get all webcams in Germany: <https://api.windy.com/api/webcams/v2/list/country=DE?key=YOUR_API_KEY>
    * by geographical locationi; for example, to get all webcams around the eastern French-Spanish border: <https://api.windy.com/api/webcams/v2/list/nearby=42.44,3.14,100?key=YOUR_API_KEY>
    * of course, **you should have a look at the other endpoints!**
* endpoint that gives details on one or more webcams; for example, to get details for a webcam located on the "Pic du Midi", in the Pyrenees: <https://api.windy.com/api/webcams/v2/list/webcam=1259146823?show=webcams:image,location,player&key=YOUR_API_KEY>. This endpoint returns an object containing deeply nested data! In this example, you would need to get use one of the "embed" links as a `src` attribute for an `<iframe>` tag. Here's how you'd get the data:

    * JS - assuming `data` is what you got via `res.json()` (fetch) or `res.data` (axios): `data.result.webcams[0].player.lifetime.embed`.
    * PHP - assuming `$data` is obtained by decoding Guzzle's response as an object via `json_decode($response->getBody())`: `$data->result->webcams[0]->player->lifetime->embed`.

### 2. MET API

Good news: you don't need an API key for this one! So, head straight to the [documentation](https://metmuseum.github.io/).

Here are a few examples:

* You can get _all_ the objects referenced in the API via this endpoint: <https://collectionapi.metmuseum.org/public/collection/v1/objects>. :warning: **This is probably a bad idea**, since you will get a fairly large amount of data (2.5Mb), and it could slow down your app.
* Another way to access objects is to use the "search" endpoint. E.g. if you want all *paintings* depicting *sunsets*, and *with images*, you would call: <https://collectionapi.metmuseum.org/public/collection/v1/search?medium=Paintings&hasImages=true&q=sunset>.
* Then you can call another endpoint to get _details_ of an object, via its *id*, e.g.: <https://collectionapi.metmuseum.org/public/collection/v1/objects/436329>. The data you get is quite easy to use (hint: look at the `primaryImage` and `primaryImageSmall` for pictures...).
