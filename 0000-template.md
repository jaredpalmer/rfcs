- Start Date: 2017-12-11)
- RFC PR: (leave this empty)
- React Issue: (leave this empty)

# Summary

Provide an isomorphic data fetching lifecycle 

This RFC relates to RFC #8 (`componentDidServerRender`). However, that appears to be more concerned with side-effects and not props / data fetching.

# Basic example

```
class Example extends React.Component {
  getInitialProps(props, context) {
    // must be a promise
    return Api.getPostById(props.match.params.id).then(post => ({ post }))
  }
  
  render() {
    return <div>{this.props.post}</div>
  }
}
```

# Motivation

Why are we doing this? What use cases does it support? What is the expected
outcome?

`getInitialProps` made popular by Next.js seems to be the ideal approach to server side data fetching. In Next.js's implementation, render is blocked on the client and server until the promise has resolved. This is contentious as some applications want to render _something_ while loading. Perhaps another API or component-API like `<ErrorBoundary>` could be used provide this kind of behavior


# Detailed design


React should resolve `getInitialProps` prior to mounting the component. Since this avoids state entirely, it should not have the inconsistencies that usually occur when `setState` is used in componentWillMount.

# Drawbacks

Why should we *not* do this? Please consider:

There are a lot of alternatives in user land. 

Todo

# Alternatives


Usually they are called `fetchComponentData` or `fetchData`. 

# Adoption strategy

If we implement this proposal, how will existing React developers adopt it? Is
this a breaking change? Can we write a codemod? Should we coordinate with
other projects or libraries?

Todo

# How we teach this

Todo

What names and terminology work best for these concepts and why? How is this
idea best presented? As a continuation of existing React patterns?

Would the acceptance of this proposal mean the React documentation must be
re-organized or altered? Does it change how React is taught to new developers
at any level?

How should this feature be taught to existing React developers?

# Unresolved questions

Optional, but suggested for first drafts. What parts of the design are still
TBD?
