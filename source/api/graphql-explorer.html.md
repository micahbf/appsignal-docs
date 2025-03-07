---
title: "GraphQL Explorer"
---
Use this GraphQL explorer to play around with AppSignal's GraphQL API. This is the API used in our frontend, so it will remain always up to date. Please note that documenting this API is a work in progress.

## Explorer

<div class="c-form">
  <label for="token" class="c-form__label">Enter your personal API <a href="https://appsignal.com/users/edit" target="_blank">token</a> </label><br>
  <input type="text" id="token" name="token" class="c-form__input">
</div>
<div id="graphiql" style="height: 100vh;margin-bottom:40px">Loading..</div>

## Examples
[Here](graphql-explorer-examples.html) are some of the query examples to get you started.

<script crossorigin src="https://unpkg.com/react/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom/umd/react-dom.production.min.js"></script>
<script crossorigin src="https://unpkg.com/graphiql/graphiql.min.js"></script>
<link href="https://unpkg.com/graphiql/graphiql.min.css" rel="stylesheet" />


<script>
  function graphQLFetcher(graphQLParams) {
    let token = document.querySelector('#token').value;
    return fetch(
      `https://appsignal.com/graphql?token=${token}`,
      {
        method: 'post',
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(graphQLParams),
        credentials: 'omit',
      },
    ).then(function (response) {
      return response.json().catch(function () {
        return response.text();
      });
    });
  }

  ReactDOM.render(
    React.createElement(GraphiQL, {
      fetcher: graphQLFetcher,
      defaultVariableEditorOpen: false,
    }),
    document.getElementById('graphiql'),
  );
</script>
