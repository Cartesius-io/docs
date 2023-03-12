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

```url
https://api.cartesius.io/beta/forward?
    apiKey=<YOUR_API_KEY>&   
    q=Platz d. Deutschen Einheit 4, 20457 HH
```

**With Filters (Bounding Box, Languages, Categories)**

```url
https://api.cartesius.io/beta/forward?
    apiKey=<YOUR_API_KEY>&   
    languages=de,en,es& 
    categories=amenity:theatre,highway&
    bbox=9.65,53.38,10.33,53.75&
    q=Platz d. Deutschen Einheit 4, 20457 HH
```

### Results

Results will be ranked based on popularity and population, meaning if you search for something that does not have any exact matches, results that have a higher population or popularity will have a higher sort score.&#x20;

The result will be a list of valid [GeoJSON Features](https://geojson.org/) [(RFC 7946)](https://tools.ietf.org/html/rfc7946). A detailed overview of all properties with explanations can be found [here](../geo-feature-model.md).

### Endpoint Documentation

{% swagger src="../../.gitbook/assets/swagger-spec.json" path="/forward" method="get" %}
[swagger-spec.json](../../.gitbook/assets/swagger-spec.json)
{% endswagger %}
