# AWS

```jsx
aws cognito-idp get-user --region 'us-west-2' --access-token 'token'
aws cognito-idp update-user-attributes --region 'us-west-2' --access-token 'testToken' --user-attributes Name="email",Value="uuganbayar@infinite.mn"
aws cognito-idp get-user-attribute-verification-code --region 'us-east-2' --attribute-name 'email' --access-token 'token'
aws cognito-idp verify-user-attribute --region 'us-west-2' --attribute-name 'email' --code '*verify-code*' --access-token 'token'
```