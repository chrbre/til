# How to set descriptions in graphql files

- A description is surrounded with " or triple " for a block
- Only type definitions may have a description, type extensions may __not__

Example:

	"Description for the type"
	type MyObjectType {
  		"""
  		Description for field
  		Supports **multi-line** description for your [API](http://example.com)!
  		"""
  		myField: String!

  		otherField(
    		"Description for argument"
    		arg: Int
  		)
	}