---
description: Convert Coordinates into Geo-Features
---

# Reverse Geocoding

Reverse Geocoding allows you to convert coordinates into Geo-Features with their Addresses, Names, Properties, and Shapes. If you would like to learn more about the information you can retrieve, take a look at the [Geo-Feature Model](../geo-feature-model.md).

{% hint style="info" %}
If you prefer OpenAPI/Swagger Documentations, click [here](https://api.cartesius.io/beta/openapi#/default/ForwardController\_forwardRequest).
{% endhint %}

### Examples

**Minimum**

{% tabs %}
{% tab title="HTTP" %}
{% code overflow="wrap" %}
```uri
https://api.cartesius.io/beta/reverse?apiKey=<YOUR_API_KEY>&lat=52.517831262&
lon=13.372331844
```
{% endcode %}
{% endtab %}

{% tab title="Node/Browser" %}
<pre class="language-typescript"><code class="lang-typescript">import { CartesiusClient } from "@cartesius/sdk"

<strong>const client = new CartesiusClient({
</strong>  apiKey: '&#x3C;YOUR-API-KEY>',
});

const result = await client.reverse(52.517831262, 13.372331844);
</code></pre>
{% endtab %}

{% tab title="Go" %}
Coming soon!
{% endtab %}
{% endtabs %}

**With Filters (Languages, Categories)**

{% tabs %}
{% tab title="HTTP" %}
{% code overflow="wrap" %}
```uri
https://api.cartesius.io/beta/forward?apiKey=<YOUR_API_KEY>&languages=de,en,es&categories=amenity:restaurant,highway&bbox=9.65,53.38,10.33,53.75&q=Platz d. Deutschen Einheit 4, 20457 HH
```
{% endcode %}
{% endtab %}

{% tab title="Node/Browser" %}
<pre class="language-typescript"><code class="lang-typescript">import { CartesiusClient } from "@cartesius/sdk"

<strong>const client = new CartesiusClient({
</strong>  apiKey: '&#x3C;YOUR-API-KEY>',
});

client.reverse(52.517831262, 13.372331844, 5, {
  languages: ['deu', 'en'], // ISO 3166 ALPHA-2 or ALPHA-3
  fields: ['w3w', 'displayValue'], // fields to return
  categories: {
    type: 'amenity',
  },
});

</code></pre>
{% endtab %}

{% tab title="Go" %}
Coming soon!
{% endtab %}
{% endtabs %}

### Results

The Results will contain Geo features in the given radius (defaults to 1 km) sorted ascending by the distance to the given coordinates.&#x20;

The result will be a list of valid [GeoJSON Features](https://geojson.org/) [(RFC 7946)](https://tools.ietf.org/html/rfc7946). A detailed overview of all properties with explanations can be found [here](../geo-feature-model.md).

### Endpoint Documentation

{% swagger src="https://api.cartesius.io/beta/openapi-json" path="/reverse" method="get" %}
[https://api.cartesius.io/beta/openapi-json](https://api.cartesius.io/beta/openapi-json)
{% endswagger %}
