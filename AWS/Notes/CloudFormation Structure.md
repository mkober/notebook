In CloudFormation, a template is a JSON or a YAML-formatted text file that describes your AWS infrastructure. Templates include several major sections. **The Resources section is the only required section. Some sections in a template can be in any order.** However, as you build your template, it might be helpful to use the logical ordering of the following list, as values in one section might refer to values from a previous section. Take note that all of the sections here are optional, except for Resources, which is the only one required.

- Format Version
- Description
- Metadata
- Parameters
- Mappings
- Conditions
- Transform
- **Resources (required)**
- Outputs

Clipped from: [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html)

# Template anatomy

A template is a JSON- or YAML-formatted text file that describes your AWS infrastructure. The following examples show an AWS CloudFormation template structure and its sections.

## JSON

The following example shows a JSON-formatted template fragment.

{  
  "AWSTemplateFormatVersion" : "version date",  
  
  "Description" : "JSON string",  
  
  "Metadata" : {  
    template metadata  
  },  
  
  "Parameters" : {  
    set of parameters  
  },  
   
  "Rules" : {  
    set of rules  
  },  
  
  "Mappings" : {  
    set of mappings  
  },  
  
  "Conditions" : {  
    set of conditions  
  },  
  
  "Transform" : {  
    set of transforms  
  },  
  
  "Resources" : {  
    set of resources  
  },  
   
  "Outputs" : {  
    set of outputs  
  }  
}

## YAML

The following example shows a YAML-formatted template fragment.

---  
AWSTemplateFormatVersion: "version date"  
  
Description:  
  String  
  
Metadata:  
  template metadata  
  
Parameters:  
  set of parameters  
  
Rules:  
  set of rules  
  
Mappings:  
  set of mappings  
  
Conditions:  
  set of conditions  
  
Transform:  
  set of transforms  
  
Resources:  
  set of resources  
  
Outputs:  
  set of outputs  
 

## Template sections

Templates include several major sections. The Resources section is the only required section. Some sections in a template can be in any order. However, as you build your template, it can be helpful to use the logical order shown in the following list because values in one section might refer to values from a previous section.

[Format Version (optional)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/format-version-structure.html)

The AWS CloudFormation template version that the template conforms to. The template format version isn't the same as the API or WSDL version. The template format version can change independently of the API and WSDL versions.

[Description (optional)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-description-structure.html)

A text string that describes the template. This section must always follow the template format version section.

[Metadata (optional)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/metadata-section-structure.html)

Objects that provide additional information about the template.

[Parameters (optional)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html)

Values to pass to your template at runtime (when you create or update a stack). You can refer to parameters from the Resources and Outputs sections of the template.

[Rules (optional)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/rules-section-structure.html)

Validates a parameter or a combination of parameters passed to a template during a stack creation or stack update.

[Mappings (optional)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/mappings-section-structure.html)

A mapping of keys and associated values that you can use to specify conditional parameter values, similar to a lookup table. You can match a key to a corresponding value by using the [Fn::FindInMap](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-findinmap.html) intrinsic function in the Resources and Outputs sections.

[Conditions (optional)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/conditions-section-structure.html)

Conditions that control whether certain resources are created or whether certain resource properties are assigned a value during stack creation or update. For example, you could conditionally create a resource that depends on whether the stack is for a production or test environment.

[Transform (optional)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/transform-section-structure.html)

For [serverless applications](https://docs.aws.amazon.com/lambda/latest/dg/deploying-lambda-apps.html) (also referred to as Lambda-based applications), specifies the version of the [AWS Serverless Application Model (AWS SAM)](https://github.com/awslabs/serverless-application-specification) to use. When you specify a transform, you can use AWS SAM syntax to declare resources in your template. The model defines the syntax that you can use and how it's processed.

You can also use [AWS::Include](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/create-reusable-transform-function-snippets-and-add-to-your-template-with-aws-include-transform.html) transforms to work with template snippets that are stored separately from the main AWS CloudFormation template. You can store your snippet files in an Amazon S3 bucket and then reuse the functions across multiple templates.

[Resources (required)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resources-section-structure.html)

Specifies the stack resources and their properties, such as an Amazon Elastic Compute Cloud instance or an Amazon Simple Storage Service bucket. You can refer to resources in the Resources and Outputs sections of the template.

[Outputs (optional)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/outputs-section-structure.html)

Describes the values that are returned whenever you view your stack's properties. For example, you can declare an output for an S3 bucket name and then call the aws cloudformation describe-stacks AWS CLI command to view the name.

###### Note

When authoring templates, do not use duplicate major sections, for example using multiple resource sections. Although CloudFormation may accept the template, it will have an undefined behavior when processing the template, and may incorrectly provision resources, or return inexplicable errors.