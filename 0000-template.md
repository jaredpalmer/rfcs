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

`getInitialProps` made popular by Next.js seems to be the ideal approach to server side data fetching. In Next.js's implementation, render is blocked on the client and server until the promise has resolved. 


Please focus on explaining the motivation so that if this RFC is not accepted,
the motivation could be used to develop alternative solutions. In other words,
enumerate the constraints you are trying to solve without coupling them too
closely to the solution you have in mind.

# Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with React to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

React should resolve `getInitialProps` prior to mounting the component. Since this avoids state entirely, it should not have the inconsistencies that usually occur when `setState` is used in componentWillMount.

# Drawbacks

Why should we *not* do this? Please consider:

There are a lot of alternatives in user land. 

There are tradeoffs to choosing any path. Attempt to identify them here.

# Alternatives

What other designs have been considered? What is the impact of not doing this?

Usually they are called `fetchComponentData` or `fetchData`. 

# Adoption strategy

If we implement this proposal, how will existing React developers adopt it? Is
this a breaking change? Can we write a codemod? Should we coordinate with
other projects or libraries?

# How we teach this

What names and terminology work best for these concepts and why? How is this
idea best presented? As a continuation of existing React patterns?

Would the acceptance of this proposal mean the React documentation must be
re-organized or altered? Does it change how React is taught to new developers
at any level?

How should this feature be taught to existing React developers?

# Unresolved questions

Optional, but suggested for first drafts. What parts of the design are still
TBD?
