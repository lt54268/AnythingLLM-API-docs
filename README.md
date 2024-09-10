# AnythingLLM的API接口用法
## 一、验证API密钥是否有效
```
curl -X 'GET' \
  'http://服务器IP:3001/api/v1/auth' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：GET
#### 2、请求地址：'http://服务器IP:3001/api/v1/auth'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
###  响应：
#### 1、响应体：
##### 响应状态：200
```
{
  "authenticated": true
}
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
#### 2、响应头：
```
 content-length: 22 
 content-type: application/json; charset=utf-8 
 date: Fri,23 Aug 2024 08:07:02 GMT 
 etag: W/"16-sJz8uwjdDv0wvm7//BYdNw8vMbU" 
 vary: Origin 
 x-powered-by: Express 
```
## 二、通过API密钥查看详细的用户信息
```
curl -X 'GET' \
  'http://服务器IP:3001/api/v1/admin/users' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：GET
#### 2、请求地址：'http://服务器IP:3001/api/v1/admin/users'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
###  响应：
#### 1、响应体：
##### 响应状态：200
```
{
  "users": [
    {
      "id": 1,                                      // 用户ID，后续经常用到
      "username": "admin1",
      "pfpFilename": null,
      "role": "admin",
      "suspended": 0,
      "seen_recovery_codes": true,
      "createdAt": "2024-08-28T01:43:44.971Z",
      "lastUpdatedAt": "2024-08-28T01:43:44.971Z"
    }
  ]
}
```
##### 响应状态：401
```
AnythingLLM未处于多用户模式
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头：
```
 connection: keep-alive 
 content-length: 197 
 content-type: application/json; charset=utf-8 
 date: Wed,28 Aug 2024 06:40:17 GMT 
 etag: W/"c5-3tgeZr8+rnHQ4t0k/TUKIhNftDM" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 三、使用用户名和密码创建新用户
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/admin/users/new' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "username": "sample-sam",
  "password": "hunter2",
  "role": "default"
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/v1/admin/users/new'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体
```
{
  "username": "sample-sam",  // 用户名不少于6位字符
  "password": "hunter2",     // 密码不少于8位字符
  "role": "default | admin"  // default代表普通用户，admin代表管理员
}
```
###  响应：
#### 1、响应体：
##### 响应状态：200
```
{
  "user": {
    "id": 1,
    "username": "sample-sam",
    "role": "default"
  },
  "error": null
}
```
##### 响应状态：400
```
{
  "user": null,
  "error": "password should be at least 8 characters long"
}
```

##### 响应状态：401
```
AnythingLLM未处于多用户模式
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头：
```
 access-control-allow-origin: http://xxx.xxx.xxx.xxx:3001 
 connection: keep-alive 
 content-length: 69 
 content-type: application/json; charset=utf-8 
 date: Wed,28 Aug 2024 06:52:45 GMT 
 etag: W/"45-80mcr2iEUER4o3FJbxqL6fJvkaY" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express
```
## 四、通过用户ID更新用户设置
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/admin/users/用户ID' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "username": "sample-sam2",
  "password": "12345678",
  "role": "default",
  "suspended": 0
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/v1/admin/users/{用户ID}'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体
```
{
  "username": "sample-sam2",  // 用户名不少于6位字符
  "password": "12345678",     // 密码不少于8位字符
  "role": "default | admin"  // default代表普通用户，admin代表管理员
  "suspended": 0
}
```
###  响应：
#### 1、响应体：
##### 响应状态：200
```
{
  "success": true,
  "error": null
}
```
##### 响应状态：401
```
AnythingLLM未处于多用户模式
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头：
```
 access-control-allow-origin: http://xxx.xxx.xxx.xxx:3001 
 connection: keep-alive 
 content-length: 29 
 content-type: application/json; charset=utf-8 
 date: Wed,28 Aug 2024 07:13:23 GMT 
 etag: W/"1d-i6U0PHpLtYnve+huEfmngzghAaU" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express
```
## 五、通过用户ID删除用户
```
curl -X 'DELETE' \
  'http://服务器IP:3001/api/v1/admin/users/用户ID' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：DELETE
#### 2、请求地址：'http://服务器IP:3001/api/v1/admin/users/{用户ID}'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "success": true,
  "error": null
}
```
##### 响应状态：401
```
AnythingLLM未处于多用户模式
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头：
```
 access-control-allow-origin: http://xxx.xxx.xxx.xxx:3001 
 connection: keep-alive 
 content-length: 29 
 content-type: application/json; charset=utf-8 
 date: Wed,28 Aug 2024 07:21:45 GMT 
 etag: W/"1d-i6U0PHpLtYnve+huEfmngzghAaU" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express
```
## 六、读取有权限访问指定工作区的用户列表
```
curl -X 'GET' \
  'http://服务器IP:3001/api/v1/admin/workspaces/工作区ID/users' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：GET
#### 2、请求地址：'http://服务器IP:3001/api/v1/admin/workspaces/{工作区ID}/users'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "users": [
    {
      "userId": 1,
      "username": "admin1",
      "role": "admin",
      "lastUpdatedAt": "2024-08-28T03:52:23.985Z"
    }
  ]
}
```
##### 响应状态：401
```
AnythingLLM未处于多用户模式
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头：
```
 connection: keep-alive 
 content-length: 102 
 content-type: application/json; charset=utf-8 
 date: Wed,28 Aug 2024 07:32:29 GMT 
 etag: W/"66-LAO7TC1b+mzvdCsuwGuRXdBfMOE" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 七、重写工作区权限，使其只能由给定的用户ID和管理员访问
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/admin/workspaces/工作区ID/update-users' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "userIds": [
    1,
    3
  ]
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/v1/admin/workspaces/{工作区ID}/update-users'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体
```
{
  "userIds": [
    1,
    3
  ]
}
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "success": true,
  "error": null
}
```
##### 响应状态：401
```
AnythingLLM未处于多用户模式
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头：
```
 access-control-allow-origin: http://xxx.xxx.xxx.xxx:3001 
 connection: keep-alive 
 content-length: 29 
 content-type: application/json; charset=utf-8 
 date: Wed,28 Aug 2024 07:42:20 GMT 
 etag: W/"1d-i6U0PHpLtYnve+huEfmngzghAaU" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express
```
## 八、上传一个新文件到AnythingLLM的文档存储目录
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/document/upload' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@入职指引手册1.pdf;type=application/pdf'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/v1/document/upload'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: multipart/form-data'
#### 4、请求体
```
'file=@入职指引手册1.pdf;type=application/pdf'
或是
'file=@大模型调研报告.docx;type=application/vnd.openxmlformats-officedocument.wordprocessingml.document'
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "success": true,
  "error": null,
  "documents": [
    {
      "id": "b77b9b21-4787-49d3-9f62-d384d62644ef",
      "url": "file://C:\\Users\\13007\\AppData\\Roaming\\anythingllm-desktop\\storage\\hotdir\\入职指引手册1.pdf",
      "title": "入职指引手册1.pdf",
      "docAuthor": "WPS 文字",
      "description": "No description found.",
      "docSource": "pdf file uploaded by the user.",
      "chunkSource": "",
      "published": "2024/8/26 09:35:13",
      "wordCount": 1,
      "pageContent": "入职指引手册\n亲爱的xxx\n欢迎您加入HITOSEA大家庭xxx\n",
      "token_count_estimate": 2298,
      "location": "C:\\Users\\13007\\AppData\\Roaming\\anythingllm-desktop\\storage\\documents\\custom-documents\\1.pdf-b77b9b21-4787-49d3-9f62-d384d62644ef.json"
    }
  ]
}
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 access-control-allow-origin: http://localhost:3001 
 connection: keep-alive 
 content-length: 6245 
 content-type: application/json; charset=utf-8 
 date: Mon,26 Aug 2024 01:35:14 GMT 
 etag: W/"1865-jjPVYk02YhMDxV2oqoLWiW7Tdlo" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 九、实例所有文档存储目录内的文件的列表
```
curl -X 'GET' \
  'http://服务器IP:3001/api/v1/documents' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：GET
#### 2、请求地址：'服务器IP/api/v1/documents'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
###  响应：
#### 1、响应体：
##### 响应状态：200
```
{
  "localFiles": {
    "name": "documents",
    "type": "folder",
    "items": [
      {
        "name": "custom-documents",
        "type": "folder",
        "items": [
          {
            "name": ".pdf-63233eaa-e9c6-41cc-9857-be4442f8a564.json",
            "type": "file",
            "id": "63233eaa-e9c6-41cc-9857-be4442f8a564",
            "url": "file://C:\\Users\\13007\\AppData\\Roaming\\anythingllm-desktop\\storage\\hotdir\\分享会细则-共享.pdf",
            "title": "分享会细则-共享.pdf",
            "docAuthor": "WPS 文字",
            "description": "No description found.",
            "docSource": "pdf file uploaded by the user.",
            "chunkSource": "localfile://C:\\Users\\13007\\Downloads\\分享会细则-共享.pdf",
            "published": "2024/8/22 17:22:52",
            "wordCount": 1,
            "token_count_estimate": 578,
            "cached": true,
            "pinnedWorkspaces": [],
            "canWatch": false,
            "watched": false
          },
          {
            "name": "1.pdf-b77b9b21-4787-49d3-9f62-d384d62644ef.json",
            "type": "file",
            "id": "b77b9b21-4787-49d3-9f62-d384d62644ef",
            "url": "file://C:\\Users\\13007\\AppData\\Roaming\\anythingllm-desktop\\storage\\hotdir\\入职指引手册1.pdf",
            "title": "入职指引手册1.pdf",
            "docAuthor": "WPS 文字",
            "description": "No description found.",
            "docSource": "pdf file uploaded by the user.",
            "chunkSource": "",
            "published": "2024/8/26 09:35:13",
            "wordCount": 1,
            "token_count_estimate": 2298,
            "cached": false,
            "pinnedWorkspaces": [],
            "canWatch": false,
            "watched": false
          }
        ]
      }
    ]
  }
}
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头：
```
 connection: keep-alive 
 content-length: 1253 
 content-type: application/json; charset=utf-8 
 date: Mon,26 Aug 2024 02:24:51 GMT 
 etag: W/"4e5-NKv7+2V9TGhB6ien53wCLYi7PHw" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 十、检查可上传的文件类型和MIME
```
curl -X 'GET' \
  'http://服务器IP:3001/api/v1/document/accepted-file-types' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：GET
#### 2、请求地址：'http://服务器IP:3001/api/v1/documents/accepted-file-types'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
###  响应：
#### 1、响应体：
##### 响应状态：200
```
{
  "types": {
    "text/plain": [
      ".txt",
      ".md",
      ".org",
      ".adoc",
      ".rst"
    ],
    "text/html": [
      ".html"
    ],
    "application/vnd.openxmlformats-officedocument.wordprocessingml.document": [
      ".docx"
    ],
    "application/vnd.openxmlformats-officedocument.presentationml.presentation": [
      ".pptx"
    ],
    "application/vnd.oasis.opendocument.text": [
      ".odt"
    ],
    "application/vnd.oasis.opendocument.presentation": [
      ".odp"
    ],
    "application/pdf": [
      ".pdf"
    ],
    "application/mbox": [
      ".mbox"
    ],
    "audio/wav": [
      ".wav"
    ],
    "audio/mpeg": [
      ".mp3"
    ],
    "video/mp4": [
      ".mp4"
    ],
    "video/mpeg": [
      ".mpeg"
    ],
    "application/epub+zip": [
      ".epub"
    ]
  }
}
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：404
```
Not Found
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 connection: keep-alive 
 content-length: 539 
 content-type: application/json; charset=utf-8 
 date: Mon,26 Aug 2024 02:40:41 GMT 
 etag: W/"21b-EaWQ5lnu+8EaAOJSSzZrz/3SbhI" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 十一、在文档存储目录内创建一个新文件夹
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/document/create-folder' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "new-folder"
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/v1/document/create-folder'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体
```
{
  "name": "new-folder"
}
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "success": true,
  "message": null
}
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 access-control-allow-origin: http://localhost:3001 
 connection: keep-alive 
 content-length: 31 
 content-type: application/json; charset=utf-8 
 date: Mon,26 Aug 2024 02:57:19 GMT 
 etag: W/"1f-0QHciDxBM1R+KE+c4xX6xe/FdrI" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 十二、在文件存储目录内移动文件
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/document/move-files' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "files": [
    {
      "from": "custom-documents/file.txt-fc4beeeb-e436-454d-8bb4-e5b8979cb48f.json",
      "to": "folder/file.txt-fc4beeeb-e436-454d-8bb4-e5b8979cb48f.json"
    }
  ]
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/v1/document/move-files'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体
```
{
  "files": [
    {
      "from": "custom-documents/file.txt-fc4beeeb-e436-454d-8bb4-e5b8979cb48f.json",
      "to": "folder/file.txt-fc4beeeb-e436-454d-8bb4-e5b8979cb48f.json"
    }
  ]
}
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "success": true,
  "message": null
}
```
##### 响应状态：500
```
{
  "success": false,
  "message": "Failed to move some files."
}
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
#### 2、响应头
```
 access-control-allow-origin: http://localhost:3001 
 connection: keep-alive 
 content-length: 56 
 content-type: application/json; charset=utf-8 
 date: Mon,26 Aug 2024 03:09:40 GMT 
 etag: W/"38-PMEV2hr36ttp0XS99fjB91IjhjE" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 十三、创建新的工作区
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/workspace/new' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "My New Workspace"
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/v1/workspace/new'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体
```
{
  "name": "My New Workspace"
}
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "workspace": {
    "id": 2,
    "name": "My New Workspace",
    "slug": "my-new-workspace",
    "vectorTag": null,
    "createdAt": "2024-08-26T03:23:14.006Z",
    "openAiTemp": null,
    "openAiHistory": 20,
    "lastUpdatedAt": "2024-08-26T03:23:14.006Z",
    "openAiPrompt": null,
    "similarityThreshold": 0.25,
    "chatProvider": null,
    "chatModel": null,
    "topN": 4,
    "chatMode": "chat",
    "pfpFilename": null,
    "agentProvider": null,
    "agentModel": null,
    "queryRefusalResponse": null
  },
  "message": null
}
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 access-control-allow-origin: http://localhost:3001 
 connection: keep-alive 
 content-length: 422 
 content-type: application/json; charset=utf-8 
 date: Mon,26 Aug 2024 03:23:14 GMT 
 etag: W/"1a6-9WzAkUufx+ovXm7JA8nNZ9a6Wss" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 十四、列出当前所有的工作区
```
curl -X 'GET' \
  'http://服务器IP:3001/api/v1/workspaces' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：GET
#### 2、请求地址：'http://服务器IP:3001/api/v1/workspaces'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
###  响应：
#### 1、响应体：
##### 响应状态：200
```
{
  "workspaces": [
    {
      "id": 1,
      "name": "test1",
      "slug": "test1",                                      // 工作区的唯一标号，后续经常用到
      "vectorTag": null,
      "createdAt": "2024-08-22T09:18:46.284Z",
      "openAiTemp": null,
      "openAiHistory": 20,
      "lastUpdatedAt": "2024-08-22T09:18:46.284Z",
      "openAiPrompt": null,
      "similarityThreshold": 0.25,
      "chatProvider": null,
      "chatModel": null,
      "topN": 4,
      "chatMode": "chat",
      "pfpFilename": null,
      "agentProvider": null,
      "agentModel": null,
      "queryRefusalResponse": null,
      "threads": [
        {
          "user_id": null,
          "slug": "eedbd9c2-ae12-4970-8672-745c9f49fa5d"  // 对话窗口的唯一标号，后续经常用到
        }
      ]
    },
    {
      "id": 2,
      "name": "My New Workspace",
      "slug": "my-new-workspace",
      "vectorTag": null,
      "createdAt": "2024-08-26T03:23:14.006Z",
      "openAiTemp": null,
      "openAiHistory": 20,
      "lastUpdatedAt": "2024-08-26T03:23:14.006Z",
      "openAiPrompt": null,
      "similarityThreshold": 0.25,
      "chatProvider": null,
      "chatModel": null,
      "topN": 4,
      "chatMode": "chat",
      "pfpFilename": null,
      "agentProvider": null,
      "agentModel": null,
      "queryRefusalResponse": null,
      "threads": []
    }
  ]
}
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 connection: keep-alive 
 content-length: 870 
 content-type: application/json; charset=utf-8 
 date: Mon,26 Aug 2024 03:31:17 GMT 
 etag: W/"366-FMwTEP1yYDxCWHUwZfoPjUwSeNk" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express
```
## 十五、通过工作区的唯一标号slug删除该工作区
```
curl -X 'DELETE' \
  'http://服务器IP:3001/api/v1/workspace/需要删除的工作区的slug' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：DELETE
#### 2、请求地址：'http://服务器IP:3001/api/v1/workspaces/{工作区的slug}'
#### 3、请求头：
```
'accept: */*'
'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
###  响应：
#### 1、响应体：
##### 响应状态：200
```
OK
```
##### 响应状态：400
```
Bad Request
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 access-control-allow-origin: http://localhost:3001 
 connection: keep-alive 
 content-length: 11 
 content-type: text/plain; charset=utf-8 
 date: Mon,26 Aug 2024 03:45:27 GMT 
 etag: W/"b-EFiDB1U+dmqzx9Mo2UjcZ1SJPO8" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 十六、通过工作区的唯一标号slug更新工作区设置
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/workspace/需要更新的工作区的slug/update' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "Updated Workspace Name",
  "openAiTemp": 0.2,
  "openAiHistory": 20,
  "openAiPrompt": "Respond to all inquires and questions in binary - do not respond in any other format."
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/v1/workspace/{工作区的slug}/update'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体
```
{
  "name": "Updated Workspace Name",
  "openAiTemp": 0.2,                                                                                        // 模型温度，数字越高模型越有创意
  "openAiHistory": 20,                                                                                      // 模型记忆中的先前聊天的数量，推荐20，任何超过45的值都可能导致连续聊天失败
  "openAiPrompt": "Respond to all inquires and questions in binary - do not respond in any other format."  // 角色预设
}
```
###  响应：
#### 1、响应体：
##### 响应状态：200
```
{
  "workspace": {
    "id": 8,
    "name": "Updated Workspace Name",
    "slug": "test4",
    "vectorTag": null,
    "createdAt": "2024-08-28T08:27:06.404Z",
    "openAiTemp": 0.2,
    "openAiHistory": 20,
    "lastUpdatedAt": "2024-08-28T08:27:06.404Z",
    "openAiPrompt": "Respond to all inquires and questions in binary - do not respond in any other format.",
    "similarityThreshold": 0.25,
    "chatProvider": null,
    "chatModel": null,
    "topN": 4,
    "chatMode": "chat",
    "pfpFilename": null,
    "agentProvider": null,
    "agentModel": null,
    "queryRefusalResponse": null
  },
  "message": null
}
```
#### 响应状态：400
```
Bad Request
```
#### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 access-control-allow-origin: http://xxx.xxx.xxx.xxx:3001 
 connection: keep-alive 
 content-length: 499 
 content-type: application/json; charset=utf-8 
 date: Wed,28 Aug 2024 08:27:38 GMT 
 etag: W/"1f3-+ljC1kxaJFViGuqicLcJXi6e1GQ" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 十七、通过工作区的唯一标号slug添加或删除工作区中的文件
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/workspace/需要进行操作的工作区的slug/update-embeddings' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "adds": [
    "custom-documents/my-pdf.pdf-hash.json"
  ],
  "deletes": [
    "custom-documents/anythingllm.txt-hash.json"
  ]
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/v1/workspaces/{工作区的slug}/update-embeddings'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体：
```
{
  "adds": [
    "custom-documents/my-pdf.pdf-hash.json"
  ],
  "deletes": [
    "custom-documents/anythingllm.txt-hash.json"
  ]
}
```
###  响应：
#### 1、响应体：
##### 响应状态：200
```
{
  "workspace": {
    "id": 1,
    "name": "test1",
    "slug": "test1",
    "vectorTag": null,
    "createdAt": "2024-08-22T09:18:46.284Z",
    "openAiTemp": null,
    "openAiHistory": 20,
    "lastUpdatedAt": "2024-08-22T09:18:46.284Z",
    "openAiPrompt": null,
    "similarityThreshold": 0.25,
    "chatProvider": null,
    "chatModel": null,
    "topN": 4,
    "chatMode": "chat",
    "pfpFilename": null,
    "agentProvider": null,
    "agentModel": null,
    "queryRefusalResponse": null,
    "documents": [
      {
        "id": 1,
        "docId": "30adaa77-1b15-4ca3-bb21-8b7d489c6349",
        "filename": ".pdf-63233eaa-e9c6-41cc-9857-be4442f8a564.json",
        "docpath": "custom-documents/.pdf-63233eaa-e9c6-41cc-9857-be4442f8a564.json",
        "workspaceId": 1,
        "metadata": "{\"id\":\"63233eaa-e9c6-41cc-9857-be4442f8a564\",\"url\":\"file://C:\\\\Users\\\\13007\\\\AppData\\\\Roaming\\\\anythingllm-desktop\\\\storage\\\\hotdir\\\\分享会细则-共享.pdf\",\"title\":\"分享会细则-共享.pdf\",\"docAuthor\":\"WPS 文字\",\"description\":\"No description found.\",\"docSource\":\"pdf file uploaded by the user.\",\"chunkSource\":\"localfile://C:\\\\Users\\\\13007\\\\Downloads\\\\分享会细则-共享.pdf\",\"published\":\"2024/8/22 17:22:52\",\"wordCount\":1,\"token_count_estimate\":578}",
        "pinned": false,
        "watched": false,
        "createdAt": "2024-08-22T09:23:07.768Z",
        "lastUpdatedAt": "2024-08-22T09:23:07.768Z"
      }
    ]
  }
}
```
#### 响应状态：400
```
Bad Request
```
#### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 access-control-allow-origin: http://localhost:3001 
 connection: keep-alive 
 content-length: 1258 
 content-type: application/json; charset=utf-8 
 date: Mon,26 Aug 2024 06:03:01 GMT 
 etag: W/"4ea-aX9UiZZT8MYc+on28vB7QCuoOwY" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express
```
## 十八、在某个工作区中通过工作区唯一标号slug添加或删除图钉（图钉相当于”置顶文档“，当模型对某个文档理解不理想时，通过添加图钉让模型增强对该文档的理解）
```
curl -X 'POST' \
  'http://服务器IP:3001/api/workspace/需要进行操作的工作区的slug/update-pin' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "docPath": "custom-documents/my-pdf.pdf-hash.json",
  "pinStatus": true
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/workspaces/{工作区的slug}/update-pin'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体：
```
{
  "docPath": "custom-documents/my-pdf.pdf-hash.json",
  "pinStatus": true                                     // 或是flase
}
```
###  响应：
#### 1、响应体：
##### 响应状态：200
```
{
  "message": "Pin status updated successfully"
}
```
##### 响应状态：404
```
Not Found
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 access-control-allow-origin: http://localhost:3001 
 connection: keep-alive 
 content-length: 9 
 content-type: text/plain; charset=utf-8 
 date: Mon,26 Aug 2024 06:59:14 GMT 
 etag: W/"9-0gXL1ngzMqISxa6S1zx3F4wtLyg" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 十九、通过API密钥与工作区进行对话
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/workspace/需要进行对话的工作区的slug/chat' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "message": "分享会的开始时间?",
  "mode": "chat"
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/v1/workspace/{工作区的slug}/chat'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体：
```
{
  "message": "分享会的开始时间?",
  "mode": "query | chat"         // query为查询模式，chat为聊天模式
}
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "id": "271802f6-d883-48dc-b5c9-a6695c3c49a7",
  "type": "textResponse",
  "close": true,
  "error": null,
  "chatId": 6,
  "textResponse": "每周五下午17:00。",
  "sources": [
    {
      "id": "ae01ac32-d935-4779-b09c-0388e47f5070",
      "url": "file://C:\\Users\\13007\\AppData\\Roaming\\anythingllm-desktop\\storage\\hotdir\\分享会细则-共享.pdf",
      "title": "分享会细则-共享.pdf",
      "docAuthor": "WPS 文字",
      "description": "No description found.",
      "docSource": "pdf file uploaded by the user.",
      "chunkSource": "localfile://C:\\Users\\13007\\Downloads\\分享会细则-共享.pdf",
      "published": "2024/8/22 17:22:52",
      "wordCount": 1,
      "token_count_estimate": 578,
      "text": "<document_metadata>\nsourceDocument: 分享会细则-共享.pdf\npublished: 2024/8/22 17:22:52\n</document_metadata>\n\nxxx",
      "_distance": 0.23625129461288452,
      "score": 0.7637487053871155
    },
    {
      "id": "60dd3407-e729-425e-9671-180faf2edd91",
      "url": "file://C:\\Users\\13007\\AppData\\Roaming\\anythingllm-desktop\\storage\\hotdir\\分享会细则-共享.pdf",
      "title": "分享会细则-共享.pdf",
      "docAuthor": "WPS 文字",
      "description": "No description found.",
      "docSource": "pdf file uploaded by the user.",
      "chunkSource": "localfile://C:\\Users\\13007\\Downloads\\分享会细则-共享.pdf",
      "published": "2024/8/22 17:22:52",
      "wordCount": 1,
      "token_count_estimate": 578,
      "text": "<document_metadata>\nsourceDocument: 分享会细则-共享.pdf\npublished: 2024/8/22 17:22:52\n</document_metadata>\n\nxxx",
      "_distance": 0.2597131133079529,
      "score": 0.7402868866920471
    },
    {
      "id": "81f17a4e-e8f9-46e7-8be8-edc1bd073973",
      "url": "file://C:\\Users\\13007\\AppData\\Roaming\\anythingllm-desktop\\storage\\hotdir\\分享会细则-共享.pdf",
      "title": "分享会细则-共享.pdf",
      "docAuthor": "WPS 文字",
      "description": "No description found.",
      "docSource": "pdf file uploaded by the user.",
      "chunkSource": "localfile://C:\\Users\\13007\\Downloads\\分享会细则-共享.pdf",
      "published": "2024/8/22 17:22:52",
      "wordCount": 1,
      "token_count_estimate": 578,
      "text": "<document_metadata>\nsourceDocument: 分享会细则-共享.pdf\npublished: 2024/8/22 17:22:52\n</document_metadata>\n\nxxx",
      "_distance": 0.3002476096153259,
      "score": 0.6997523903846741
    }
  ]
}
```
##### 响应状态：400
```
Bad Request
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 access-control-allow-origin: http://localhost:3001 
 connection: keep-alive 
 content-length: 3714 
 content-type: application/json; charset=utf-8 
 date: Mon,26 Aug 2024 07:14:41 GMT 
 etag: W/"e82-ZcCxi2uXiOGxGz3/8XUvansSFpM" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express
```
## 二十、使用API与工作区执行流式聊天
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/workspace/需要进行对话的工作区的slug/stream-chat' \
  -H 'accept: text/event-stream' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "message": "分享会有什么用?",
  "mode": "chat"
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://服务器IP:3001/api/v1/workspace/{工作区的slug}/stream-chat'
#### 3、请求头：
'accept: text/event-stream'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体：
```
{
  "message": "分享会的开始时间?",
  "mode": "query | chat"        // query为查询模式，chat为聊天模式
}
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"分享","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"会有","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"以下","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"用途","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"：\n","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"1","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":".","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":" 促进","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"知识","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"共享","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"与","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"团队","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"成长","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"。\n","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"2","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":".","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":" 激","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"发","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"创新","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"思维","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"与","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"灵感","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"。\n","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"3","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":".","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":" 增","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"强","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"团队","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"凝聚力","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"与合作","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"精神","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"。\n","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"4","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":".","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":" 分","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"享","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"工作","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"技能","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"与方法","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"。\n","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"5","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":".","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":" ","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"交流","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"成功","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"案例","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"与","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"经验","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"教训","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"。\n","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"6","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":".","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":" 了解","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"行业","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"动态","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"与","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"前沿","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"资讯","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"。\n","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"7","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":".","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":" 关注","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"个人","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"成长","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"与","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"职业","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"发展","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"。","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[],"type":"textResponseChunk","textResponse":"","close":false,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","sources":[{"id":"ae01ac32-d935-4779-b09c-0388e47f5070","url":"file://C:\\Users\\13007\\AppData\\Roaming\\anythingllm-desktop\\storage\\hotdir\\分享会细则-共享.pdf","title":"分享会细则-共享.pdf","docAuthor":"WPS 文字","description":"No description found.","docSource":"pdf file uploaded by the user.","chunkSource":"localfile://C:\\Users\\13007\\Downloads\\分享会细则-共享.pdf","published":"2024/8/22 17:22:52","wordCount":1,"token_count_estimate":578,"text":"<document_metadata>\nsourceDocument: 分享会细则-共享.pdf\npublished: 2024/8/22 17:22:52\n</document_metadata>\n\nxxx\n分享会细则\n一、目的\n促进知识共享与团队成长、激发创新思维与灵感、增强团队凝聚力与合作精神。\n二、分享内容（三次至少有一次与工作相关）\n1、工作技能与方法\n2、成功案例与经验教训\n3、涉及相关的行业动态与前沿资讯\n4、个人成长与职业发展\n三、分享会规则及执行\n1、分享人员选定\n①报名方式：自愿报名或部门轮流的方式（提前一周报名）\n2、参会人员规定\n根据分享会主题而定，例如是技术分享会，则技术人员必须参加，非技术部门\n不强制参与。\n3、分享时间与频率","_distance":0.25364476442337036,"score":0.7463552355766296},{"id":"60dd3407-e729-425e-9671-180faf2edd91","url":"file://C:\\Users\\13007\\AppData\\Roaming\\anythingllm-desktop\\storage\\hotdir\\分享会细则-共享.pdf","title":"分享会细则-共享.pdf","docAuthor":"WPS 文字","description":"No description found.","docSource":"pdf file uploaded by the user.","chunkSource":"localfile://C:\\Users\\13007\\Downloads\\分享会细则-共享.pdf","published":"2024/8/22 17:22:52","wordCount":1,"token_count_estimate":578,"text":"<document_metadata>\nsourceDocument: 分享会细则-共享.pdf\npublished: 2024/8/22 17:22:52\n</document_metadata>\n\n不强制参与。\n3、分享时间与频率\n①时间及地点：每周五下午17:00于办公室定期举办；\n②时长：每组30分钟以内，确保内容充实又不冗长；\n③场次：每场限2组以内分享。\n3、分享形式\n①可以采用演讲、案例分析、小组讨论、互动问答等多种形式；\n②辅助工具：结合使用多媒体资料，如PPT、视频等，增强分享的效果。\n4、反馈与评估\n分享结束后，人力行政部组织参会人线上填写《XXX分享会》反馈评价，并提\n出相关看法或建议。\n5、激励机制\n①对积极参与分享且效果良好的成员给予一定的奖励，不限于现金红包、小礼","_distance":0.29510271549224854,"score":0.7048972845077515},{"id":"81f17a4e-e8f9-46e7-8be8-edc1bd073973","url":"file://C:\\Users\\13007\\AppData\\Roaming\\anythingllm-desktop\\storage\\hotdir\\分享会细则-共享.pdf","title":"分享会细则-共享.pdf","docAuthor":"WPS 文字","description":"No description found.","docSource":"pdf file uploaded by the user.","chunkSource":"localfile://C:\\Users\\13007\\Downloads\\分享会细则-共享.pdf","published":"2024/8/22 17:22:52","wordCount":1,"token_count_estimate":578,"text":"<document_metadata>\nsourceDocument: 分享会细则-共享.pdf\npublished: 2024/8/22 17:22:52\n</document_metadata>\n\nxxx","_distance":0.3104579448699951,"score":0.6895420551300049}],"type":"textResponseChunk","textResponse":"","close":true,"error":false}

data: {"uuid":"ede36b58-015f-487d-8dee-3dcd3a19bfe0","type":"finalizeResponseStream","close":true,"error":false,"chatId":7}
```
##### 响应状态：400
```
Bad Request
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
#### 2、响应头
```
 access-control-allow-origin: * 
 cache-control: no-cache 
 connection: keep-alive 
 content-type: text/event-stream 
 date: Mon,26 Aug 2024 07:48:55 GMT 
 transfer-encoding: chunked 
 vary: Origin 
 x-powered-by: Express 
```
## 二十一、从系统中永久删除文件
```
curl -X 'DELETE' \
  'http://服务器IP:3001/api/v1/system/remove-documents' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "names": [
    "custom-documents/file.txt-fc4beeeb-e436-454d-8bb4-e5b8979cb48f.json"
  ]
}'
```
### 请求：DELETE
#### 1、请求方法：
#### 2、请求地址：'http://服务器IP:3001/api/v1/system/remove-documents'
#### 3、请求头：
'accept: text/event-stream'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体：
```
{
  "names": [
    "custom-documents/file.txt-fc4beeeb-e436-454d-8bb4-e5b8979cb48f.json"
  ]
}
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "success": true,
  "message": "Documents removed successfully"
}
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 access-control-allow-origin: http://xxx.xxx.xxx.xxx:3001 
 connection: keep-alive 
 content-length: 59 
 content-type: application/json; charset=utf-8 
 date: Wed,28 Aug 2024 09:36:02 GMT 
 etag: W/"3b-Kgj0rUX7Wfdzzchh6ZxCoMOPsuA" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 二十二、在某个工作区新建对话窗口
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/workspace/需要新建对话的工作区的slug/thread/new' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "userId": 1
}'
```
### 请求：POST
#### 1、请求方法：
#### 2、请求地址：'http://服务器IP:3001/api/v1/workspace/{工作区的slug}/thread/new'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体：
```
{
  "userId": 1
}
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "thread": {
    "id": 20,
    "name": "Thread",
    "slug": "a8fe6a14-440a-4caf-9f70-c208981f7bec",    // 新建成功的对话窗口的ID
    "workspace_id": 8,                                 // 工作区的ID
    "user_id": 1,
    "createdAt": "2024-08-28T09:27:23.531Z",
    "lastUpdatedAt": "2024-08-28T09:27:23.531Z"
  },
  "message": null
}
```
##### 响应状态：400
```
Bad Request
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 access-control-allow-origin: http://xxx.xxx.xxx.xxx:3001 
 connection: keep-alive 
 content-length: 208 
 content-type: application/json; charset=utf-8 
 date: Wed,28 Aug 2024 09:27:23 GMT 
 etag: W/"d0-GJtrPgrS2KeUAaw/GQ7da52NI6s" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```
## 二十三、在某个工作区删除对话窗口
```
curl -X 'DELETE' \
  'http://服务器IP:3001/api/v1/workspace/需要删除对话所在的工作区的slug/thread/需要删除对话的slug' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：DELETE
#### 1、请求方法：
#### 2、请求地址：'http://服务器IP:3001/api/v1/workspace/{工作区的slug}/thread/{对话窗口的slug}'
#### 3、请求头：
```
'accept: */*'
'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
OK
```
##### 响应状态：400
```
Bad Request
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
## 二十四、在某个工作区的新建对话窗口进行聊天
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/workspace/需要进行对话的工作区的slug/thread/需要进行对话的窗口的slug/chat' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "message": "分享会什么时候开始?",
  "mode": "chat",
  "userId": 1
}'
```
### 请求：POST
#### 1、请求方法：
#### 2、请求地址：'http://服务器IP:3001/api/v1/workspace/{工作区的slug}/thread/{对话窗口的slug}/chat'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体：
```
{
  "message": "分享会什么时候开始?",
  "mode": "query | chat"          // query为查询模式，chat为聊天模式
  "userId": 1
}
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "id": "0807fe42-fa14-4f87-9f32-f64a67ad3f63",
  "type": "textResponse",
  "close": true,
  "error": null,
  "chatId": 61,
  "textResponse": "每周五下午17:00开始。",
  "sources": [
    {
      "id": "8ea8860f-b39b-4093-8185-2542a67335c1",
      "url": "file:///app/collector/hotdir/分享会细则-共享.pdf",
      "title": "分享会细则-共享.pdf",
      "docAuthor": "WPS 文字",
      "description": "No description found.",
      "docSource": "pdf file uploaded by the user.",
      "chunkSource": null,
      "published": "8/28/2024, 3:45:10 AM",
      "wordCount": 1,
      "token_count_estimate": 578,
      "text": "<document_metadata>\nsourceDocument: 分享会细则-共享.pdf\npublished: 8/28/2024, 3:45:10 AM\n</document_metadata>\n\nxxx\nxxx",
      "_distance": 0.3431391716003418,
      "score": 0.6568608283996582
    },
    {
      "id": "f2af6fc1-a80e-4d5f-8970-8c5ee4a63094",
      "url": "file:///app/collector/hotdir/分享会细则-共享.pdf",
      "title": "分享会细则-共享.pdf",
      "docAuthor": "WPS 文字",
      "description": "No description found.",
      "docSource": "pdf file uploaded by the user.",
      "chunkSource": null,
      "published": "8/28/2024, 3:45:10 AM",
      "wordCount": 1,
      "token_count_estimate": 578,
      "text": "<document_metadata>\nsourceDocument: 分享会细则-共享.pdf\npublished: 8/28/2024, 3:45:10 AM\n</document_metadata>\n\nxxx",
      "_distance": 0.5512117743492126,
      "score": 0.44878822565078735
    }
  ]
}
```
##### 响应状态：400
```
Bad Request
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 access-control-allow-origin: http://xxx.xxx.xxx.xxx:3001 
 connection: keep-alive 
 content-length: 2801 
 content-type: application/json; charset=utf-8 
 date: Wed,28 Aug 2024 10:04:35 GMT 
 etag: W/"af1-gafuoMXI3fi8r9gSaIbgzL/yOyM" 
 keep-alive: timeout=5 
 vary: Origin 
 x-powered-by: Express 
```

## 二十五、在某个工作区的新建对话列表进行流式聊天
```
curl -X 'POST' \
  'http://服务器IP:3001/api/v1/workspace/需要进行对话的所在的工作区的slug/thread/需要进行对话的窗口的slug/stream-chat' \
  -H 'accept: text/event-stream' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "message": "一场分享会的时长是多久？",
  "mode": "chat",
  "userId": 1
}'
```
### 请求：POST
#### 1、请求方法：
#### 2、请求地址：'http://服务器IP:3001/api/v1/workspace/{工作区的slug}/thread/{对话窗口的slug}/stream-chat'
#### 3、请求头：
'accept: text/event-stream'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体：
```
{
  "message": "分享会什么时候开始?",
  "mode": "query | chat"          // query为查询模式，chat为聊天模式
  "userId": 1
}
```
### 响应
#### 1、响应体：
##### 响应状态：200
```
data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"一场","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"分享","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"会","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"的时间","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"限制","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"为","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"每组","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"30","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"分钟","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"以内","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"。","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[],"type":"textResponseChunk","textResponse":"","close":false,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","sources":[{"id":"8ea8860f-b39b-4093-8185-2542a67335c1","url":"file:///app/collector/hotdir/分享会细则-共享.pdf","title":"分享会细则-共享.pdf","docAuthor":"WPS 文字","description":"No description found.","docSource":"pdf file uploaded by the user.","chunkSource":null,"published":"8/28/2024, 3:45:10 AM","wordCount":1,"token_count_estimate":578,"text":"<document_metadata>\nsourceDocument: 分享会细则-共享.pdf\npublished: 8/28/2024, 3:45:10 AM\n</document_metadata>\n\nxxx","_distance":0.3652048110961914,"score":0.6347951889038086},{"id":"f2af6fc1-a80e-4d5f-8970-8c5ee4a63094","url":"file:///app/collector/hotdir/分享会细则-共享.pdf","title":"分享会细则-共享.pdf","docAuthor":"WPS 文字","description":"No description found.","docSource":"pdf file uploaded by the user.","chunkSource":null,"published":"8/28/2024, 3:45:10 AM","wordCount":1,"token_count_estimate":578,"text":"<document_metadata>\nsourceDocument: 分享会细则-共享.pdf\npublished: 8/28/2024, 3:45:10 AM\n</document_metadata>\n\nxxx","_distance":0.5283359885215759,"score":0.4716640114784241}],"type":"textResponseChunk","textResponse":"","close":true,"error":false}

data: {"uuid":"4790ca06-2eb2-4c54-9a59-6bbc0d19f1bb","type":"finalizeResponseStream","close":true,"error":false,"chatId":64}

```
##### 响应状态：400
```
Bad Request
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
#### 2、响应头
```
 access-control-allow-origin: * 
 cache-control: no-cache 
 connection: keep-alive 
 content-type: text/event-stream 
 date: Wed,28 Aug 2024 10:18:41 GMT 
 transfer-encoding: chunked 
 vary: Origin 
 x-powered-by: Express 
```
## 二十六、列出AnythingLLM的所有用户
```
curl -X 'GET' \
  'http://服务器IP:3001/api/v1/users' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：GET
#### 1、请求方法：
#### 2、请求地址：'http://服务器IP:3001/api/v1/users'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
### 响应
#### 1、响应体：
##### 响应状态：200
```
{
  "users": [
    {
      "id": 1,
      "username": "admin1",
      "role": "admin"
    },
    {
      "id": 3,
      "username": "sample-sam",
      "role": "default"
    }
  ]
}
```
##### 响应状态：401
```
AnythingLLM未处于多用户模式
```
##### 响应状态：403
```
{
  "message": "Invalid API Key"
}
```
##### 响应状态：500
```
内部服务器错误
```
#### 2、响应头
```
 content-length: 105 
 content-type: application/json; charset=utf-8 
 date: Wed,28 Aug 2024 10:30:29 GMT 
 etag: W/"69-KdC3+5v7felIATEMnojkYD6OtkE" 
 vary: Origin 
 x-powered-by: Express 
```


