
# 完整方法
0.准备：gpt plus或pro账号，良好
1.确定代理端口，在clash的设置里能看，一般是7897或7890

2.使用反向隧道将本地端口暴露给远端，
ssh -N -R <远端端口，一般为7890>:127.0.0.1:<本地端口> -o ExitOnForwardFailure=yes -o ServerAliveInterval=60 -o ServerAliveCountMax=3 -p <远端SSH端口> <远端用户名>@<远端IP>

3.配置服务器代理：
如果上面远端端口选7890的话，这里就是：
export HTTP_PROXY=http://127.0.0.1:7890
export HTTPS_PROXY=http://127.0.0.1:7890

4.测试代理是否正常工作：
curl -sI -x http://127.0.0.1:7890 https://api.openai.com/v1/models | head -n1

应该返回401或者200

# 极简方法
直接问ai：
提示词：请向我解释如何通过使用SSH反向隧道技术，让远程服务器能够通过我的本机代理访问 OpenAI的codex；然后把自己的ssh ip发给ai让它帮你填就行；
注意检查一下ai给的流程与上面完整方法差异