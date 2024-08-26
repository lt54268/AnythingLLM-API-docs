# AnythingLLM的API接口用法
## 一、验证API密钥是否有效
```
curl -X 'GET' \
  'http://192.168.100.153:3001/api/v1/auth' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：GET
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/auth'
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
## 二、上传一个新文件到AnythingLLM的文档存储目录
```
curl -X 'POST' \
  'http://192.168.100.153:3001/api/v1/document/upload' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@入职指引手册1.pdf;type=application/pdf'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/document/upload'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: multipart/form-data'
#### 4、请求体
'file=@入职指引手册1.pdf;type=application/pdf'
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
## 三、实例所有文档存储目录内的文件的列表
```
curl -X 'GET' \
  'http://192.168.100.153:3001/api/v1/documents' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：GET
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/documents'
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
## 四、检查可上传的文件类型和MIME
```
curl -X 'GET' \
  'http://192.168.100.153:3001/api/v1/document/accepted-file-types' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：GET
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/documents/accepted-file-types'
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
## 五、在文档存储目录内创建一个新文件夹
```
curl -X 'POST' \
  'http://192.168.100.153:3001/api/v1/document/create-folder' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "new-folder"
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/document/create-folder'
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
## 六、在文件存储目录内移动文件
```
curl -X 'POST' \
  'http://192.168.100.153:3001/api/v1/document/move-files' \
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
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/document/move-files'
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
## 七、创建新的工作区
```
curl -X 'POST' \
  'http://192.168.100.153:3001/api/v1/workspace/new' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "My New Workspace"
}'
```
### 请求：
#### 1、请求方法：POST
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/workspace/new'
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
## 八、列出当前所有的工作区
```
curl -X 'GET' \
  'http://192.168.100.153:3001/api/v1/workspaces' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：GET
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/workspaces'
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
      "threads": [
        {
          "user_id": null,
          "slug": "eedbd9c2-ae12-4970-8672-745c9f49fa5d"
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
## 十、通过工作区的slug删除该工作区
```
curl -X 'DELETE' \
  'http://192.168.100.153:3001/api/v1/workspace/需要删除的工作区的slug' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：DELETE
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/workspaces/*slug'
#### 3、请求头：
'accept: */*'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
###  响应：
#### 1、响应体：
##### 响应状态：200
```
OK
```
