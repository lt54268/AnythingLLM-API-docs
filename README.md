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
## 十、通过工作区的唯一标号slug删除该工作区
```
curl -X 'DELETE' \
  'http://192.168.100.153:3001/api/v1/workspace/需要删除的工作区的slug' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
```
### 请求：
#### 1、请求方法：DELETE
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/workspaces/{slug}'
#### 3、请求头：
```
'accept: */*'
```
'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'
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
## 十一、通过工作区的唯一标号slug添加或删除工作区中的文件
```
curl -X 'POST' \
  'http://192.168.100.153:3001/api/v1/workspace/需要进行操作的工作区的slug/update-embeddings' \
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
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/workspaces/{slug}/update-embeddings'
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
## 十二、在某个工作区中通过工作区唯一标号slug添加或删除图钉（图钉相当于”置顶文档“，当模型对某个文档理解不理想时，通过添加图钉让模型增强对该文档的理解）
```
curl -X 'POST' \
  'http://192.168.100.153:3001/api/workspace/需要进行操作的工作区的slug/update-pin' \
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
#### 2、请求地址：'http://192.168.100.153:3001/api/workspaces/{slug}/update-pin'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体：
```
{
  "docPath": "custom-documents/my-pdf.pdf-hash.json",
  "pinStatus": true
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
## 十三、与工作区进行对话
```
curl -X 'POST' \
  'http://192.168.100.153:3001/api/v1/workspace/需要进行对话的工作区的slug/chat' \
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
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/workspace/{slug}/chat'
#### 3、请求头：
'accept: application/json'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体：
```
{
  "message": "分享会的开始时间?",
  "mode": "query | chat"
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
## 十四、使用工作区执行流式聊天
```
curl -X 'POST' \
  'http://192.168.100.153:3001/api/v1/workspace/需要进行对话的工作区的slug/stream-chat' \
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
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/workspace/{slug}/stream-chat'
#### 3、请求头：
'accept: text/event-stream'

'Authorization: Bearer G0xxx-xxx-xxx-xxxB3'

'Content-Type: application/json'
#### 4、请求体：
```
{
  "message": "分享会的开始时间?",
  "mode": "query | chat"
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
## 十五、从系统中永久删除文件
```
curl -X 'DELETE' \
  'http://192.168.100.153:3001/api/v1/system/remove-documents' \
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
#### 2、请求地址：'http://192.168.100.153:3001/api/v1/system/remove-documents'
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
## 十六、
