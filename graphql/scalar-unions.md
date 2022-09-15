# Can you create a union out of scalars in graphql?

No. Scalars can't be used as part of unions, since per the specification, unions specifically "represent an object that could be one of a list of GraphQL Object types."

Note that if you're trying to return one of several scalars for an output field, it's possible to utilize a union for the parent type to achieve a similar result. For example, this isn't possible:

	type Post {
  		content: String | Int
	}

but you can do the following:

	type PostString {
  		content: String
	}

	type PostInt {
  		content: Int
	}

	union Post = PostString | PostInt

