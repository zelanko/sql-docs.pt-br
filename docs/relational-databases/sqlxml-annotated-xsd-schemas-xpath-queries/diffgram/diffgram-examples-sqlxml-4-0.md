---
title: Exemplos de DiffGram (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], examples
- examples [SQLXML], DiffGram
- diffgr:parentID
- parentID annotation
ms.assetid: fc148583-dfd3-4efb-a413-f47b150b0975
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 326bd4b924e0bd5e474399a372248addce8c4b78
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030857"
---
# <a name="diffgram-examples-sqlxml-40"></a>Exemplos de DiffGram (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Os exemplos deste tópico consistem em DiffGrams que executam operações de inserção, atualização e exclusão no banco de dados. Antes de usar os exemplos, observe o seguinte:  
  
-   Os exemplos usarão duas tabelas (Cust e Ord) que devem ser criadas se você quiser testar os exemplos de DiffGram:  
  
    ```  
    Cust(CustomerID, CompanyName, ContactName)  
    Ord(OrderID, CustomerID)  
    ```  
  
-   A maioria dos exemplos deste tópico usa o seguinte Esquema XSD:  
  
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
  
     Salve este esquema como DiffGramSchema.xml na mesma pasta em que você salva outros arquivos usados nos exemplos.  
  
## <a name="a-deleting-a-record-by-using-a-diffgram"></a>A. Excluindo um registro usando um DiffGram  
 O DiffGram, neste exemplo, exclui um registro de cliente (com CustomerID ALFKI) da tabela Cust e exclui o registro de pedido correspondente (cuja OrderID é 1) da tabela Ord.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance/>  
  
    <diffgr:before>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI"   
               OrderID="1"/>  
        <Customer diffgr:id="Customer1"   
                  msdata:rowOrder="0"   
                  CustomerID="ALFKI">  
           <CompanyName>Alfreds Futterkiste</CompanyName>  
           <ContactName>Maria Anders</ContactName>  
        </Customer>  
    </diffgr:before>  
    <msdata:errors/>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 No  **\<antes de >** bloquear, há um  **\<Order >** elemento (**diffgr:ID="customer4 ="Diffgr:ID="Order1"**) e um  **\< Cliente >** elemento (**diffgr:ID="customer4 ="Customer1"**). Esses elementos representam registros existentes no banco de dados. O  **\<DataInstance >** elemento não tem os registros correspondentes (com o mesmo **diffgr:ID="customer4**). Isso indica um operação de exclusão.  
  
#### <a name="to-test-the-diffgram"></a>Para testar o DiffGram  
  
1.  Crie estas tabelas na **tempdb** banco de dados.  
  
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
  
2.  Adicione estes dados de exemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie o DiffGram acima e cole em um arquivo de texto. Salve o arquivo como MyDiffGram.xml na mesma pasta usada na etapa anterior.  
  
4.  Copie o DiffGramSchema fornecido anteriormente neste tópico e cole-o em um arquivo de texto. Salve o arquivo como DiffGramSchema.xml.  
  
5.  Crie e use o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o DiffGram.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="b-inserting-a-record-by-using-a-diffgram"></a>b. Inserindo um registro usando um DiffGram  
 Neste exemplo, o DiffGram insere um registro na tabela Cust e um registro na tabela Ord.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"   
      sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
          xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
          xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
       <Customer diffgr:id="Customer1" msdata:rowOrder="0"    
                 diffgr:hasChanges="inserted" CustomerID="ALFKI">  
        <CompanyName>C3Company</CompanyName>  
        <ContactName>C3Contact</ContactName>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"  
               diffgr:hasChanges="inserted"   
               CustomerID="ALFKI" OrderID="1"/>  
      </Customer>  
    </DataInstance>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 Neste DiffGram a  **\<antes de >** bloco não for especificado (nenhum banco de dados existente identificados de registros). Há duas instâncias de registro (identificado pela  **\<cliente >** e  **\<Order >** elementos no  **\<DataInstance >** bloco) que mapeiam para tabelas Cust e Ord, respectivamente. Esses dois elementos especificam o **diffgr: HasChanges** atributo (**hasChanges = "inserted"**). Isso indica uma operação de inserção. Nesse diffgram, se você especificar **hasChanges = "modified"**, você está indicando que você deseja modificar um registro não existir, o que resulta em um erro.  
  
#### <a name="to-test-the-diffgram"></a>Para testar o DiffGram  
  
1.  Crie estas tabelas na **tempdb** banco de dados.  
  
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
  
2.  Adicione estes dados de exemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie o DiffGram acima e cole em um arquivo de texto. Salve o arquivo como MyDiffGram.xml na mesma pasta usada na etapa anterior.  
  
4.  Copie o DiffGramSchema fornecido anteriormente neste tópico e cole-o em um arquivo de texto. Salve o arquivo como DiffGramSchema.xml.  
  
5.  Crie e use o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o DiffGram.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="c-updating-an-existing-record-by-using-a-diffgram"></a>C. Atualizando um registro existente usando um DiffGram  
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
  
 O  **\<antes de >** bloco inclui um  **\<cliente >** elemento (**diffgr:ID="customer4 ="Customer1"**). O  **\<DataInstance >** inclusões em bloco correspondente  **\<cliente >** elemento com o mesmo **id**. O  **\<cliente >** elemento no  **\<NewDataSet >** também especifica **diffgr: HasChanges = "modified"**. Isso indica uma operação de atualização e o registro do cliente na **Cust** tabela é atualizada adequadamente. Observe que, se o **diffgr: HasChanges** atributo não for especificado, a lógica de processamento de DiffGram ignora esse elemento e nenhuma atualização será executada.  
  
#### <a name="to-test-the-diffgram"></a>Para testar o DiffGram  
  
1.  Crie estas tabelas na **tempdb** banco de dados.  
  
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
  
2.  Adicione estes dados de exemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie o DiffGram acima e cole em um arquivo de texto. Salve o arquivo como MyDiffGram.xml na mesma pasta usada na etapa anterior.  
  
4.  Copie o DiffGramSchema fornecido anteriormente neste tópico e cole-o em um arquivo de texto. Salve o arquivo como DiffGramSchema.xml.  
  
5.  Crie e use o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o DiffGram.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="d-inserting-updating-and-deleting-records-by-using-a-diffgram"></a>D. Inserindo, atualizando e excluindo registros usando um DiffGram  
 Neste exemplo, um DiffGram relativamente complexo é usado para executar operações de inserção, atualização e exclusão.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                diffgr:hasChanges="modified"   
                CustomerID="ANATR">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Elizabeth Lincoln</ContactName>  
          <Order diffgr:id="Order2" msdata:rowOrder="1"   
               msdata:hiddenCustomerID="ANATR"   
               CustomerID="ANATR" OrderID="2"/>  
      </Customer>  
  
      <Customer diffgr:id="Customer3" msdata:rowOrder="2"   
                CustomerID="ANTON">  
         <CompanyName>Chop-suey Chinese</CompanyName>  
         <ContactName>Yang Wang</ContactName>  
         <Order diffgr:id="Order3" msdata:rowOrder="2"   
               msdata:hiddenCustomerID="ANTON"   
               CustomerID="ANTON" OrderID="3"/>  
      </Customer>  
      <Customer diffgr:id="Customer4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                CustomerID="AROUT">  
         <CompanyName>Around the Horn</CompanyName>  
         <ContactName>Thomas Hardy</ContactName>  
         <Order diffgr:id="Order4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                msdata:hiddenCustomerID="AROUT"   
               CustomerID="AROUT" OrderID="4"/>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
      <Order diffgr:id="Order1" msdata:rowOrder="0"   
             msdata:hiddenCustomerID="ALFKI"   
             CustomerID="ALFKI" OrderID="1"/>  
      <Customer diffgr:id="Customer1" msdata:rowOrder="0"   
                CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                CustomerID="ANATR">  
        <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
        <ContactName>Ana Trujillo</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 A lógica do DiffGram processa este DiffGram como a seguir:  
  
-   De acordo com a lógica de processamento de DiffGram, todos os elementos de nível superior na  **\<antes de >** bloquear são mapeados para tabelas correspondentes, conforme descrito no esquema de mapeamento.  
  
-   O  **\<antes de >** bloco tem um  **\<Order >** elemento (**dffgr:id = "Diffgr:ID="Order1"**) e um  **\<cliente >** elemento (**diffgr:ID="customer4 ="Customer1"**) para que não há nenhum elemento correspondente no  **\<DataInstance >** bloco (com a mesma ID). Isto indica uma operação de exclusão e os registros são excluídos das tabelas Cust e Ord.  
  
-   O  **\<antes de >** bloco tem um  **\<cliente >** elemento (**diffgr:ID="customer4 ="Customer2"**) para as quais há um correspondente **\<Cliente >** elemento de  **\<DataInstance >** bloco (com a mesma ID). O elemento de  **\<DataInstance >** bloco especifica **diffgr: HasChanges = "modified"**. Esta é uma operação de atualização em que para o cliente ANATR, as informações de CompanyName e ContactName são atualizadas na tabela Cust usando valores que são especificados na  **\<DataInstance >** bloco.  
  
-   O  **\<DataInstance >** bloco tem um  **\<cliente >** elemento (**diffgr:ID="customer4 ="Customer3"**) e um  **\<Ordem >** elemento (**diffgr:ID="customer4 ="Order3"**). Nenhum desses elementos especifica o **diffgr: HasChanges** atributo. Portanto, a lógica de processamento do DiffGram ignora esses elementos.  
  
-   O  **\<DataInstance >** bloco tem um  **\<cliente >** elemento (**diffgr:ID="customer4 ="Customer4"**) e um  **\<Ordem >** elemento (**diffgr:ID="customer4 ="Order4"**) para o qual há nenhum elemento correspondente no \<antes > bloco. Esses elementos na  **\<DataInstance >** bloco especificar **diffgr: HasChanges = "inserted"**. Portanto, um registro novo é adicionado na tabela Cust e na tabela Ord.  
  
#### <a name="to-test-the-diffgram"></a>Para testar o DiffGram  
  
1.  Criar as tabelas a seguir na **tempdb** banco de dados.  
  
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
  
2.  Adicione estes dados de exemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie o DiffGram acima e cole em um arquivo de texto. Salve o arquivo como MyDiffGram.xml na mesma pasta usada na etapa anterior.  
  
4.  Copie o DiffGramSchema fornecido anteriormente neste tópico e cole-o em um arquivo de texto. Salve o arquivo como DiffGramSchema.xml.  
  
5.  Crie e use o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o DiffGram.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. Aplicando atualizações usando um DiffGram com a anotação diffgr:parentID  
 Este exemplo ilustra como o **parentID** anotação é especificada na  **\<antes >** bloco de DiffGram é usado na aplicação das atualizações.  
  
```  
<NewDataSet />  
<diffgr:before>  
   <Order diffgr:id="Order1" msdata:rowOrder="0" OrderID="2" />  
   <Order diffgr:id="Order3" msdata:rowOrder="2" OrderID="4" />  
  
   <OrderDetail diffgr:id="OrderDetail1"   
                diffgr:parentId="Order1"   
                msdata:rowOrder="0"   
                ProductID="13"   
                OrderID="2" />  
   <OrderDetail diffgr:id="OrderDetail3"   
                diffgr:parentId="Order3"  
                ProductID="77"  
                OrderID="4"/>  
</diffgr:before>  
</diffgr:diffgram>  
```  
  
 Este DiffGram Especifica uma operação de exclusão porque há apenas um  **\<antes de >** bloco. No DiffGram, o **parentID** anotação é usada para especificar uma relação pai-filho entre os pedidos e detalhes do pedido. Quando SQLXML exclui os registros, ele exclui registros da tabela filho identificada por essa relação e, em seguida, exclui os registros da tabela pai correspondente.  
  
  
