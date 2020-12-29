---
title: "For JSON what to do with nothing?"
published: true
---

When you run a valid query against our backend normally you receive data in a JSON format, but when the query is valid and no data is returned you receive a 204. The way our current parsing is setup this reports back a failure which really isn't correct. So what can we do to solve that problem?

# Optional Values

I would prefer an empty JSON file so an empty object could be be created, but what do you do with the values of the object? Make everything optional? This would be horrible to unwrap the values every time you call them. This would also break the external API as it would change the existing behaviour for clients who consume these endpoints.

# Optional Object

What about making the object optional, same problems, but at a higher level. You'd have to unwrap it all the time and it breaks the existing behaviour.

# Default Values

What about having default values for all the fields? What's a correct default value? I don't want to pre-fill in something that's wrong. Obviously this is were an optional value is better, but as discussed above, doesn't work.

# Custom Return

We currently have our own custom Result and was put in place before Swift came out with there own version. We could add another case to the Result indicating the call was successful, but this feels kludgy and I would rather remove the custom Result and use the one that comes with Swift.

# Fake failure

Before any of these changes were put in place. An empty result even when it is returned in a 204 would fail. So I'm leaning towards still having it fail, but adding another Error type saying that it had no data. This is technically a lie, but aligns us with the existing behaviour.

# Conclusion

Talked to the team about what to do and we agreed on having fake failures was the best case of action. It's not the prettiest solution, but it works and is of minimal impact to customers of our API. And sometimes that's what's best.
