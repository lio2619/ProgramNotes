## asmx to wsdl

* 記得要先啟動該asmx
* 通常disco的路徑為：C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.8 Tools
```bash
disco /out:C:\Users\user\Downloads\MRAC_wsdl http://localhost:4280/TransactionListReal.asmx
```

## wsdl to reference.cs

* 通常wsdl的路徑為：C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.8 Tools
```bash
wsdl.exe C:\Users\user\Downloads\MRAC_wsdl\AP2AP\new\PushTransaction.wsdl /out:C:\Users\user\Downloads\MRAC_wsdl\AP2AP\new\Reference.cs
```