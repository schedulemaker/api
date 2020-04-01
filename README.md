# api
Contains schema, data source, and resolver definitions for AWS AppSync

Make sure any resolvers attached to [Banner Proxy](https://github.com/schedulmaker/banner-proxy) use `$context.args.<INPUT_FIELD_NAME>` See below for example:

Query:
```
type Query {
   getCampus(event: BannerProxyInput): [BannerResult]
}
```
Resolver mapping:
```
#**
The value of 'payload' after the template has been evaluated
will be passed as the event to AWS Lambda.
*#
{
  "version" : "2017-02-28",
  "operation": "Invoke",
  "payload": $util.toJson($context.args.event) # Since the input field in the query is "event", we use $context.args.event
}
```
