# sshTunnel

## Description

ssh tunnel forwarding library for Go. Implemented using golang.org/x/crypto/ssh . Like linux command:

```shell
ssh -N -f -L 3307:remoteHost:3306 sshUsername@sshHostname
```

## Installation

```shell
go get -u github.com/alwaysthanks/sshTunnel
```

## Examples

### 1.simple ssh forwarding

```go
sshTool, err := NewSSHTool(sshHostname, sshUsername, sshPassword, "")
if err != nil {

}
ctx, cancel := context.WithCancel(context.Background())
defer cancel()
proxyServer, err := NewTunnelServer(ctx, localAddr, remoteAddr, sshTool)
if err != nil {

}
//run ssh proxy
go proxyServer.Start()
//begin your service
```

### 2.use ssh connections pool

```go
sshTool, err := NewSSHTool(sshHostname, sshUsername, sshPassword, "")
if err != nil {

}
ctx, cancel := context.WithCancel(context.Background())
defer cancel()
//here use ssh pool
proxyServer, err := NewTunnelServerWithPool(ctx, localAddr, remoteAddr, sshTool)
if err != nil {

}
//run ssh proxy
go proxyServer.Start()
//begin your service
```
## License
View the [LICENSE](https://github.com/alwaysthanks/sshTunnel/blob/master/LICENSE) file