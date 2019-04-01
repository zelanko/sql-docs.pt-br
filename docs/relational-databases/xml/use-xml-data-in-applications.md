---
title: Usar dados XML em aplicativos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- parameters [XML in SQL Server]
- XML [SQL Server], ADO
- columns [XML in SQL Server], ADO.NET
- ADO [XML in SQL Server]
- columns [XML in SQL Server], SQL Server Native Client
- xml data type [SQL Server], ADO
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- ADO.NET [XML in SQL Server]
- XML [SQL Server], ADO.NET
- columns [XML in SQL Server], ADO
- xml data type [SQL Server], ADO.NET
- XML [SQL Server], SQL Server Native Client
ms.assetid: 5dabf7e0-c6df-451d-a070-4661f84607fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e309fa06adddfa54775085d9ec8955d604a381fc
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510068"
---
# <a name="use-xml-data-in-applications"></a>Usar dados XML em aplicativos
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve as opções disponíveis para trabalhar com o tipo de dados **xml** em seu aplicativo. O tópico contém informações sobre o seguinte:  
  
-   Tratando XML de uma coluna de tipo **xml** usando o ADO e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   Tratando XML de uma coluna de tipo **xml** usando o ADO.NET  
  
-   Tratando tipo **xml** em parâmetros usando o ADO.NET  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-ado-and-sql-server-native-client"></a>Tratando XML de uma coluna de tipo xml usando o ADO e o SQL Server Native Client  
 Para usar componentes MDAC para acessar os tipos e recursos introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], a propriedade de inicialização DataTypeCompatibility deve estar definida na cadeia de conexão do ADO.  
  
 Por exemplo, o exemplo a seguir do Visual Basic Scripting Edition (VBScript) mostra os resultados de uma consulta em uma coluna de tipo de dados **xml** , `Demographics`, na tabela `Sales.Store` do banco de dados `AdventureWorks2012` de exemplo. Especificamente, a consulta procura o valor da instância dessa coluna para a linha em que o `CustomerID` é igual a `3`.  
  
```  
Const DS = "MyServer"  
Const DB = "AdventureWorks2012"  
  
Set objConn = CreateObject("ADODB.Connection")  
Set objRs = CreateObject("ADODB.Recordset")  
  
CommandText = "SELECT Demographics" & _  
              " FROM Sales.Store" & _  
              " INNER JOIN Sales.Customer" & _  
              " ON Sales.Store.BusinessEntityID = sales.customer.StoreID" & _  
              " WHERE Sales.Customer.CustomerID = 3" & _  
              " OR Sales.Customer.CustomerID = 4"  
  
ConnectionString = "Provider=SQLNCLI11" & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;" & _  
                   "DataTypeCompatibility=80"  
  
'Connect to the data source.  
objConn.Open ConnectionString  
  
'Execute command through the connection and display  
Set objRs = objConn.Execute(CommandText)  
  
Dim rowcount  
rowcount = 0  
Do While Not objRs.EOF  
   rowcount = rowcount + 1  
   MsgBox "Row " & rowcount & _  
           vbCrLf & vbCrLf & objRs(0)  
   objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
```  
  
 Esse exemplo mostra como definir a propriedade de compatibilidade de tipo de dados. Por padrão, isso é definido como 0 ao usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Se você definir o valor como 80, o provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client fará com que as colunas de tipo **xml** e definidas pelo usuário sejam exibidas como tipos de dados do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] . Esses tipos são DBTYPE_WSTR e DBTYPE_BYTES, respectivamente.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Native Client também deve estar instalado no computador cliente e a cadeia de conexão deve especificá-lo para uso como o provedor de dados com "`Provider=SQLNCLI11;...`".  
  
#### <a name="to-test-this-example"></a>Para testar este exemplo  
  
1.  Verifique se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client está instalado e se o MDAC 2.6.0 ou posterior está disponível no computador cliente.  
  
     Para obter mais informações, veja [Programação do SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client-programming.md).  
  
2.  Verifique se o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] de exemplo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado.  
  
     Esse exemplo requer o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] de exemplo.  
  
3.  Copie o código mostrado anteriormente neste tópico e cole-o em seu editor de texto ou de código. Salve o arquivo como HandlingXmlDataType.vbs.  
  
4.  Modifique o script conforme necessário para sua instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e salve as alterações.  
  
     Por exemplo, quando `MyServer` estiver especificado, ele deve ser substituído pelo nome `(local)` ou real do servidor no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado.  
  
5.  Execute HandlingXmlDataType.vbs e execute o script.  
  
 Os resultados devem ser semelhantes à seguinte saída de exemplo:  
  
```  
Row 1  
  
<StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>1500000</AnnualSales>  
  <AnnualRevenue>150000</AnnualRevenue>  
  <BankName>Primary International</BankName>  
  <BusinessType>OS</BusinessType>  
  <YearOpened>1974</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>38000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>40</NumberEmployees>  
</StoreSurvey>  
  
Row 2  
  
<StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>United Security</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1976</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>6000</SquareFeet>  
  <Brands>2</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>5</NumberEmployees>  
</StoreSurvey>  
```  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-adonet"></a>Tratando XML de uma coluna de tipo xml usando o ADO.NET  
 Para tratar XML de uma coluna de tipo de dados **xml** usando o ADO.NET e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , você pode usar o comportamento padrão da classe **SqlCommand** . Por exemplo, uma coluna de tipo de dados **xml** e seus valores podem ser recuperados da mesma maneira como qualquer coluna SQL é recuperada usando um **SqlDataReader**. No entanto, se você desejar trabalhar com o conteúdo de uma coluna de tipo de dados **xml** como XML, primeiro precisará atribuir o conteúdo a um tipo **XmlReader** .  
  
 Para obter mais informações e um código de exemplo, confira “Valores de coluna XML em um Leitor de Dados” na documentação do SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] .  
  
## <a name="handling-an-xml-type-column-in-parameters-by-using-adonet"></a>Tratando uma coluna de tipo xml em parâmetros usando o ADO.NET  
 Para tratar um tipo de dados xml passado como um parâmetro no ADO.NET e no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], é possível fornecer o valor como uma instância do tipo de dados **SqlXml** . Nenhum tratamento especial está envolvido porque as colunas de tipo de dados **xml** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem aceitar valores de parâmetros da mesma maneira que outras colunas e tipos de dados, como **string** ou **integer**.  
  
 Para obter mais informações e um código de exemplo, confira “Valores XML como parâmetros de comando” na documentação do SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
