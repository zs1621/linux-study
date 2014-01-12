
##**netstat**

 - `-l`: 只显示监听的端口
 - `-p`: 显示使用这个端口的程序PID
 - `-n`: 本地端口显示ip

>
###netstat -lpn 
<table class="table table-bordered table-striped table condensed">
   <tr>
       <th>Proto</th>
       <th>Recv-Q</th>
       <th>Send-Q</th>
       <th>Local-Addess</th> 
       <th>Foreign-Address</th>
       <th>State</th>
       <th>PID/Programe-name</th>
   </tr>
   <tr>
       <td>TCP</td>
       <td>0</td>
       <td>0</td>
       <td>127.0.0.1:53</td>  
       <td>0.0.0.0:*</td>
       <td>Listen</td> 
       <td>3975/dnsmasq</td>
   </tr>
</table>  

看上面的例子

 - **Proto**: 协议名称
 - **Recv-Q** 和 **Send-Q**: 接收队列和发送队列，一般情况为0， 如果不是表示软件包正在队列中堆积 
 - **Local-Address**: 本地端socket的地址和端口
 - **Foreign-Address**: 对应本地端的另一端的socket 的地址和端口
 - **State**: 状态，本文中的例子显示的监听状态的端口
 - **PID**: 表示实用此端口的程序的id

