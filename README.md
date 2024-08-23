# AnythingLLM的API接口用法

## 一、验证API密钥是否有效（无需传参）
curl -X 'GET' \
  'http://192.168.100.153:3001/api/v1/auth' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer G0BM9Y3-MTVMFTR-QJNC7R5-84NF5B3'


请求结果：
成功（200）返回
{
  "authenticated": true
}
失败（403）返回
{
  "message": "Invalid API Key"
}


二、111
