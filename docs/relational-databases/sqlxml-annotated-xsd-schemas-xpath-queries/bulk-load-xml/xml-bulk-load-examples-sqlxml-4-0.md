---
title: Exemplos de carregamento em massa XML (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- ConnectionCommand property
- XMLFragment property
- relationship chains [SQLXML]
- multiple table bulk loading
- examples [SQLXML], XML Bulk Load
- overflow data [SQLXML]
- sql:datatype
- transaction mode [SQLXML]
- CheckConstraints property
- sql:overflow-field
- XML Bulk Load [SQLXML], examples
- TempFilePath property
- datatype annotation
- Transaction property
- KeepIdentity property
- Execute method
- streaming XML data
- xml data type [SQL Server], SQLXML
- bulk load [SQLXML], examples
ms.assetid: 970e4553-b41d-4a12-ad50-0ee65d1f305d
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4527b1c3fb4e3573bad5b34a3c4743da16d94487
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32973421"
---
# <a name="xml-bulk-load-examples-sqlxml-40"></a>Exemplos do XML Bulk Load (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Os exemplos a seguir ilustram a funcionalidade do XML Bulk Load no Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cada exemplo fornece um esquema XSD e seu esquema XDR equivalente.  
  
## <a name="bulk-loader-script-validateandbulkloadvbs"></a>Script de Carregador em Massa (ValidateAndBulkload.vbs)  
 O script a seguir, escrito no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript), carrega um documento XML no DOM XML; valida em relação um esquema; e, se o documento for válido, executa um XML bulk load para carregar o XML em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabela. Esse script pode ser usado com cada um dos exemplos individuais que farão referência a ele posteriormente neste tópico.  
  
> [!NOTE]  
>  O XML Bulk Load não lançará um aviso ou um erro se nenhum conteúdo for carregado do arquivo de dados. Portanto, é uma prática recomendada validar seu arquivo de dados XML antes de executar uma operação de carregamento em massa.  
  
```vbs  
Dim FileValid  
  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
'Validate the data file prior to bulkload  
Dim sOutput   
sOutput = ValidateFile("SampleXMLData.xml", "", "SampleSchema.xml")  
WScript.Echo sOutput  
  
If FileValid Then  
   ' Check constraints and initiate transaction (if needed)  
   ' objBL.CheckConstraints = True  
   ' objBL.Transaction=True  
  'Execute XML bulkload using file.  
  objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
  set objBL=Nothing  
End If  
  
Function ValidateFile(strXmlFile,strUrn,strXsdFile)  
  
   ' Create a schema cache and add SampleSchema.xml to it.  
   Dim xs, fso, sAppPath  
   Set fso = CreateObject("Scripting.FileSystemObject")   
   Set xs = CreateObject("MSXML2.XMLSchemaCache.6.0")  
   sAppPath = fso.GetFolder(".")   
   xs.Add strUrn, sAppPath & "\" & strXsdFile  
  
   ' Create an XML DOMDocument object.  
   Dim xd   
   Set xd = CreateObject("MSXML2.DOMDocument.6.0")  
  
   ' Assign the schema cache to the DOM document.  
   ' schemas collection.  
   Set xd.schemas = xs  
  
   ' Load XML document as DOM document.  
   xd.async = False  
   xd.Load sAppPath & "\" & strXmlFile  
  
   ' Return validation results in message to the user.  
   If xd.parseError.errorCode <> 0 Then  
        ValidateFile = "Validation failed on " & _  
             strXmlFile & vbCrLf & _  
             "=======" & vbCrLf & _  
             "Reason: " & xd.parseError.reason & _  
             vbCrLf & "Source: " & _  
             xd.parseError.srcText & _  
             vbCrLf & "Line: " & _  
             xd.parseError.Line & vbCrLf  
             FileValid = False  
    Else  
        ValidateFile = "Validation succeeded for " & _  
             strXmlFile & vbCrLf & _  
             "========" & _  
             vbCrLf & "Contents to be bulkloaded" & vbCrLf  
             FileValid = True  
    End If  
End Function  
```  
  
## <a name="a-bulk-loading-xml-in-a-table"></a>A. Carregando o XML em massa em uma tabela  
 Este exemplo estabelece uma conexão com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que é especificado na propriedade ConnectionString (MyServer). O exemplo também especifica a propriedade ErrorLogFile. Portanto, a saída de erro é salva no arquivo especificado ("C:\error.log") que você também poderá decidir alterar para um local diferente. Observe também que o método Execute tem como seus parâmetros o arquivo de esquema de mapeamento (SampleSchema.xml) e o arquivo de dados XML (SampleXMLData.xml). Quando executa o carregamento em massa, a tabela Cust que você criou no **tempdb** banco de dados conterá novos registros com base no conteúdo do arquivo de dados XML.  
  
#### <a name="to-test-a-sample-bulk-load"></a>Para testar um exemplo de carregamento em massa  
  
1.  Crie esta tabela:  
  
    ```sql  
    CREATE TABLE Cust(CustomerID  int PRIMARY KEY,  
                      CompanyName varchar(20),  
                      City        varchar(20));  
    GO  
    ```  
  
2.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleSchema.xml. Para este arquivo, adicione o seguinte esquema XSD:  
  
    ```xml  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
       <xsd:element name="ROOT" sql:is-constant="1" >  
         <xsd:complexType>  
           <xsd:sequence>  
             <xsd:element name="Customers" sql:relation="Cust" maxOccurs="unbounded">  
               <xsd:complexType>  
                 <xsd:sequence>  
                   <xsd:element name="CustomerID"  type="xsd:integer" />  
                   <xsd:element name="CompanyName" type="xsd:string" />  
                   <xsd:element name="City"        type="xsd:string" />  
                 </xsd:sequence>  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
          </xsd:complexType>  
         </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleXMLD.xml. Para esse arquivo, adicione o seguinte documento XML:  
  
    ```xml  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Sean Chai</CompanyName>  
        <City>New York</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Tom Johnston</CompanyName>  
         <City>Los Angeles</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Institute of Art</CompanyName>  
        <City>Chicago</City>  
      </Customers>  
    </ROOT>  
    ```  
  
4.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como ValidateAndBulkload.vbs. Para esse arquivo, adicione o código VBScript que foi fornecido anteriormente, no início deste tópico. Modifique a cadeia de conexão para fornecer o nome do servidor apropriado. Especifique o caminho apropriado para os arquivos que são especificados como parâmetros para o método Execute.  
  
5.  Execute o código VBScript. O XML Bulk Load carrega o XML para a tabela Cust.  
  
 Este é o esquema XDR equivalente:  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers"  sql:relation="Cust" >  
      <element type="CustomerID"  sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City"        sql:field="City" />  
  
   </ElementType>  
</Schema>  
```  
  
## <a name="b-bulk-loading-xml-data-in-multiple-tables"></a>B. Carregando dados XML em massa em várias tabelas  
 Neste exemplo, o documento XML consiste de  **\<cliente >** e  **\<ordem >** elementos.  
  
```xml  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Sean Chai</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Tom Johnston</CompanyName>  
     <City>LA</City>    
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Institute of Art</CompanyName>  
    <Order OrderID="4" />  
  </Customers>  
</ROOT>  
```  
  
 Bulk Este exemplo carrega os dados XML em duas tabelas, **Cust** e **CustOrder**:  
  
-   Cust (CustomerID, CompanyName, cidade)  
  
-   CustOrder (OrderID, CustomerID)  
  
 O seguinte esquema XSD define a exibição XML dessas tabelas. O esquema Especifica a relação pai-filho entre o  **\<cliente >** e  **\<ordem >** elementos.  
  
```xml  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Customers" sql:relation="Cust" >  
          <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="CustomerID"  type="xsd:integer" />  
              <xsd:element name="CompanyName" type="xsd:string" />  
              <xsd:element name="City"        type="xsd:string" />  
              <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
                <xsd:complexType>  
                  <xsd:attribute name="OrderID" type="xsd:integer" />  
                </xsd:complexType>  
              </xsd:element>  
             </xsd:sequence>  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 XML Bulk Load usa a relação chave primária/estrangeira chave especificada anteriormente entre o  **\<Cust >** e  **\<CustOrder >** elementos em massa carregar os dados em ambas as tabelas .  
  
#### <a name="to-test-a-sample-bulk-load"></a>Para testar um exemplo de carregamento em massa  
  
1.  Crie duas tabelas no **tempdb** banco de dados:  
  
    ```sql  
    USE tempdb;  
    CREATE TABLE Cust(  
           CustomerID  int PRIMARY KEY,  
           CompanyName varchar(20),  
           City        varchar(20));  
    CREATE TABLE CustOrder(        OrderID     int PRIMARY KEY,   
            CustomerID int FOREIGN KEY REFERENCES Cust(CustomerID));  
    ```  
  
2.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleSchema.xml. Adicione ao arquivo o esquema XSD que é fornecido neste exemplo.  
  
3.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleData.xml. Adicione ao arquivo o documento XML que foi fornecido anteriormente neste exemplo.  
  
4.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como ValidateAndBulkload.vbs. Para esse arquivo, adicione o código VBScript que foi fornecido anteriormente, no início deste tópico. Modifique a cadeia de conexão para fornecer o nome apropriado de servidor e de banco de dados. Especifique o caminho apropriado para os arquivos que são especificados como parâmetros para o método Execute.  
  
5.  Execute o código VBScript anterior. O XML Bulk Load carrega o documento XML para as tabelas Cust e CustOrder.  
  
 Este é o esquema XDR equivalente:  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
<sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="c-using-chain-relationships-in-the-schema-to-bulk-load-xml"></a>C. Usando relações de cadeia no esquema para carregamento em massa do XML  
 Este exemplo ilustra como a relação M:N especificada no esquema de mapeamento é usada pelo XML Bulk Load para carregar dados em uma tabela que representa uma relação M:N.  
  
 Por exemplo, considere este esquema XSD:  
  
```xml  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Ord"  
          parent-key="OrderID"  
          child="OrderDetail"  
          child-key="OrderID" />  
  
    <sql:relationship name="ODProduct"  
          parent="OrderDetail"  
          parent-key="ProductID"  
          child="Product"  
          child-key="ProductID"   
          inverse="true"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Ord"   
                     sql:key-fields="OrderID" >  
          <xsd:complexType>  
            <xsd:sequence>  
             <xsd:element name="Product"  
                          sql:relation="Product"   
                          sql:key-fields="ProductID"  
                          sql:relationship="OrderOD ODProduct">  
               <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
           <xsd:attribute name="OrderID"   type="xsd:integer" />   
           <xsd:attribute name="CustomerID"   type="xsd:string" />  
         </xsd:complexType>  
       </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 O esquema especifica um  **\<ordem >** elemento com um  **\<produto >** elemento filho. O  **\<ordem >** elemento é mapeado para a tabela Ord e o  **\<produto >** elemento é mapeado para a tabela de produtos no banco de dados. A relação de cadeia especificada no  **\<produto >** elemento identifica uma relação de M:N representada pela tabela OrderDetail. (Uma ordem pode incluir vários produtos, e um produto pode ser incluído em muitos pedidos.)  
  
 Quando você está carregando em massa um documento XML com esse esquema, os registros são adicionados às tabelas Ord, Product e OrderDetail.  
  
#### <a name="to-test-a-working-sample"></a>Para testar um exemplo de funcionamento  
  
1.  Crie três tabelas:  
  
    ```sql  
    CREATE TABLE Ord (  
             OrderID     int  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  Salve o esquema fornecido anteriormente neste exemplo como SampleSchema.xml.  
  
3.  Salve os dados XML de exemplo a seguir como SampleXMLData.xml:  
  
    ```xml  
    <ROOT>    
      <Order OrderID="1" CustomerID="ALFKI">  
        <Product ProductID="1" ProductName="Chai" />  
        <Product ProductID="2" ProductName="Chang" />  
      </Order>  
      <Order OrderID="2" CustomerID="ANATR">  
        <Product ProductID="3" ProductName="Aniseed Syrup" />  
        <Product ProductID="4" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como ValidateAndBulkload.vbs. Para esse arquivo, adicione o código VBScript que foi fornecido anteriormente, no início deste tópico. Modifique a cadeia de conexão para fornecer o nome apropriado de servidor e de banco de dados. Remova os comentários das linhas a seguir do código fonte para obter este exemplo.  
  
    ```vbs  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    ```  
  
5.  Execute o código VBScript. O XML Bulk Load carrega o documento XML para as tabelas Ord e Product.  
  
## <a name="d-bulk-loading-in-identity-type-columns"></a>D. Carregamento em massa em colunas de tipo de identidade  
 Este exemplo ilustra como o carregamento em massa trata colunas de tipo de identidade. No exemplo, os dados são carregados em massa para três tabelas (Ord, Product e OrderDetail).  
  
 Nestas tabelas:  
  
-   OrderID na tabela Ord é uma coluna de tipo de identidade  
  
-   ProductID na tabela Product é uma coluna de tipo de identidade.  
  
-   As colunas OrderID e ProductID na tabela OrderDetail são colunas de chave estrangeira que se referem a colunas de chave primária nas tabelas Ord e Product.  
  
 A seguir, são descritos os esquemas de tabela para este exemplo:  
  
```  
Ord (OrderID, CustomerID)  
Product (ProductID, ProductName)  
OrderDetail (OrderID, ProductID)  
```  
  
 Neste exemplo de XML Bulk Load, a propriedade KeepIdentity o carregamento em massa do modelo de objeto é definida como false. Portanto, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gera valores de identidade para as colunas ProductID e OrderID nas tabelas Product e Ord, respectivamente (todos os valores fornecidos nos documentos a serem carregados em massa são ignorados).  
  
 Neste caso, o XML Bulk Load identifica a relação de chave primária/chave estrangeira entre as tabelas. O Bulk Load primeiro insere registros nas tabelas com a chave primária e, em seguida, propaga o valor de identidade gerado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para as tabelas com colunas de chave estrangeira. No exemplo a seguir, o XML Bulk Load insere dados nas tabelas nesta ordem:  
  
1.  Product  
  
2.  Ord  
  
3.  OrderDetail  
  
    > [!NOTE]  
    >  Para propagar os valores de identidade gerados nas tabelas Products e Orders, a lógica de processamento exige que o XML Bulk Load acompanhe a inserção mais recente desses valores na tabela OrderDetails. Para fazer isso, o XML Bulk Load cria tabelas intermediárias, popula os dados nessas tabelas e depois os remove.  
  
#### <a name="to-test-a-working-sample"></a>Para testar um exemplo de funcionamento  
  
1.  Crie estas tabelas:  
  
    ```  
    CREATE TABLE Ord (  
             OrderID     int identity(1,1)  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int identity(1,1) PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleSchema.xml. Adicione este esquema XSD a este arquivo.  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
       <xsd:appinfo>  
        <sql:relationship name="OrderOD"  
              parent="Ord"  
              parent-key="OrderID"  
              child="OrderDetail"  
              child-key="OrderID" />  
        <sql:relationship name="ODProduct"  
              parent="OrderDetail"  
              parent-key="ProductID"  
              child="Product"  
              child-key="ProductID"   
              inverse="true"/>  
       </xsd:appinfo>  
     </xsd:annotation>  
  
      <xsd:element name="Order" sql:relation="Ord"   
                                sql:key-fields="OrderID" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="Product" sql:relation="Product"   
                         sql:key-fields="ProductID"  
                         sql:relationship="OrderOD ODProduct">  
              <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
              </xsd:complexType>  
            </xsd:element>  
         </xsd:sequence>  
            <xsd:attribute name="OrderID"   type="xsd:integer" />   
            <xsd:attribute name="CustomerID"   type="xsd:string" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleXMLD.xml. Adicione o documento XML a seguir.  
  
    ```  
    <ROOT>    
      <Order OrderID="11" CustomerID="ALFKI">  
        <Product ProductID="11" ProductName="Chai" />  
        <Product ProductID="22" ProductName="Chang" />  
      </Order>  
      <Order OrderID="22" CustomerID="ANATR">  
         <Product ProductID="33" ProductName="Aniseed Syrup" />  
        <Product ProductID="44" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como ValidateAndBulkload.vbs. Para este arquivo, adicione o código VBScript a seguir. Modifique a cadeia de conexão para fornecer o nome apropriado de servidor e de banco de dados. Especifique o caminho apropriado para os arquivos que servem como parâmetros para o **Execute** método.  
  
    ```  
    Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "C:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction = False  
    objBL.KeepIdentity = False  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    Set objBL = Nothing  
    MsgBox "Done."  
    ```  
  
5.  Execute o código VBScript. O XML Bulk Load carregará os dados nas tabelas apropriadas.  
  
## <a name="e-generating-table-schemas-before-bulk-loading"></a>E. Gerando esquemas de tabela antes do carregamento em massa  
 O XML Bulk Load poderá opcionalmente gerar as tabelas se elas não existirem antes do carregamento em massa. Definindo a propriedade SchemaGen do objeto SQLXMLBulkLoad como TRUE faz isso. Você também pode solicitar o XML Bulk Load descarte todas as tabelas existentes e recriá-los, definindo a propriedade SGDropTables como TRUE. O exemplo de VBScript a seguir ilustra o uso dessas propriedades.  
  
 Além disso, este exemplo define duas propriedades adicionais como TRUE:  
  
-   CheckConstraints. A definição desta propriedade como TRUE assegura que os dados que estão sendo inseridos nas tabelas não violem nenhuma restrição especificada (neste caso, as restrições PRIMARY KEY/FOREIGN KEY especificadas entre as tabelas Cust e CustOrder. Se houver uma violação de restrição, o carregamento em massa falhará.  
  
-   XMLFragment. Esta propriedade deve ser definida como TRUE porque o exemplo de documento XML (fonte de dados) não contém nenhum elemento de alto nível único (e é, assim, um fragmento).  
  
 Este é o código VBScript:  
  
```  
Dim objBL   
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
objBL.CheckConstraints=true  
objBL.XMLFragment = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
```  
  
#### <a name="to-test-a-working-sample"></a>Para testar um exemplo de funcionamento  
  
1.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleSchema.xml. Adicione ao arquivo o esquema XSD fornecido no exemplo anterior, "Usando relações de cadeia no esquema para carregamento em massa do XML".  
  
2.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleXMLD.xml. Adicione ao arquivo o documento XML fornecido no exemplo anterior, "Usando relações de cadeia no esquema para carregamento em massa do XML". Remover o \<raiz > elemento do documento (para torná-lo um fragmento).  
  
3.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como ValidateAndBulkload.vbs. Para este arquivo, adicione o código VBScript neste exemplo. Modifique a cadeia de conexão para fornecer o nome apropriado de servidor e de banco de dados. Especifique o caminho apropriado para os arquivos que são especificados como parâmetros para o método Execute.  
  
4.  Execute o código VBScript. O XML Bulk Load cria as tabelas necessárias na base do esquema de mapeamento fornecido e carrega em massa os dados nele.  
  
## <a name="f-bulk-loading-from-a-stream"></a>F. Carregando em massa de um fluxo  
 O método de execução do modelo de objeto XML Bulk Load usa dois parâmetros. O primeiro parâmetro é o arquivo de esquema de mapeamento. O segundo parâmetro fornece os dados XML que devem ser carregados no banco de dados. Há duas maneiras de passar os dados XML para o método de execução de carregamento em massa de XML:  
  
-   Especifique o nome do arquivo como o parâmetro.  
  
-   Transmita um fluxo que contenha os dados XML.  
  
 Este exemplo ilustra como carregar em massa de um fluxo.  
  
 O VBScript primeiro executa uma instrução SELECT para recuperar informações de cliente da tabela Customers no banco de dados Northwind. Como a cláusula FOR XML é especificada (com a opção ELEMENTS) na instrução SELECT, a consulta retorna um documento XML centralizado no elemento desta forma:  
  
```  
<Customer>  
  <CustomerID>..</CustomerID>  
  <CompanyName>..</CompanyName>  
  <City>..</City>  
</Customer>  
...  
```  
  
 O script, em seguida, transmite o XML como um fluxo para o método Execute como seu segundo parâmetro. O volume do método Execute carrega os dados na tabela Cust.  
  
 Como este script define a propriedade SchemaGen como TRUE e a propriedade SGDropTables como TRUE, o XML Bulk Load cria a tabela Cust no banco de dados especificado. (Se a tabela já existir, o XML Bulk Load primeiro descartará a tabela e depois a recriará.)  
  
 Este é exemplo de VBScript:  
  
```  
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
Set objCmd = CreateObject("ADODB.Command")  
Set objConn = CreateObject("ADODB.Connection")  
Set objStrmOut = CreateObject ("ADODB.Stream")  
  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile     = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen        = True  
objBL.SGDropTables     = True  
objBL.XMLFragment      = True  
' Open a connection to the instance of SQL Server to get the source data.  
  
objConn.Open "provider=SQLOLEDB;server=(local);database=tempdb;integrated security=SSPI"  
Set objCmd.ActiveConnection = objConn  
objCmd.CommandText = "SELECT CustomerID, CompanyName, City FROM Customers FOR XML AUTO, ELEMENTS"  
  
' Open the return stream and execute the command.  
Const adCRLF = -1  
Const adExecuteStream = 1024  
objStrmOut.Open  
objStrmOut.LineSeparator = adCRLF  
objCmd.Properties("Output Stream").Value = objStrmOut  
objCmd.Execute , , adExecuteStream  
objStrmOut.Position = 0  
  
' Execute bulk load. Read source XML data from the stream.  
objBL.Execute "SampleSchema.xml", objStrmOut  
  
Set objBL = Nothing  
```  
  
 O seguinte esquema de mapeamento XSD fornece as informações necessárias para criar a tabela:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="ROOT" sql:is-constant="true" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customers"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="Customers" sql:relation="Cust" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element name="CustomerID"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(5)"/>  
      <xsd:element name="CompanyName"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
      <xsd:element name="City"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
 Este é esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
    </ElementType>  
</Schema>  
```  
  
### <a name="opening-a-stream-on-an-existing-file"></a>Abrindo um fluxo em um arquivo existente  
 Você também pode abrir um fluxo em um arquivo de dados XML existente e transmitir o fluxo como um parâmetro para o método Execute (em vez de transmitir o nome de arquivo como o parâmetro).  
  
 Este é um exemplo do Visual Basic de transmitir um fluxo como o parâmetro:  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad  
Dim objStrm As New ADODB.Stream  
Dim objFileSystem As New Scripting.FileSystemObject  
Dim objFile As Scripting.TextStream  
  
MsgBox "Begin BulkLoad..."  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
' Here again a stream is specified that contains the source data   
' (instead of the file name). But this is just an illustration.  
' Usually this is useful if you have an XML data   
' stream that is created by some other means that you want to bulk   
' load. This example starts with an XML text file, so it may not be the   
' best to use a stream (you can specify the file name directly).  
' Here you could have specified the file name itself.   
Set objFile = objFileSystem.OpenTextFile("c:\SampleData.xml")  
objStrm.Open  
objStrm.WriteText objFile.ReadAll  
objStrm.Position = 0  
objBL.Execute "c:\SampleSchema.xml", objStrm  
  
Set objBL = Nothing  
MsgBox "Done."  
End Sub  
```  
  
 Para testar o aplicativo, use o seguinte documento XML em um arquivo (SampleData.xml) e o esquema XSD que é fornecido neste exemplo:  
  
 Estes são os dados de origem de XML (SampleData.xml):  
  
```  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Hanari Carnes</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Toms Spezialitten</CompanyName>  
     <City>LA</City>  
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Victuailles en stock</CompanyName>  
    <Order CustomerID= "4444" OrderID="4" />  
</Customers>  
</ROOT>  
```  
  
 Este é o esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="g-bulk-loading-in-overflow-columns"></a>G. Carregando em massa em colunas de estouro  
 Se o esquema de mapeamento Especifica uma coluna de estouro usando o **SQL: overflow-campo** anotação, carregamento em massa XML copia todos os dados não consumidos do documento de origem para essa coluna.  
  
 Considere este esquema XSD:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Customers" sql:relation="Cust"  
                                sql:overflow-field="OverflowColumn" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
          <xsd:attribute name="CustomerID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 O esquema identifica uma coluna de estouro (OverflowColumn) para a tabela Cust. Como resultado, todos os não consumidos dados XML para cada  **\<cliente >** elemento é adicionado a essa coluna.  
  
> [!NOTE]  
>  Todos os elementos abstratos (elementos para os quais **abstract = "true"** for especificado) e todos os atributos proibidos (atributos para os quais **proibido = "true"** for especificado) serão considerados estouro pelo XML Bulk Carregar e são adicionados para a coluna de estouro, se especificado. (Caso contrário, eles serão ignorados.)  
  
#### <a name="to-test-a-working-sample"></a>Para testar um exemplo de funcionamento  
  
1.  Crie duas tabelas no **tempdb** banco de dados:  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle',  
                  OverflowColumn nvarchar(200));  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID    int PRIMARY KEY,  
                  CustomerID int FOREIGN KEY   
                                 REFERENCES Cust(CustomerID));  
    GO  
    ```  
  
2.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleSchema.xml. Adicione ao arquivo o esquema XSD que é fornecido neste exemplo.  
  
3.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleXMLD.xml. Adicione o seguinte documento XML ao arquivo:  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City><![CDATA[NY]]> </City>  
        <Junk>garbage in overflow</Junk>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <![CDATA[LA]]>   
        <!-- <xyz><address>111 Maple, Seattle</address></xyz>   -->  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como ValidateAndBulkload.vbs. Para esse arquivo, adicione o código do Microsoft Visual Basic Scripting Edition (VBScript) a seguir. Modifique a cadeia de conexão para fornecer o nome apropriado de servidor e de banco de dados. Especifique o caminho apropriado para os arquivos que são especificados como parâmetros para o método Execute.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  Execute o código VBScript.  
  
 Este é o esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"   
                       sql:overflow-field="OverflowColumn"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="h-specifying-the-file-path-for-temp-files-in-transaction-mode"></a>H. Especificando o caminho do arquivo para arquivos temporários em modo de transação  
 Quando você está carregando em massa em modo de transação (isto é, quando a propriedade de transação é definida como TRUE), você também deve definir a propriedade TempFilePath quando qualquer uma das seguintes condições for verdadeira:  
  
-   Você estiver carregando em massa para um servidor remoto.  
  
-   Você desejar usar uma unidade local ou pasta alternativa (uma que não seja o caminho especificado pela variável de ambiente TEMP) para armazenar os arquivos temporários que são criados no modo de transação.  
  
 Por exemplo, o código VBScript a seguir carrega em massa dados do arquivo SampleXMLData.xml para as tabelas de banco de dados no modo de transação. A propriedade TempFilePath é especificada para definir o caminho para os arquivos temporários que são gerados no modo de transação.  
  
```  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.Transaction=True  
objBL.TempFilePath="\\Server\MyDir"  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
set objBL=Nothing  
```  
  
> [!NOTE]  
>  O caminho do arquivo temporário deve ser um local compartilhado que seja acessível à conta de serviço da instância de destino do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e à conta que está executando o aplicativo de carregamento em massa. A menos que você está carregando em massa em um servidor local, o caminho de arquivo temporário deve ser um caminho UNC (como \\\servername\sharename).  
  
#### <a name="to-test-a-working-sample"></a>Para testar um exemplo de funcionamento  
  
1.  Criar essa tabela em **tempdb** banco de dados:  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (     CustomerID uniqueidentifier,   
          LastName  varchar(20));  
    GO  
    ```  
  
2.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleSchema.xml. Adicione o seguinte esquema XSD ao arquivo:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleXMLD.xml. Adicione o seguinte documento XML ao arquivo:  
  
    ```  
    <ROOT>  
    <Customers CustomerID="6F9619FF-8B86-D011-B42D-00C04FC964FF"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
4.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como ValidateAndBulkload.vbs. Para este arquivo, adicione o código VBScript a seguir. Modifique a cadeia de conexão para fornecer o nome apropriado de servidor e de banco de dados. Especifique o caminho apropriado para os arquivos que são especificados como parâmetros para o método Execute. Especifique também o caminho apropriado para a propriedade TempFilePath.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.TempFilePath="\\server\folder"  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  Execute o código VBScript.  
  
     O esquema deve especificar correspondente **SQL: DataType** para o **CustomerID** atributo quando o valor de **CustomerID** é especificado como um GUID que inclui chaves ({ e}), como:  
  
    ```  
    <ROOT>  
    <Customers CustomerID="{6F9619FF-8B86-D011-B42D-00C04FC964FF}"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
     Este é o esquema atualizado:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string"   
                        sql:datatype="uniqueidentifier" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
     Quando **SQL: DataType** é especificado identificando o tipo de coluna como **uniqueidentifier**, a operação de carregamento em massa remove as chaves ({e}) da **CustomerID** valor antes de inseri-lo na coluna.  
  
 Este é o esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
<ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
</ElementType>  
<ElementType name="Customers" sql:relation="Cust" >  
  <AttributeType name="CustomerID"  sql:datatype="uniqueidentifier" />  
  <AttributeType name="LastName"   />  
  
  <attribute type="CustomerID" />  
  <attribute type="LastName"   />  
</ElementType>  
</Schema>  
```  
  
## <a name="i-using-an-existing-database-connection-with-the-connectioncommand-property"></a>I. Usando uma conexão de banco de dados existente com a propriedade ConnectionCommand  
 Você pode usar uma conexão existente do ADO para carregamento em massa do XML. Isto será útil se o XML Bulk Load for apenas uma de muitas operações que serão executados em uma fonte de dados.  
  
 A propriedade ConnectionCommand permite que você use uma conexão ADO existente usando um objeto de comando ADO. Isso é ilustrado no seguinte exemplo do Visual Basic:  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad4  
Dim objCmd As New ADODB.Command  
Dim objConn As New ADODB.Connection  
  
'Open a connection to an instance of SQL Server.  
objConn.Open "provider=SQLOLEDB;data source=(local);database=tempdb;integrated security=SSPI"  
'Ask the Command object to use the connection just established.  
Set objCmd.ActiveConnection = objConn  
  
'Tell Bulk Load to use the active command object that is using the Connection obj.  
objBL.ConnectionCommand = objCmd  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
'The Transaction property must be set to True if you use ConnectionCommand.  
objBL.Transaction = True  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
End Sub  
```  
  
#### <a name="to-test-a-working-sample"></a>Para testar um exemplo de funcionamento  
  
1.  Crie duas tabelas no **tempdb** banco de dados:  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust(  
                   CustomerID   varchar(5) PRIMARY KEY,  
                   CompanyName  varchar(30),  
                   City         varchar(20));  
    GO  
    CREATE TABLE CustOrder(  
                   CustomerID  varchar(5) references Cust (CustomerID),  
                   OrderID     varchar(5) PRIMARY KEY);  
    GO  
    ```  
  
2.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleSchema.xml. Adicione o seguinte esquema XSD ao arquivo:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
    <xsd:annotation>  
      <xsd:appinfo>  
        <sql:relationship name="CustCustOrder"  
              parent="Cust"  
              parent-key="CustomerID"  
              child="CustOrder"  
              child-key="CustomerID" />  
      </xsd:appinfo>  
    </xsd:annotation>  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:sequence>  
           <xsd:element name="CustomerID"  type="xsd:integer" />  
           <xsd:element name="CompanyName" type="xsd:string" />  
           <xsd:element name="City"        type="xsd:string" />  
           <xsd:element name="Order"   
                              sql:relation="CustOrder"  
                              sql:relationship="CustCustOrder" >  
             <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:integer" />  
             </xsd:complexType>  
           </xsd:element>  
         </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleXMLD.xml. Adicione o seguinte documento XML ao arquivo:  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  Crie um aplicativo Visual Basic (EXE Padrão) e o código anterior. Adicione estas referências ao projeto:  
  
    ```  
    Microsoft XML BulkLoad for SQL Server 4.0 Type Library  
    Microsoft ActiveX Data objects 2.6 Library  
    ```  
  
5.  Execute o aplicativo.  
  
 Este é o esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
         <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="j-bulk-loading-in-xml-data-type-columns"></a>J. Carregamento em massa em colunas de tipo de dados xml  
 Se o esquema de mapeamento Especifica uma [tipo de dados xml](../../../t-sql/xml/xml-transact-sql.md) coluna usando o **SQL: DataType = "xml"** anotação, o XML Bulk Load pode copiar os elementos filho XML para o campo mapeado do documento de origem para isso coluna.  
  
 Considere o esquema XSD a seguir, o qual mapeia uma exibição da tabela Production.ProductModel no banco de dados AdventureWorks de exemplo. Nessa tabela, o campo CatalogDescription do **xml** tipo de dados é mapeado para um  **\<Desc >** elemento usando o **SQL: Field** e **sql: tipo de dados = "xml"** anotações.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Name" type="xs:string"></xsd:element>  
        <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element name="ProductDescription">  
              <xsd:complexType>  
                <xsd:sequence>  
                  <xsd:element name="Summary" type="xs:anyType"/>  
                </xsd:sequence>  
              </xsd:complexType>  
            </xsd:element>  
          </xsd:sequence>  
        </xsd:complexType>  
        </xsd:element>   
     </xsd:sequence>  
     <xsd:attribute name="ProductModelID" sql:field="ProductModelID" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
#### <a name="to-test-a-working-sample"></a>Para testar um exemplo de funcionamento  
  
1.  Verifique se o banco de dados AdventureWorks de exemplo está instalado.  
  
2.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleSchema.xml. Copie o esquema XSD anterior, cole-o no arquivo e salve-o.  
  
3.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como SampleXMLD.xml. Copie o documento XML a seguir, cole-o no arquivo e salve-o na mesma pasta que foi usada para a etapa anterior.  
  
    ```  
    <ProductModel ProductModelID="2005">  
        <Name>Mountain-100 (2005 model)</Name>  
        <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
            <p1:ProductDescription xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
                  xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
                  xmlns:wf="http://www.adventure-works.com/schemas/OtherFeatures"   
                  xmlns:html="http://www.w3.org/1999/xhtml"   
                  xmlns="">  
                <p1:Summary>  
                    <html:p>Our top-of-the-line competition mountain bike.   
          Performance-enhancing options include the innovative HL Frame,   
          super-smooth front suspension, and traction for all terrain.  
                            </html:p>  
                </p1:Summary>  
                <p1:Manufacturer>  
                    <p1:Name>AdventureWorks</p1:Name>  
                    <p1:Copyright>2002-2005</p1:Copyright>  
                    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
                </p1:Manufacturer>  
                <p1:Features>These are the product highlights.   
                     <wm:Warranty>  
                        <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
                        <wm:Description>parts and labor</wm:Description>  
                    </wm:Warranty><wm:Maintenance>  
                        <wm:NoOfYears>10 years</wm:NoOfYears>  
                        <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
                    </wm:Maintenance><wf:wheel>High performance wheels.</wf:wheel><wf:saddle>  
                        <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle><wf:pedal>  
                        <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal><wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter   
          and wall-thickness required of a premium mountain frame.   
          The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame><wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset></p1:Features>  
                <!-- add one or more of these elements... one for each specific product in this product model -->  
                <p1:Picture>  
                    <p1:Angle>front</p1:Angle>  
                    <p1:Size>small</p1:Size>  
                    <p1:ProductPhotoID>118</p1:ProductPhotoID>  
                </p1:Picture>  
                <!-- add any tags in <specifications> -->  
                <p1:Specifications> These are the product specifications.  
                       <Material>Almuminum Alloy</Material><Color>Available in most colors</Color><ProductLine>Mountain bike</ProductLine><Style>Unisex</Style><RiderExperience>Advanced to Professional riders</RiderExperience></p1:Specifications>  
            </p1:ProductDescription>  
        </Desc>  
    </ProductModel>  
    ```  
  
4.  Crie um arquivo em seu editor de texto ou editor XML preferido e salve-o como BulkloadXml.vbs. Copie o código VBScript a seguir e cole-o no arquivo. Salve-o na mesma pasta que foi usada para os arquivos de dados e de esquema XML anteriores.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=AdventureWorks;integrated security=SSPI"  
  
    Dim fso, sAppPath  
    Set fso = CreateObject("Scripting.FileSystemObject")   
    sAppPath = fso.GetFolder(".")   
  
    objBL.ErrorLogFile = sAppPath & "\error.log"  
  
    'Execute XML bulkload using file.  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  Execute o script BulkloadXml.vbs.  
  
  
