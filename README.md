##this is docker with small picture generator for anythingllm testing - download docker file from:
[https://drive.google.com/file/d/1lUEAYyCwRgGWqOpryeYJYHt9XLsROSGW/view?usp=sharing]

there is a special tool "generate_pictest" that doesn't require interaction with grafana, it returns base64 string for small picture.

##after downloading load docker:

docker load < grafana-mcp-integration.tar

##Command to start docker (may depend on your grafana server configuration):

sudo docker run -d \
  --name grafana-mcp-integration \
  -p 9001:3000 \
  -e GRAFANA_URL=https://<YOUR_GRAFANA_IP_ADDRESS> \
  -e GRAFANA_TOKEN=<YOUR_GRAFANA_TOKEN> \
  -e GRAFANA_VERIFY_SSL=false \
  -e RENDER_TIMEOUT_MS=120000 \
  -e MCP_REQUEST_TIMEOUT_MS=180000 \
  -e LOG_LEVEL=debug \
  grafana-mcp-integration:latest

##configuration of mcp for anythingllm

{
    "mcpServers":  {
      "grafana": {
        "url":"http://<YOUR_SERVER_HOSTING_MCP_IP_ADDRESS>:9001/sse",
        "type":"sse"
      }
    }
  }

##query for anythingllm (may depent on your LLM):
  
  @agent grafana image use generate_pictest
