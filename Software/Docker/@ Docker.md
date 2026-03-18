Context https://docs.docker.com/get-started/overview/:


## Cross OS Usage
Docker will automatically determine what CPU is used for building an image. To force a target platform to be used, use `--platform`

Using an image like `arm32v6/ubuntu` is the same as specifying `ubuntu` w/ `--platform arm32v6`

## My Thoughts
Docker is the ultimate package manager. Write code one place and run it anywhere. From this comes a mountain of complexity.
Pros:
- Can be confident that local versions of code will run on other platforms
- Allows for testing full backend stacks
Cons:
- Can be confusing
- Bind Mounting can lead to weird filesystem behavior


Table of Contents:
	[[Documentation]]
	[[Software/Docker/Commands]]


