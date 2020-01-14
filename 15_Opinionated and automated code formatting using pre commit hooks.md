## Opinionated and automated code formatting using pre commit hooks

```For as long as we can remember, what style to use for formatting code has been a matter of personal taste, company policy and heated debate. Finally, the industry appears to be tiring of this endless argument and teams are freeing up surprisingly large amounts of time by forgoing these discussions and just adopting``` **opinionated and automated code formatting tools**. 

```Even if you don't agree 100% with the opinions of the various tools, the benefits of focusing on what your code does rather than how it looks is something most teams should be able to get behind.``` 

[Prettier](https://www.thoughtworks.com/radar/tools/prettier) has been getting our vote for JavaScript, but similar tools, such as [Black](https://github.com/ambv/black) for Python, are available for many other languages and are increasingly being built-in as we see with [Golang](https://golang.org/cmd/gofmt/) and [Elixir.](https://elixir-lang.org/blog/2018/01/17/elixir-v1-6-0-released/) 

```The key here is not to spend hours discussing which rules to enforce, but instead pick a tool that is opinionated, minimally configurable and automated — ideally as a pre-commit hook.```
