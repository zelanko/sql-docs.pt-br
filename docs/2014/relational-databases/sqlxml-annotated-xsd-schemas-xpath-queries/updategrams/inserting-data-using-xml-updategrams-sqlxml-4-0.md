---
title: Inserindo dados usando Updategrams XML (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- xsi:nil attribute
- unique values
- <after> block
- id attribute
- data insertions [SQLXML]
- nil attribute
- <before> block
- updg:guid attribute
- multiple record insertions
- returnid attribute
- updategrams [SQLXML], inserting data
- updg:at-identity attribute
- invalid characters [SQLXML]
- updg:returnid attribute
- updg:id attribute
- namespaces [SQLXML], updategrams
- IDENTITY-type column
- guid attribute
- record insertion [SQLXML]
- null values [SQLXML]
- at-identity attribute
- xml data type [SQL Server], SQLXML
ms.assetid: 4dc48762-bc12-43fb-b356-ea1b9c1e287e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b06e98d5ef3dfc4ad8ab99e374e2d7b5539c98be
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637905"
---
# <a name="inserting-data-using-xml-updategrams-sqlxml-40"></a>Inserindo dados usando diagramas de atualização XML (SQLXML 4.0)
  Um updategram indica uma operação de inserção quando uma instância de registro é exibida na **\<depois de >** bloco, mas não no **\<correspondente antes de >** bloco. Nesse caso, o updategram insere o registro no **\<depois de >** bloco no banco de dados.  
  
 Este é o formato do diagrama de atualização em uma operação de inserção:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   [<updg:before>  
   </updg:before>]  
    <updg:after [updg:returnid="x y ...] >  
       <ElementName [updg:id="value"]   
                   [updg:at-identity="x"]   
                   [updg:guid="y"]  
                   attribute="value"   
                   attribute="value"  
                   ...  
       />  
      [<ElementName .../>... ]  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
## <a name="before-block"></a>\<antes do bloco >  
 O **\<antes de >** bloco pode ser omitido para uma operação de inserção. Se o atributo opcional `mapping-schema` não for especificado, o **\<ElementName >** especificado no updategram será mapeado para uma tabela de banco de dados e os elementos filho ou atributos serão mapeados para colunas na tabela.  
  
## <a name="after-block"></a>\<após o bloco de >  
 Você pode especificar um ou mais registros no **\<após >** bloco.  
  
 Se o **\<após** o bloco de > não fornecer um valor para uma coluna específica, o updategram usará o valor padrão especificado no esquema anotado (se um esquema tiver sido especificado). Se o esquema não especificar um valor padrão para a coluna, o updategram não especificará nenhum valor explícito para essa coluna e, em vez disso, atribuirá o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] valor padrão (se especificado) a essa coluna. Se não houver nenhum valor padrão [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e a coluna aceitar um valor NULL, o diagrama de atualização definirá o valor da coluna como NULL. Caso a coluna não tenha um valor padrão nem aceite valores NULL, o comando apresentará uma falha e o diagrama de atualização retornará um erro. O atributo opcional `updg:returnid` é usado para retornar o valor de identidade gerado pelo sistema quando um registro é adicionado a uma tabela com uma coluna do tipo IDENTITY.  
  
## <a name="updgid-attribute"></a>Atributo updg:id  
 Se o diagrama de atualização só estiver inserindo registros, ele não exigirá o atributo `updg:id`. Para obter mais informações sobre `updg:id`, consulte [atualizando dados usando os &#40;updategrams XML&#41;SQLXML 4,0](updating-data-using-xml-updategrams-sqlxml-4-0.md).  
  
## <a name="updgat-identity-attribute"></a>Atributo updg:at-identity  
 Quando um diagrama de atualização insere um registro em uma tabela que possui uma coluna do tipo IDENTITY, o diagrama pode capturar o valor atribuído do sistema usando o atributo opcional `updg:at-identity`. Esse valor pode ser usado em todas as operações subsequentes. Após a execução do diagrama de atualização, você pode retornar o valor de identidade gerado pela especificação do atributo `updg:returnid`.  
  
## <a name="updgguid-attribute"></a>Atributo updg:guid  
 O atributo `updg:guid` é um atributo opcional que gera um identificador globalmente exclusivo. Esse valor permanece no escopo para todo o **\<** o bloco de > de sincronização em que é especificado. Você pode usar esse valor em qualquer lugar no bloco **\<sincronizar >** . O atributo chama a função `NEWGUID()`[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para gerar o identificador exclusivo.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de trabalho usando os exemplos a seguir, você deve atender aos requisitos especificados em [requisitos para executar exemplos do SQLXML](../../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
 Antes de usar os exemplos de diagrama de atualização, observe o seguinte:  
  
-   A maioria dos exemplos usa mapeamento padrão (ou seja, nenhum esquema de mapeamento é especificado no diagrama de atualização). Para obter mais exemplos de Updategrams que usam esquemas de mapeamento, consulte [especificando um esquema de mapeamento anotado em um &#40;SQLXML do&#41;updategram 4,0](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
-   A maioria dos exemplos usa o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]. Todas as atualizações são aplicadas às tabelas deste banco de dados.  
  
### <a name="a-inserting-a-record-by-using-an-updategram"></a>A. Inserindo um registro usando um diagrama de atualização  
 Este diagrama de atualização centrado em atributo insere um registro na tabela HumanResources.Employee do banco de dados [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)].  
  
 Neste exemplo, o diagrama de atualização não especifica um esquema de mapeamento. Dessa forma, o diagrama usa o mapeamento padrão, no qual o nome do elemento é mapeado para um nome de tabela e os atributos ou elementos filho para as colunas contidas nessa tabela.  
  
 O esquema [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] para a tabela HumanResources.Department impõe uma restrição 'não nulo' em todas as colunas. Portanto, o diagrama de atualização deve incluir valores especificados para todas as colunas. DepartmentID é uma coluna do tipo IDENTITY. Por isso, nenhum valor é especificado para ela.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name="New Product Research"   
            GroupName="Research and Development"   
            ModifiedDate="2010-08-31"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como MyUpdategram.xml.  
  
2.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Em um mapeamento centrado em elemento, o diagrama de atualização tem esta aparência:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department>  
            <Name> New Product Research </Name>  
            <GroupName> Research and Development </GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Em um diagrama de atualização de modo misto (centrado em elemento e centrado em atributo), um elemento pode ter tanto atributos como subelementos, conforme mostrado neste diagrama:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name=" New Product Research "   
            <GroupName>Research and Development</GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="b-inserting-multiple-records-by-using-an-updategram"></a>B. Inserindo vários registros usando um diagrama de atualização  
 Este diagrama de atualização adiciona dois novos registros de troca à tabela HumanResources.Shift. O updategram não especifica o\<opcional **antes** do bloco de >.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como Updategram-AddShifts.xml.  
  
2.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Outra versão deste exemplo é um updategram que usa duas\<separadas **depois que >** blocos, em vez de um bloco para inserir os dois funcionários. Isso é válido e pode ser codificado da seguinte maneira:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after >  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="c-working-with-valid-sql-server-characters-that-are-not-valid-in-xml"></a>C. Trabalhando com caracteres SQL Server válidos que não são válidos no XML  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], os nomes de tabela podem incluir um espaço, como a tabela Order Details no banco de dados Northwind. No entanto, isso não é válido em caracteres XML válidos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identificadores, mas não identificadores XML válidos podem ser codificados usando ' __xHHHH\_\_' como o valor de codificação, em que HHHH significa o código UCS-2 hexadecimal de quatro dígitos para o caractere em a ordem mais significativa do bit.  
  
> [!NOTE]  
>  Este exemplo usa o banco de dados Northwind. Você pode instalar o banco de dados Northwind usando um script SQL disponível para download neste [site da Microsoft](https://www.microsoft.com/download/details.aspx?id=23654).  
  
 Além disso, o nome do elemento deve ser colocado entre colchetes ([]). Como os caracteres [e] não são válidos em XML, você deve codificá-los como _x005B\_ e _x005D\_, respectivamente. (Se você usar um esquema de mapeamento, poderá fornecer nomes de elemento que não contêm caracteres inválidos, como espaços em branco. O esquema de mapeamento faz o mapeamento necessário; portanto, você não precisa codificar esses caracteres).  
  
 Este diagrama de atualização adiciona um registro à tabela Order Details no banco de dados Northwind:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <_x005B_Order_x0020_Details_x005D_ OrderID="1"  
            ProductID="11"  
            UnitPrice="$1.0"  
            Quantity="1"  
            Discount="0.0" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 A coluna UnitPrice da tabela Order Details é do tipo `money`. Para aplicar a conversão de tipo apropriada (de um tipo `string` em um tipo `money`), o caractere de cifrão ($) deve ser adicionado como parte do valor. Se o diagrama de atualização não especificar um esquema de mapeamento, o primeiro caractere do valor `string` será avaliado. Se o primeiro caractere for um cifrão ($), a conversão apropriada será aplicada.  
  
 Se o diagrama de atualização for especificado em um esquema de mapeamento em que a coluna seja marcada como `dt:type="fixed.14.4"` ou `sql:datatype="money"`, o cifrão ($) não será necessário e a conversão será feita pelo mapeamento. Esse é o modo recomendado para garantir uma conversão de tipos bem-sucedida.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como UpdategramSpacesInTableName.xml.  
  
2.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="d-using-the-at-identity-attribute-to-retrieve-the-value-that-has-been-inserted-in-the-identity-type-column"></a>D. Usando o atributo at-identity para recuperar o valor inserido na coluna do tipo IDENTITY  
 O diagrama de atualização a seguir insere dois registros: um na tabela Sales.SalesOrderHeader e outro na tabela Sales.SalesOrderDetail.  
  
 Primeiro, o diagrama adiciona um registro à tabela Sales.SalesOrderHeader. Nessa tabela, a coluna SalesOrderID é uma coluna do tipo IDENTITY. Portanto, quando você adiciona esse registro à tabela, o diagrama de atualização usa o atributo `at-identity` para capturar o valor SalesOrderID atribuído como "x" (um valor de espaço reservado). O updategam então especifica essa `at-identity` variável como o valor do atributo SalesOrderID no elemento \<Sales. SalesOrderDetail >.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
   <Sales.SalesOrderHeader updg:at-identity="x"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00001111-2222-3333-4444-556677889900"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
      <Sales.SalesOrderDetail SalesOrderID="x"  
                LineNumber="1"  
                OrderQty="1"  
                ProductID="776"  
                SpecialOfferID="1"  
                UnitPrice="2429.9928"  
                UnitPriceDiscount="0.00"  
                rowguid="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"  
                ModifiedDate="2001-07-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Se você quiser retornar o valor de identidade gerado pelo atributo `updg:at-identity`, poderá usar o atributo `updg:returnid`. A seguir, é mostrado um diagrama de atualização revisado que retorna esse valor de identidade. (Esse diagrama adiciona dois registros de pedido e dois registros de detalhe de pedido, só para tornar o exemplo um pouco mais complexo.)  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync>  
  <updg:before>  
  </updg:before>  
  <updg:after updg:returnid="x y" >  
       <HumanResources.Shift updg:at-identity="x" Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift updg:at-identity="y" Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:after>  
 </updg:sync>  
</ROOT>  
```  
  
 Quando o diagrama é executado, ele retorna resultados semelhantes aos mostrados a seguir, incluindo o valor de identidade (o valor gerado da coluna ShiftID usado para a identidade da tabela) gerado:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">   
  <returnid>   
    <x>4</x>   
    <y>5</y>   
  </returnid>   
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como Updategram-returnId.xml.  
  
2.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="e-using-the-updgguid-attribute-to-generate-a-unique-value"></a>E. Usando o atributo updg:guid para gerar um valor exclusivo  
 Nesse exemplo, o diagrama de atualização insere um registro nas tabelas Cust e CustOrder. Além disso, o diagrama gera um valor exclusivo para o atributo CustomerID usando o atributo `updg:guid`.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after updg:returnid="x" >  
      <Cust updg:guid="x" >  
         <CustID>x</CustID>  
         <LastName>Fuller</LastName>  
      </Cust>  
      <CustOrder>  
         <CustID>x</CustID>  
         <OrderID>1</OrderID>  
      </CustOrder>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 O diagrama especifica o atributo `returnid`. Como resultado, o GUID gerado é retornado:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <returnid>  
    <x>7111BD1A-7F0B-4CEE-B411-260DADFEFA2A</x>   
  </returnid>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como Updategram-GenerateGuid.xml.  
  
2.  Crie estas tabelas:  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust (CustID uniqueidentifier, LastName varchar(20))  
    CREATE TABLE CustOrder (CustID uniqueidentifier, OrderID int)  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="f-specifying-a-schema-in-an-updategram"></a>F. Especificando um esquema em um diagrama de atualização  
 O diagrama deste exemplo insere um registro na seguinte tabela:  
  
```  
CustOrder(OrderID, EmployeeID, OrderType)  
```  
  
 Um esquema XSD é especificado nesse diagrama (ou seja, não há nenhum mapeamento padrão dos elementos e atributos). O esquema fornece o mapeamento necessário dos elementos e atributos para as tabelas e colunas do banco de dados.  
  
 O esquema a seguir (CustOrderSchema. xml) descreve um elemento **\<CustOrder >** que consiste nos atributos **OrderID** e **EmployeeID** . Para tornar o esquema mais interessante, um valor padrão é atribuído ao atributo **EmployeeID** . Um diagrama usa o valor padrão de um atributo apenas em operações de inserção e, nesse caso, só se o diagrama não especificar tal atributo.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="CustOrder" >  
   <xsd:complexType>  
        <xsd:attribute name="OrderID"     type="xsd:integer" />   
        <xsd:attribute name="EmployeeID"  type="xsd:integer" />  
        <xsd:attribute name="OrderType  " type="xsd:integer" default="1"/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Esse diagrama insere um registro na tabela CustOrder. O diagrama especifica apenas os valores de atributo OrderID e EmployeeID. Ele não especifica o valor de atributo OrderType. Dessa forma, o diagrama usa o valor padrão do atributo EmployeeID especificado no esquema anterior.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
             xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync mapping-schema='CustOrderSchema.xml'>  
<updg:after>  
       <CustOrder OrderID="98000" EmployeeID="1" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 Para obter mais exemplos de Updategrams que especificam um esquema de mapeamento, consulte [especificando um esquema de mapeamento anotado &#40;em um&#41;SQLXML do updategram 4,0](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Crie esta tabela no banco de dados **tempdb** :  
  
    ```  
    USE tempdb  
    CREATE TABLE CustOrder(  
                     OrderID int,   
                     EmployeeID int,   
                     OrderType int)  
    ```  
  
2.  Copie o esquema acima e cole-o em um arquivo de texto. Salve o arquivo como CustOrderSchema.xml.  
  
3.  Copie o diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como CustOrderUpdategram.xml na mesma pasta usada na etapa anterior.  
  
4.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o esquema XDR equivalente:  
  
```  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
 <ElementType name="CustOrder" >  
    <AttributeType name="OrderID" />  
    <AttributeType name="EmployeeID" />  
    <AttributeType name="OrderType" default="1" />  
    <attribute type="OrderID"  />  
    <attribute type="EmployeeID" />  
    <attribute type="OrderType" />  
  </ElementType>  
</Schema>  
```  
  
### <a name="g-using-the-xsinil-attribute-to-insert-null-values-in-a-column"></a>G. Usando o atributo xsi:nil para inserir valores nulos em uma coluna  
 Caso queira inserir um valor nulo na coluna correspondente da tabela, você pode especificar o atributo `xsi:nil` em um elemento de um diagrama. No esquema XSD correspondente, o atributo XSD `nillable` também deve ser especificado.  
  
 Por exemplo, considere este esquema XSD:  
  
```  
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="Student" sql:relation="Students">  
  <xsd:complexType>  
    <xsd:all>  
      <xsd:element name="fname" sql:field="first_name"   
                                type="xsd:string"   
                                 nillable="true"/>  
    </xsd:all>  
    <xsd:attribute name="SID"   
                        sql:field="StudentID"  
                        type="xsd:ID"/>      
    <xsd:attribute name="lname"       
                        sql:field="last_name"  
                        type="xsd:string"/>  
    <xsd:attribute name="minitial"    
                        sql:field="middle_initial"   
                        type="xsd:string"/>  
    <xsd:attribute name="years"       
                         sql:field="no_of_years"  
                         type="xsd:integer"/>  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 O esquema XSD especifica **anulável = "true"** para o elemento **\<fname >** . O seguinte diagrama usa esse esquema:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
      xmlns:updg="urn:schemas-microsoft-com:xml-updategram"  
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  
<updg:sync mapping-schema='StudentSchema.xml'>  
  <updg:before/>  
  <updg:after>  
    <Student SID="S00004" lname="Elmaci" minitial="" years="2">  
      <fname xsi:nil="true">  
    </fname>  
    </Student>  
  </updg:after>  
</updg:sync>  
  
</ROOT>  
```  
  
 O updategram especifica `xsi:nil` para o elemento **\<fname >** no **\<depois** do bloco de >. Portanto, quando esse diagrama é executado, um valor NULL é inserido na coluna first_name da tabela.  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Crie a tabela a seguir no banco de dados **tempdb** :  
  
    ```  
    USE tempdb  
    CREATE TABLE Students (  
       StudentID char(6)NOT NULL ,  
       first_name varchar(50),  
       last_name varchar(50),  
       middle_initial char(1),  
       no_of_years int NULL)  
    GO  
    ```  
  
2.  Copie o esquema acima e cole-o em um arquivo de texto. Salve o arquivo como StudentSchema.xml.  
  
3.  Copie o diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como StudentUpdategram.xml na mesma pasta usada na etapa anterior para salvar StudentSchema.xml.  
  
4.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="h-specifying-namespaces-in-an-updategram"></a>H. Especificando namespaces em um diagrama de atualização  
 Em um diagrama de atualização, você pode ter elementos que pertencem a um namespace declarado no mesmo elemento do diagrama. Nesse caso, o esquema correspondente deve declarar também o mesmo namespace e o elemento deve pertencer àquele namespace de destino.  
  
 Por exemplo, no updategram (UpdateGram-ElementHavingNamespace. xml) a seguir, o elemento **\<Order >** pertence a um namespace declarado no elemento.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema='XSD-ElementHavingNameSpace.xml'>  
    <updg:after>  
       <x:Order  xmlns:x="http://server/xyz/schemas/"  
             updg:at-identity="SalesOrderID"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00009999-8888-7777-6666-554433221100"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Nesse caso, o esquema deve declarar também o namespace como mostrado neste esquema:  
  
 O esquema a seguir (XSD-ElementHavingNamespace.xml) mostra como o elemento e os atributos correspondentes devem ser declarados.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
     xmlns:dt="urn:schemas-microsoft-com:datatypes"   
     xmlns:sql="urn:schemas-microsoft-com:mapping-schema"    
     xmlns:x="http://server/xyz/schemas/"   
     targetNamespace="http://server/xyz/schemas/" >  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" type="x:Order_type"/>  
  <xsd:complexType name="Order_type">  
    <xsd:attribute name="SalesOrderID"  type="xsd:ID"/>  
    <xsd:attribute name="RevisionNumber" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OrderDate" type="xsd:dateTime"/>  
    <xsd:attribute name="DueDate" type="xsd:dateTime"/>  
    <xsd:attribute name="ShipDate" type="xsd:dateTime"/>  
    <xsd:attribute name="Status" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OnlineOrderFlag" type="xsd:boolean"/>  
    <xsd:attribute name="SalesOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="PurchaseOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="AccountNumber" type="xsd:string"/>  
    <xsd:attribute name="CustomerID" type="xsd:int"/>  
    <xsd:attribute name="ContactID" type="xsd:int"/>  
    <xsd:attribute name="SalesPersonID" type="xsd:int"/>  
    <xsd:attribute name="TerritoryID" type="xsd:int"/>  
    <xsd:attribute name="BillToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipMethodID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardApprovalCode" type="xsd:string"/>  
    <xsd:attribute name="CurrencyRateID" type="xsd:int"/>  
    <xsd:attribute name="SubTotal" type="xsd:decimal"/>  
    <xsd:attribute name="TaxAmt" type="xsd:decimal"/>  
    <xsd:attribute name="Freight" type="xsd:decimal"/>  
    <xsd:attribute name="TotalDue" type="xsd:decimal"/>  
    <xsd:attribute name="Comment" type="xsd:string"/>  
    <xsd:attribute name="rowguid" type="xsd:string"/>  
    <xsd:attribute name="ModifiedDate" type="xsd:dateTime"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o esquema acima e cole-o em um arquivo de texto. Salve o arquivo como XSD-ElementHavingNamespace.xml.  
  
2.  Copie o diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como Updategram-ElementHavingNamespace.xml na mesma pasta usada para salvar XSD-ElementHavingnamespace.xml.  
  
3.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="i-inserting-data-into-an-xml-data-type-column"></a>I. Inserindo dados em uma coluna de tipo de dados XML  
 O tipo de dados `xml` foi introduzido no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Você pode usar diagramas de atualização para inserir e atualizar dados armazenados em colunas de tipo de dados `xml` com as seguintes provisões:  
  
-   A coluna `xml` não pode ser usada para identificar uma linha existente. Portanto, ela não pode ser incluída na seção `updg:before` de um diagrama.  
  
-   Os namespaces incluídos no escopo do fragmento XML inserido na coluna `xml` serão preservados e suas declarações de namespace serão adicionadas ao elemento superior do fragmento inserido.  
  
 Por exemplo, no updategram (SampleUpdateGram. xml) a seguir, o elemento **\<Desc >** atualiza a coluna ProductDescription na tabela ProductModel de produção > no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]. O resultado desse updategram é que o conteúdo XML da coluna ProductDescription é atualizado com o conteúdo XML do elemento **\<Desc >** .  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
       <updg:before>  
<ProductModel ProductModelID="19">  
   <Name>Mountain-100</Name>  
</ProductModel>  
    </updg:before>  
    <updg:after>  
 <ProductModel>  
    <Name>Mountain-100</Name>  
    <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
        <p1:ProductDescription xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
              xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
              xmlns:wf="http://www.adventure-works.com/schemas/OtherFeatures"   
              xmlns:html="http://www.w3.org/1999/xhtml"   
              xmlns="">  
  <p1:Summary>  
     <html:p>Insert Example</html:p>  
  </p1:Summary>  
  <p1:Manufacturer>  
    <p1:Name>AdventureWorks</p1:Name>  
    <p1:Copyright>2002</p1:Copyright>  
    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
  </p1:Manufacturer>  
  <p1:Features>These are the product highlights.   
    <wm:Warranty>  
       <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
       <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
    <wm:Maintenance>  
       <wm:NoOfYears>10 years</wm:NoOfYears>  
       <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
    </wm:Maintenance>  
    <wf:wheel>High performance wheels.</wf:wheel>  
    <wf:saddle>  
      <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle>  
    <wf:pedal>  
       <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal>  
    <wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter and wall-thickness required of a premium mountain frame. The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame>  
    <wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset>  
   </p1:Features>  
   <p1:Picture>  
      <p1:Angle>front</p1:Angle>  
      <p1:Size>small</p1:Size>  
      <p1:ProductPhotoID>118</p1:ProductPhotoID>  
   </p1:Picture>  
   <p1:Specifications> These are the product specifications.  
     <Material>Almuminum Alloy</Material>  
     <Color>Available in most colors</Color>  
     <ProductLine>Mountain bike</ProductLine>  
     <Style>Unisex</Style>  
     <RiderExperience>Advanced to Professional riders</RiderExperience>  
   </p1:Specifications>  
  </p1:ProductDescription>  
 </Desc>  
      </ProductModel>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 O diagrama faz referência ao seguinte esquema XSD anotado (SampleSchema.xml):  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
     <xsd:complexType>  
       <xsd:sequence>  
          <xsd:element name="Name" type="xsd:string"></xsd:element>  
          <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
           <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="ProductDescription">  
                 <xsd:complexType>  
                   <xsd:sequence>  
                     <xsd:element name="Summary" type="xsd:anyType">  
                     </xsd:element>  
                   </xsd:sequence>  
                 </xsd:complexType>  
              </xsd:element>  
            </xsd:sequence>  
           </xsd:complexType>  
          </xsd:element>   
       </xsd:sequence>  
       <xsd:attribute name="ProductModelID" sql:field="ProductModelID"/>  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o esquema acima e cole-o em um arquivo de texto. Salve o arquivo como XSD-SampleSchema.xml.  
  
    > [!NOTE]  
    >  Pelo fato de os diagramas suportarem o mapeamento padrão, não há como identificar o começo e o fim do tipo de dados `xml`. Na prática, isso significa que será necessário um esquema de mapeamento durante a inserção ou atualização de tabelas com colunas de tipo de dados `xml`. Quando um esquema não é fornecido, SQLXML retorna um erro informando que uma das colunas da tabela está faltando.  
  
2.  Copie o diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como SampleUpdategram.xml na mesma pasta usada para salvar SampleSchema.xml.  
  
3.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Consulte também  
 [Considerações &#40;de segurança do Updategram SQLXML 4,0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
