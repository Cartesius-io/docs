# Quick Start

## Register an account

We offer a generous free tier to test our API. You can[ sign up](https://app.cartesius.io/auth/signup) for free without any payment details. If you already have an account, login to your existing account.

## Get your API keys

Your API requests are authenticated using API keys. Any request that doesn't include an API key will return an error.

You can generate an API key from your Dashboard and view key-specific statistics at any time. For more details, please refer to [api-keys.md](cartesius-studio/api-keys.md "mention").

## Use the API

The best way to interact with our API is to use one of our official libraries. If you would rather not use our libraries, you can simply send HTTP-Requests to our API (see curl).

{% tabs %}
{% tab title="curl" %}
```sh
curl 
--location 'https://api.cartesius.io/<version>/<endpoints>' 
--header 'X-API-KEY: <your api key>'
```
{% endtab %}

{% tab title="Node/Browser" %}
```
Expected soon!
```
{% endtab %}

{% tab title="more comming soon..." %}
We are currently working hard to publish more libraries, please stay tuned!
{% endtab %}
{% endtabs %}

Learn more about the API [here](reference/api/).
