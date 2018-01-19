# ex-kraken-api

**Elixir library for Kraken (kraken.com) exchange API**

## Attribution

Based upon

 1. https://github.com/x-ji/kraken_api
 2. https://github.com/1st8/exkraken
 3. https://github.com/parubets/kraken_elixir
 
## TODO

 Add additional endpoint methods for custom API keys.
 
 Maybe publish this in a different package

## Installation

NOTE: This section needs to be updated

This package can be installed
by adding `kraken_api` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:kraken_api, "~> 0.1.0"}
  ]
end
```

The docs can
be found at [https://hexdocs.pm/kraken_api](https://hexdocs.pm/kraken_api).

## Configuration
You'll need to provide two environment variables which supply your Kraken API key and private key. You can generate them at [https://www.kraken.com/u/settings/api](https://www.kraken.com/u/settings/api)

```elixir
use Mix.Config

config :kraken_api,
  api_key: "YOUR_API_KEY",
  private_key: "YOUR_PRIVATE_KEY"
```

You might want to keep the key out of the version control system.

## Usage
The names of the available methods correspond to the names listed at [https://www.kraken.com/help/api](https://www.kraken.com/help/api). For example, "Get account balance" corresponds to the method `balance(params \\ %{})`.

The methods are divided into three modules: `Public`, `Account`, and `Trade`, corresponding to "Public Market Data", "Private User Data", and "Private User Trading"
in the Kraken API documentation.

If the API call succeeded, a tuple `{:ok, response}` will be returned, where `response` is a Map containing the response from Kraken.

If it failed, `{:error, errors}` will be returned, where `errors` might contain the reason for error given by Kraken. However, it might also simply be `nil` if it wasn't possible to obtain the reason for failure from Kraken.

Parameters are supplied as an Elixir Map to the methods. For example, 

```elixir
iex(1)> KrakenApi.Public.asset_info(%{asset: "BCH,XBT"})
{:ok,
 %{"BCH" => %{"aclass" => "currency", "altname" => "BCH", "decimals" => 10,
    "display_decimals" => 5},
    "XXBT" => %{"aclass" => "currency", "altname" => "XBT", "decimals" => 10,
    "display_decimals" => 5}}}

iex(2)> KrakenApi.Account.closed_orders(%{start: 1507204548, end: 1507244548})
{:ok,
 %{"closed" => ...},
    ...}
```

For the full list of API methods and the corresponding parameters please refer to the [Kraken documentation](https://www.kraken.com/help/api) and the [package documentation](https://hexdocs.pm/kraken_api). The [Kraken documentation](https://www.kraken.com/help/api) also contains the response formats.

## License
kraken_api is released under the MIT License. See LICENSE file for more information.

