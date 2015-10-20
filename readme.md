Resource Identifier 
===================
[![Build Status](https://magnum.travis-ci.com/palantir/resource-identifier.svg?token=a2W6r3g3xzxTyZqnjRYZ&branch=develop)](https://magnum.travis-ci.com/palantir/resource-identifier)
[![Coverage Status](https://coveralls.io/repos/palantir/resource-identifier/badge.svg?branch=develop&service=github&t=KtNNqP)](https://coveralls.io/github/palantir/resource-identifier?branch=develop)

Resource Identifiers offer a common encoding for wrapping existing unique identifiers with some additional
context that can be useful when storing those identifiers in other applications. Additionally, the context
can be used to disambiguate application-unique, but not globally-unique, identifiers when used in a common
space.

We use a format inspired by existing standards, such as [AWS ARNs][1], [URNs][2], and [URIs][3]:

    ri.<service>.<instance>.<type>.<context>.<locator>

This project provides a basic utility class (`ResourceIdentifier`) to create and verify new identifier 
strings that follow the specified format, and, parse existing identifier strings into component parts.

Format
------
Resource Identifiers contain 5 components, prefixed by a format identifier `ri` and separated with periods:

 1. **Service**: a string that represents the service (or application) that namespaces the rest of the 
    identifier. Must conform with regex pattern `[a-z][a-z0-9\-]*`.
 2. **Instance**: an optionally empty string that represents a specific service cluster, to allow 
    disambiguation of artifacts from different service clusters. Must conform to regex pattern 
    `([a-z0-9][a-z0-9\-]*)?`.
 3. **Type**: a service-specific resource type to namespace a group of locators. Must conform to regex
    pattern `[a-z][a-z0-9\-]*`.
 4. **Context**: a service-specific context related to the resource. Must conform to regex
    pattern `[a-zA-Z0-9_\-]*`.
 5. **Locator**: a string used to uniquely locate the specific resource. Must conform to regex pattern
    `[a-zA-Z0-9\-\._]+`.

[1]:http://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html
[2]:https://en.wikipedia.org/wiki/Uniform_resource_name
[3]:https://en.wikipedia.org/wiki/Uniform_resource_identifier
