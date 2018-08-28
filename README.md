# Squabble

A simple leader election. Pulled from [ExVenture](https://github.com/oestrich/ex_venture).

In order to connect multiple nodes you should also set up [libcluster](https://github.com/bitwalker/libcluster).

## Installation

Install via hex.

```elixir
def deps do
  [
    {:squabble, "~> 0.1.0"},
  ]
end
```

## Leader Notifications

Squabble will a call a module on the node when the leader node is selected. This is a behaviour. See a sample below.

```elixir
defmodule MyApp.Leader do
  @behaviour Squabble.Leader

  @impl true
  def leader_selected(term) do
  end

  @impl true
  def node_down() do
  end
end
```

Configure squabble by setting up the winner notification modules.

```elixir
config :squabble, :cluster, subscriptions: [MyApp.Leader]
```

You need to start Squabble in your application tree _after_ `libcluster` if you're using that. All nodes should be connected before starting Squabble.

```elixir
children = [
  {Squabble, []}
]
```
