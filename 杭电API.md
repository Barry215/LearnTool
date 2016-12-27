## 杭电API

### 使用方法

#### 应用内部跳转

先将用户导向 `https://api.hdu.edu.cn/oauth/authorize?response_type=code&client_id{client_id}&redirect_uri={redirect_uri}&scope={scope}`

> `scope`: 可以是 `read`, `read,write`, `read:public` 等.
>
> `redirect_uri`: 必须是合法的 URI.

如：

https://api.hdu.edu.cn/oauth/authorize?client_id=hduin&redirect_uri=https://hduin.hdu.edu.cn/auth/hduapi&response_type=code&scope=read



#### 用户在授权之后

认证服务器会跳到之前的`{redirect_uri}?code={authorization_code}`

如：

https://hduin.hdu.edu.cn/auth/hduapi?code=12996122-94e4-4573-a534-63f389ad2852



#### 应用拿到code之后

应用拿到 `authorization_code` 后应用提供者 访问 `POST` `https://api.hdu.edu.cn/oauth/tokengrant_type=authorization_code&client_id={client_id}&client_secret={client_secret}&code={authorization_code}` 获取 AccessToken



