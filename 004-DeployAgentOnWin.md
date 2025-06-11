 # DeployAgentOnWin

# Download sensuctl for Windows amd64
Invoke-WebRequest https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/6.12.0/sensu-go_6.12.0_windows_amd64.zip  -OutFile C:\Users\Administrator\sensu-go_6.12.0_windows_amd64.zip

# Unzip the file with PowerShell for Windows amd64
Expand-Archive -LiteralPath 'C:\Users\Administrator\sensu-go_6.12.0_windows_amd64.zip' -DestinationPath 'C:\\Program Files\sensu\sensuctl\bin'

Note : the path wasnt' setup automatically

# Configure the cli

```
sensuctl configure -n `
  --username "admin" `
  --password "1qa2ws3eD!" `
  --namespace "default" `
  --url "http://10.0.99.10:8080"
```

# Download the Sensu agent for Windows amd64
```
Invoke-WebRequest https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/6.12.0/sensu-go-agent_6.12.0.7321_en-US.x64.msi  -OutFile "$env:userprofile\sensu-go-agent_6.12.0.7321_en-US.x64.msi"
```

# Install the Sensu agent for Windows amd64
```
msiexec.exe /i $env:userprofile\sensu-go-agent_6.12.0.7321_en-US.x64.msi /qn
```

Note : the path was setup automatically
