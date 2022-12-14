# What are lambda layers

You can use lambda layers to externalize code and reuse it in several lambdas.

Lambda layers provide a convenient way to package libraries and other dependencies that you can use with your Lambda functions. Using layers reduces the size of uploaded deployment archives and makes it faster to deploy your code.

A layer is a .zip file archive that can contain additional code or data. A layer can contain libraries, a custom runtime, data, or configuration files. Layers promote code sharing and separation of responsibilities so that you can iterate faster on writing business logic.

See description in [AWS](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html).
