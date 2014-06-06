# 结构 UDPConn
    
    type UDPConn struct {}

UDPConn是Conn接口的实现

## func DialUDP(net string, laddr, raddr *UDPAddr) (*UDPConn, error)

参数列表

- net UDP类型
- laddr 本地地址

返回值：

- *UDPConn UDP连接
- error 错误(如果有)

功能说明：

打开一个UDP句柄,用于后续操作

代码实例：
@todo

## func ListenMulticastUDP(net string, ifi *Interface, gaddr *UDPAddr) (*UDPConn, error)

参数列表

- net UDP类型
- ifi @todo
- gaddr @todo

返回值：

- *UDPConn UDP句柄
- error 错误(如果有)

功能说明：
@todo

代码实例：
@todo


## func ListenUDP(net string, laddr *UDPAddr) (*UDPConn, error)

参数列表

- net UDP类型
- laddr 本地地址

返回值：

- *UDPConn UDP句柄
- error 错误(如果有)

功能说明：

监听本地UDP端口

代码实例：
@todo

## func (c *UDPConn) Close() error

返回值：

- error 错误(如果有)

功能说明：

关闭UDP句柄

代码实例：
@todo

## func (c *UDPConn) File() (f *os.File, err error)

返回值：
- f 文件流句柄
- error 错误(如果有)

功能说明：

获取文件流句柄

代码实例：
@todo

## func (c *UDPConn) LocalAddr() Addr

返回值：
- Addr 本地地址

功能说明：

获取UDP句柄的本地地址

代码实例：
@todo

## func (c *UDPConn) Read(b []byte) (int, error)

## func (c *UDPConn) ReadFrom(b []byte) (int, Addr, error)

## func (c *UDPConn) ReadFromUDP(b []byte) (n int, addr *UDPAddr, err error)

参数列表

- b buffer缓冲区

返回值：
- n 读入字节数
- addr 远程地址
- err 错误(如果有)

功能说明：

从UDP句柄中取出数据并填充到预分配buffer中

代码实例：

    package main
    
    import (
    	"fmt"
    	"net"
    )
    
    func main() {
    	addr, err := net.ResolveUDPAddr("udp", ":53")
    	if err != nil {
    		fmt.Println(err)
    		return
    	}
    	listen, err := net.ListenUDP("udp", addr)
    	if err != nil {
    		fmt.Println(err)
    		return
    	}
    	defer listen.Close()
    	for {
    		//max udp size = MTU(default) - IP Header - UDP Header = 1500 - 20 - 8
    		data := make([]byte, 1472)
    
    		length, remoteAddr, err := listen.ReadFromUDP(data)
    		if err != nil {
    			fmt.Println(err)
    			continue
    		}
    		fmt.Println("data length : ", length, "remote : ", remoteAddr)
    	}
    }


## func (c *UDPConn) ReadMsgUDP(b, oob []byte) (n, oobn, flags int, addr *UDPAddr, err error)

## func (c *UDPConn) RemoteAddr() Addr

## func (c *UDPConn) SetDeadline(t time.Time) error

## func (c *UDPConn) SetReadBuffer(bytes int) error

## func (c *UDPConn) SetReadDeadline(t time.Time) error

## func (c *UDPConn) SetWriteBuffer(bytes int) error

## func (c *UDPConn) SetWriteDeadline(t time.Time) error

## func (c *UDPConn) Write(b []byte) (int, error)

## func (c *UDPConn) WriteMsgUDP(b, oob []byte, addr *UDPAddr) (n, oobn int, err error)

## func (c *UDPConn) WriteTo(b []byte, addr Addr) (int, error)

## func (c *UDPConn) WriteToUDP(b []byte, addr *UDPAddr) (int, error)

