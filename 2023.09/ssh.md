# 免密登录

### 1.本地客户端生成公私钥

```bash
ssh-keygen
```



### 2. 上传公钥到服务器

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub xxx@xxx
```



### 3. 测试免密登录

```
ssh xxx@xxx
```

