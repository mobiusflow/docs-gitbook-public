---
description: API Authorization calls
---

# Authorization

The authorization controller is used to login to the API, in addition user management.

When a login call is completed, the API will return a bearer token which should be used in the auth header of all future calls. This token is set to expire 10 minutes after its generation.

A refresh token is also included in the login response, and this is used in the body of the refresh call to get new tokens with refreshed expiry times. Ensure a refresh call is made prior to any given bearer token's expiry to avoid having to login again.

{% swagger src="https://docs-engine-api.mobiusflow.io/json" path="/api/v1/auth/login" method="post" %}
[https://docs-engine-api.mobiusflow.io/json](https://docs-engine-api.mobiusflow.io/json)
{% endswagger %}

{% swagger src="https://docs-engine-api.mobiusflow.io/json" path="/api/v1/auth/refresh" method="post" %}
[https://docs-engine-api.mobiusflow.io/json](https://docs-engine-api.mobiusflow.io/json)
{% endswagger %}

{% swagger src="https://docs-engine-api.mobiusflow.io/json" path="/api/v1/auth/user" method="post" %}
[https://docs-engine-api.mobiusflow.io/json](https://docs-engine-api.mobiusflow.io/json)
{% endswagger %}

{% swagger src="https://docs-engine-api.mobiusflow.io/json" path="/api/v1/auth/user/{username}" method="get" %}
[https://docs-engine-api.mobiusflow.io/json](https://docs-engine-api.mobiusflow.io/json)
{% endswagger %}

{% swagger src="https://docs-engine-api.mobiusflow.io/json" path="/api/v1/auth/users" method="get" %}
[https://docs-engine-api.mobiusflow.io/json](https://docs-engine-api.mobiusflow.io/json)
{% endswagger %}

{% swagger src="https://docs-engine-api.mobiusflow.io/json" path="/api/v1/auth/user/roles/{_id}" method="get" %}
[https://docs-engine-api.mobiusflow.io/json](https://docs-engine-api.mobiusflow.io/json)
{% endswagger %}

{% swagger src="https://docs-engine-api.mobiusflow.io/json" path="/api/v1/auth/user/roles/{_id}" method="patch" %}
[https://docs-engine-api.mobiusflow.io/json](https://docs-engine-api.mobiusflow.io/json)
{% endswagger %}

{% swagger src="https://docs-engine-api.mobiusflow.io/json" path="/api/v1/auth/user/password/{_id}" method="patch" %}
[https://docs-engine-api.mobiusflow.io/json](https://docs-engine-api.mobiusflow.io/json)
{% endswagger %}

{% swagger src="https://docs-engine-api.mobiusflow.io/json" path="/api/v1/auth/user/{_id}" method="delete" %}
[https://docs-engine-api.mobiusflow.io/json](https://docs-engine-api.mobiusflow.io/json)
{% endswagger %}
