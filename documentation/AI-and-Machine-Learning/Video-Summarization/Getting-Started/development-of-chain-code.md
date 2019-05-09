# 开发链码
链码可看作是超级账本中的智能合约，通常用来处理网络成员达成共识的业务逻辑，任何对账本数据的查询和修改都需要调用链码实现。超级账本链码本质上是实现接口规约的程序，当前开发语言支持Go语言。

## 开发环境
采用Go语言开发链码，需要准备如下开发环境：
1.	安装配置Go，建议采用1.10.X以上版本；
2.	GitHub上获取Hyper ledge Fabric 1.0.0源码并添加到GOPATH；
3.	安装配置IDE，建议使用GoLand。

## 链码API
所有链码都需要实现Chaincode接口，接口声明如下所示。Peer节点在交易中调用链码接口方法，其中Init方法在链码实例化（instantiate）和升级（upgrade）交易中调用，以便链码执行必要的初始化操作。Invoke方法在调用（invoke）交易中使用，处理交易提案内容，修改或读取账本数据。
  
 ```
// Chaincode interface must be implemented by all chaincodes. The fabric runs
   // the transactions by calling these functions as specified.
type Chaincode interface {
   // Init is called during Instantiate transaction after the chaincode container
   // has been established for the first time, allowing the chaincode to
   // initialize its internal data
   Init(stub ChaincodeStubInterface) pb.Response
   // Invoke is called to update or query the ledger in a proposal transaction.
   // Updated state variables are not committed to the ledger until the
   // transaction is committed.
   Invoke(stub ChaincodeStubInterface) pb.Response
}
```

表-Chain code接口声明表

链码API中另一个重要接口是Chaincode StubInterface，链码与超级账本的交互都通过该接口实现，如获取调用参数、获取操作用户信息、获取交易信息、操作账本、调用其他链码等。

链码需要包含main方法，并在main方法中调用shim. Start函数启动链码，链码启动中建立与Peer节点的通信连接，实现与Peer的交互。

## 链码实例

```
func (t *SimpleChaincode) Init(stub shim.ChaincodeStubInterface) pb.Response {
   var err error
   _, args := stub.GetFunctionAndParameters()
   if len(args) != 1 {
      return shim.Error("Incorrect number of arguments. Expecting 2")
   }
   if _, err = strconv.Atoi(args[0]);  err != nil {
      return shim.Error("Expecting integer value for asset holding")
   }
   if err := stub.PutState(Name, []byte(args[0])); err != nil {
      return shim.Error(fmt.Sprintf("fail to put state: %v", err))
   }
   return shim.Success(nil)
}
```

```
func (t *SimpleChaincode) Invoke(stub shim.ChaincodeStubInterface) pb.Response {
   function, args := stub.GetFunctionAndParameters()
   switch function {
   case "invoke":
      return t.invoke(stub, args)
   case "query":
      return t.query(stub, args)
   default:
      return shim.Error("not support function")
   }
}
func (t *SimpleChaincode) invoke(stub shim.ChaincodeStubInterface, args []string) pb.Response {
   if len(args) != 1 {
      return shim.Error("Incorrect number of arguments. Expecting 1")
   }
   change, err :=  strconv.Atoi(args[0])
   if err != nil {
      return shim.Error("Expecting integer value for asset holding")
   }
   if state, err := stub.GetState(Name); err != nil {
      return shim.Error("fail to read asset state")
   }  else if value, err := strconv.Atoi(string(state)); err != nil {
      return shim.Error("fail to parse asset holding")
   } else if err := stub.PutState(Name,[]byte(strconv.Itoa(value + change))); err != nil{
      return shim.Error("fail to change asset holding")
   } else {
      return shim.Success(nil)
   }
}
```

```
func (t *SimpleChaincode) query(stub shim.ChaincodeStubInterface, args []string) pb.Response {
   if state, err := stub.GetState(Name); err != nil {
      return shim.Error("fail to read asset state")
   }  else if _, err := strconv.Atoi(string(state)); err != nil {
      return shim.Error("fail to parse asset holding")
   } else {
      return shim.Success(state)
   }
}
```

```
func main() {
   err := shim.Start(new(SimpleChaincode))
   if err != nil {
      fmt.Printf("Error starting Simple chaincode: %v\n", err)
   }
}
```
