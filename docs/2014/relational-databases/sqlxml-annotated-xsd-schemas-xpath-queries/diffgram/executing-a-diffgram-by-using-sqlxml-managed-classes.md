---
title: Executando um DiffGram usando classes gerenciadas SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], Managed Classes
- SQLXML Managed Classes, DiffGrams
- Managed Classes [SQLXML], DiffGrams
- SQLXML, Managed Classes
ms.assetid: 81c687ca-8c9f-4f58-801f-8dabcc508a06
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d8756bb3dc7b030541159c2aa127162907aa4b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013046"
---
# <a name="executing-a-diffgram-by-using-sqlxml-managed-classes"></a>Executando um DiffGram usando as classes gerenciadas SQLXML
  Este exemplo mostra como executar um arquivo DiffGram no ambiente de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework para aplicar atualizações de dados a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabelas usando classes gerenciadas SQLXML (Microsoft. Data. SQLXML).  
  
 Neste exemplo, o DiffGram atualiza as informações do cliente (CompanyName e ContactName) de ALFKI do cliente.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 O ** \<bloco before>** inclui um ** \<elemento Customer>** (**diffgr: ID = "Customer1"**). O bloco de ** \<>de DataInstance** inclui o elemento de ** \<>do cliente** correspondente com a mesma **ID**. O ** \<elemento>do cliente** na ** \<>de NewDataSet** também especifica **diffgr: hasChanges = "Modified"**. Isso indica uma operação de atualização e o registro de cliente na tabela Cust é atualizado adequadamente. Observe que, se o atributo **diffgr: hasChanges** não for especificado, a lógica de processamento de DiffGram ignorará esse elemento e nenhuma atualização será executada.  
  
 Este é o código para um aplicativo de tutorial em C# que mostra como usar as classes gerenciadas SQLXML para executar o DiffGram acima e atualizar duas tabelas (Cust, Ord) que você também criará no banco de dados **tempdb** .  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=MyServer;database=tempdb;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      SqlXmlAdapter ad;  
      // Need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandStream = new FileStream("MyDiffgram.xml", FileMode.Open, FileAccess.Read);  
      cmd.CommandType = SqlXmlCommandType.DiffGram;  
      cmd.SchemaPath = "DiffGramSchema.xml";  
      // Load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Verifique se o .NET Framework está instalado em seu computador.  
  
2.  Salve o seguinte esquema XSD (DiffGramSchema.xml) em uma pasta:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
     </xsd:annotation>  
     <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
     </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Crie essas tabelas no banco de dados **tempdb** .  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
4.  Adicione estes dados de exemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
5.  Copie o DiffGram acima e cole em um arquivo de texto. Salve o arquivo como MyDiffGram.xml na mesma pasta usada na etapa 1.  
  
6.  Salve o código C# (DiffgramSample.cs) fornecido acima na mesma pasta em que foram armazenados DiffGramSchema.xml e MyDiffGram.xml nas etapas anteriores.  
  
    > [!NOTE]  
    >  Será necessário atualizar o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão, de '`MyServer`' para o nome real da sua instância instalada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
     Se você armazenar os arquivos em uma pasta diferente, será necessário editar o código e especificar o caminho do diretório apropriado para o esquema de mapeamento.  
  
7.  Compile o código. Para compilar o código no prompt de comando, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DiffgramSample.cs  
    ```  
  
     Isso cria um executável (DiffgramSample.exe).  
  
8.  No prompt de comando, execute DiffgramSample.exe.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplos de DiffGram &#40;SQLXML 4,0&#41;](diffgram-examples-sqlxml-4-0.md)  
  
  
