---
description: Typo-tolerant search-as-you-type Geo search
---

# Autocomplete

The Autocomplete API allows you to convert addresses and place names into Geo-Features with their Coordinates, Properties, and Shape. This can be used to let users quickly find their billing or shipping address, as well as a map component to search features on a map. **Cartesius also offers search components for Leaflet, Mapbox, Maplibre, React, Angular and as Web Components.** If you would like to learn more about the information you can retrieve, take a look at the [Geo-Feature Model](../geo-feature-model.md).

{% hint style="info" %}
If you prefer OpenAPI/Swagger Documentations, click [here](https://api.cartesius.io/beta/openapi#/default/ForwardController\_forwardRequest).
{% endhint %}

The query string you provide can be any part of any address or place in the World. You can search for places and addresses in any order. Cartesius can find addresses and places that have typos or spelled as they are spoken (phonetic search). Furthermore, you can search in any language available (up to 200+). For a detailed overview of fields that are included in the search,  take a look at the [Geo-Feature Model](../geo-feature-model.md).&#x20;

If you have a complete address or place name, the  [Forward API](forward-geocoding.md) might be a better fit.

### Examples

**Minimum**

{% tabs %}
{% tab title="HTTP" %}
{% code overflow="wrap" %}
```uri
https://api.cartesius.io/beta/forward?apiKey=<YOUR_API_KEY>&q=Elbphil
```
{% endcode %}
{% endtab %}

{% tab title="Node/Browser" %}
<pre class="language-typescript"><code class="lang-typescript">import { CartesiusClient } from "@cartesius/sdk"

<strong>const client = new CartesiusClient({
</strong>  apiKey: '&#x3C;YOUR-API-KEY>',
});

const result = await client.autocomplete("Elbphil");
</code></pre>
{% endtab %}

{% tab title="Go" %}
Coming soon!
{% endtab %}
{% endtabs %}

**With Filters (Bounding Box, Languages, Categories)**

{% tabs %}
{% tab title="HTTP" %}
{% code overflow="wrap" %}
```uri
https://api.cartesius.io/beta/autocomplete?apiKey=<YOUR_API_KEY>&languages=de,en,es& categories=amenity:restaurant,highway&bbox=9.65,53.38,10.33,53.75&q=Elbphil
```
{% endcode %}
{% endtab %}

{% tab title="Node/Browser" %}
<pre class="language-typescript"><code class="lang-typescript">import { CartesiusClient } from "@cartesius/sdk"

<strong>const client = new CartesiusClient({
</strong>  apiKey: '&#x3C;YOUR-API-KEY>',
});

const result = await client.autocomplete("Elbphil",
<strong>{
</strong>  languages: ["deu", "en", "es"], // ISO 3166 ALPHA-2 or ALPHA-3
  fields: ["shape", "displayValue", "category"], // fields to return
  categories: [{
    type: 'amenity',
    specfication: 'restaurant'
  }, {
    type: "highway"
  }],
  bbox: {
    left: 9.65,
    bottom: 53.38,
    right:10.33,53.75
    top: 53.75
  },
  filter: {
    internetAccess: true
  }
});
</code></pre>
{% endtab %}

{% tab title="Go" %}
Coming soon!
{% endtab %}
{% endtabs %}

### Results

Results will be ranked based on popularity and population, meaning if you search for something that does not have any exact matches, results that have a higher population or popularity will have a higher sort score.&#x20;

The result will be a list of valid [GeoJSON Features](https://geojson.org/) [(RFC 7946)](https://tools.ietf.org/html/rfc7946). A detailed overview of all properties with explanations can be found [here](../geo-feature-model.md).

### Endpoint Documentation

{% swagger src="https://api.cartesius.io/beta/openapi-json" path="/autocomplete" method="get" %}
[https://api.cartesius.io/beta/openapi-json](https://api.cartesius.io/beta/openapi-json)
{% endswagger %}
