---
description: Convert Addresses and place names into Geo-Features
---

# Forward Geocoding

Forward Geocoding allows you to convert addresses and place names into Geo-Features with their Coordinates, Properties, and Shape. If you would like to learn more about the information you can retrieve, take a look at the [Geo-Feature Model](../geo-feature-model.md).

{% hint style="info" %}
If you prefer OpenAPI/Swagger Documentations, click [here](https://api.cartesius.io/beta/openapi#/default/ForwardController\_forwardRequest).
{% endhint %}

The query string you provide can contain incomplete and incorrect addresses or full addresses in any order. It is also possible to pass natural text, such as parts of a conversation that contains geographical references, as we [parse](address-parsing.md) important address components out of the given string. Forward Geocoding should not be used for prefix search, such as search-as-you-type or autocomplete. Please take a look at the [Autocomplete API](autocomplete.md) that covers this exact use-case.

### Examples

**Minimum**

{% tabs %}
{% tab title="HTTP" %}
```uri
https://api.cartesius.io/beta/forward?
    apiKey=<YOUR_API_KEY>&   
    q=Platz d. Deutschen Einheit 4, 20457 HH
```
{% endtab %}

{% tab title="Node/Browser" %}
<pre class="language-typescript"><code class="lang-typescript">import { CartesiusClient } from "@cartesius/sdk"

<strong>const client = new CartesiusClient({
</strong>  apiKey: '&#x3C;YOUR-API-KEY>',
});

const result = await client.forward("Platz d. Deutschen Einheit 4, 20457 HH");
</code></pre>
{% endtab %}

{% tab title="Go" %}
Coming soon!
{% endtab %}
{% endtabs %}

**With Filters (Bounding Box, Languages, Categories)**

{% tabs %}
{% tab title="HTTP" %}
```uri
https://api.cartesius.io/beta/forward?
    apiKey=<YOUR_API_KEY>&   
    languages=de,en,es& 
    categories=amenity:theatre,highway&
    bbox=9.65,53.38,10.33,53.75&
    q=Platz d. Deutschen Einheit 4, 20457 HH
```
{% endtab %}

{% tab title="Node/Browser" %}
<pre class="language-typescript"><code class="lang-typescript">import { CartesiusClient } from "@cartesius/sdk"

<strong>const client = new CartesiusClient({
</strong>  apiKey: '&#x3C;YOUR-API-KEY>',
});

const result = await client.forward("Platz d. Deutschen Einheit 4, 20457 HH",
<strong>{
</strong>  languages: ["deu", "en", "es"], // ISO 3166 ALPHA-2 or ALPHA-3
  fields: ["shape", "displayValue", "category"], // fields to return
  categories: [{
    type: 'amenity',
    specfication: 'shop'
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

{% swagger src="../../.gitbook/assets/swagger-spec.json" path="/forward" method="get" %}
[swagger-spec.json](../../.gitbook/assets/swagger-spec.json)
{% endswagger %}
