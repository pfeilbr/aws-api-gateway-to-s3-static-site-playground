# aws-api-gateway-to-s3-static-site-playground

* example of hosting static site (create-react-app) with api gateway -> s3
    * can also leverage private api gateway endpoint
* static site content at [`my-react-app`](my-react-app)

## Example Deployment Steps

```sh
STAGE="dev"
STACK_NAME="aws-api-gateway-to-s3-static-site-playground"

# deploy resoruces
sam deploy --guided

# build react app
pushd my-react-app
# need to set root to subpath because of api gateway stage in path limitation
PUBLIC_URL="/${STAGE}" npm run build
popd

# deploy site
aws s3 sync my-react-app/build/ s3://aws-api-gateway-to-s3-static-sit-staticsitebucket-2k3gk0lgl72u

# visit site
open https://a4kesxi0gg.execute-api.us-east-1.amazonaws.com/dev/index.html
```

## screenshots

<img src="https://www.evernote.com/l/AAGTad9n-GJE1YUX1WX9hfouZMDLl7DaKSkB/image.png" alt="" width="75%" />

## Resources

* [API-Gateway S3 Proxy](https://jcdubs.medium.com/api-gateway-s3-proxy-a72e398b4d03) - followed this console guide to get it to work.  export as openapi from console and embed in [`template.yaml`](template.yaml)
* [Tutorial: Create a REST API as an Amazon S3 proxy in API Gateway - Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/integrating-api-with-aws-services-s3.html#api-items-in-folder-as-s3-objects-in-bucket)
* [API Gateway S3 Integration Signature does not match with blank folder name](https://stackoverflow.com/questions/64539716/api-gateway-s3-integration-signature-does-not-match-with-blank-folder-name)
* [Functionless S3 Integration inside a Serverless Casserole-Part 1](https://medium.com/lego-engineering/functionless-s3-integration-inside-a-serverless-casserole-part-1-b300085eea78)
* [SAM Template for AWS Api Gateway Integration with S3 as AWS Service](https://stackoverflow.com/questions/60488172/sam-template-for-aws-api-gateway-integration-with-s3-as-aws-service)