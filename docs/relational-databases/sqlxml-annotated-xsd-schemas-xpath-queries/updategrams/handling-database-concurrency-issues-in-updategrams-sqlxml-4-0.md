---
title: Problemas de simultaneidade de banco de dados em Updategrams (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- <before> block
- low concurrency protection
- database concurrency [SQLXML]
- timestamp column [SQLXML]
- updategrams [SQLXML], database concurrency
- high concurrency protection [SQLXML]
- optimistic concurrency control
- concurrency [SQLXML]
- intermediate concurrency protection [SQLXML]
ms.assetid: d4b908d1-b25b-4ad9-8478-9cd882e8c44e
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eb77a6499472d116ad3b30028ce1566b68b81122
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75241289"
---
# <a name="handling-database-concurrency-issues-in-updategrams-sqlxml-40"></a>Manipulando problemas de simultaneidade de banco de dados nos diagramas de atualização (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Da mesma forma que outros mecanismos de atualização de banco de dados, os diagramas de atualização devem lidar com atualizações simultâneas dos dados em um ambiente multiusuário. Os diagramas de atualização usam o Controle de simultaneidade otimista, que usa a comparação de dados de campos selecionados como instantâneos para garantir que os dados a serem atualizados não foram alterados por outro aplicativo de usuário desde que foram lidos do banco de dados. Os Updategrams incluem esses valores de instantâneo no bloco ** \<before>** dos Updategrams. Antes de atualizar o banco de dados, o updategram verifica os valores especificados no bloco ** \<before>** em relação aos valores atualmente no banco de dados para garantir que a atualização seja válida.  
  
 O Controle de simultaneidade otimista oferece três níveis de proteção em um diagrama de atualização: baixo (nenhum), intermediário e alto. Você pode decidir qual o nível de proteção necessário especificando o diagrama de atualização de acordo com ele.  
  
## <a name="lowest-level-of-protection"></a>Nível de proteção mais baixo  
 Este nível é uma atualização cega, no qual a atualização é processada sem referência a outras atualizações que foram feitas desde que o banco de dados foi lido pela última vez. Nesse caso, você especifica apenas as colunas de chave primária no bloco ** \<before>** para identificar o registro e especifica as informações atualizadas no bloco ** \<After>** .  
  
 Por exemplo, o novo número de telefone de contato no seguinte diagrama de atualização está correto, não importando qual tenha sido o número de telefone anteriormente. Observe como o ** \<bloco before>** especifica apenas a coluna de chave primária (ContactID).  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="intermediate-level-of-protection"></a>Nível de proteção intermediário  
 Neste nível de proteção, o diagrama de atualização compara os valores atuais dos dados que estão sendo atualizados com os valores nas colunas do banco de dados, para garantir que os valores não foram alterados por alguma outra transação desde que o registro foi lido pela sua transação.  
  
 Você pode obter esse nível de proteção especificando as colunas de chave primária e as colunas que você está atualizando no bloco ** \<before>** .  
  
 Por exemplo, este diagrama de atualização altera o valor na coluna Phone da tabela Person.Contact para o contato com ContactID igual a 1. O ** \<bloco before>** especifica o atributo **Phone** para garantir que esse valor de atributo corresponda ao valor na coluna correspondente no banco de dados antes de aplicar o valor atualizado.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" Phone="398-555-0132" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="high-level-of-protection"></a>Nível de proteção alto  
 Um nível de proteção alto garante que o registro permanecerá o mesmo desde que o seu aplicativo o leu pela última vez (ou seja, desde que o seu aplicativo leu o registro, ele não foi alterado por nenhuma outra transação).  
  
 Há duas formas através das quais você pode obter esse nível de proteção alto contra atualizações simultâneas:  
  
-   Especifique colunas adicionais na tabela no bloco ** \<antes de>** .  
  
     Se você especificar colunas adicionais no bloco ** \<before>** , o updategram compara os valores especificados para essas colunas com os valores que estavam no banco de dados antes de aplicar a atualização. Se qualquer uma das colunas do registro tiver sido alterada desde que a sua transação leu o registro, o diagrama de atualização não realizará a atualização.  
  
     Por exemplo, o updategram a seguir atualiza o nome da mudança, mas especifica colunas adicionais (StartTime, EndTime) no bloco ** \<before>** , solicitando assim um nível mais alto de proteção contra atualizações simultâneas.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1"   
                 Name="Day"   
                 StartTime="1900-01-01 07:00:00.000"   
                 EndTime="1900-01-01 15:00:00.000" />  
    </updg:before>  
    <updg:after>  
       <HumanResources.Shift Name="Morning" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
     Este exemplo especifica o nível mais alto de proteção especificando todos os valores de coluna para o registro no bloco ** \<before>** .  
  
-   Especifique a coluna timestamp (se disponível) no bloco ** \<before>** .  
  
     Em vez de especificar todas as colunas de registro no bloco ** \<before**>, você pode apenas especificar a coluna timestamp (se a tabela tiver uma) junto com as colunas de chave primária no bloco ** \<before>** . O banco de dados atualiza a coluna de carimbo de data e hora com um valor exclusivo depois de cada atualização do registro. Nesse caso, o diagrama de atualização compara o valor do carimbo de data e hora com o valor correspondente no banco de dados. O valor do carimbo de data e hora armazenado no banco de dados é um valor binário. Portanto, a coluna timestamp deve ser especificada no esquema como **dt: Type = "bin. hex"**, **dt: Type = "bin. base64"** ou **SQL: datatype = "timestamp"**. (Você pode especificar o tipo de dados **XML** ou o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de dados.)  
  
#### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Crie esta tabela no banco de dados **tempdb** :  
  
    ```  
    USE tempdb  
    CREATE TABLE Customer (  
                 CustomerID  varchar(5),  
                 ContactName varchar(20),  
                 LastUpdated timestamp)  
    ```  
  
2.  Adicione este registro de exemplo:  
  
    ```  
    INSERT INTO Customer (CustomerID, ContactName) VALUES   
                         ('C1', 'Andrew Fuller')  
    ```  
  
3.  Copie o seguinte esquema XSD e cole-o no Bloco de Notas. Salve como ConcurrencySampleSchema.xml:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Customer" sql:relation="Customer" >  
       <xsd:complexType>  
            <xsd:attribute name="CustomerID"    
                           sql:field="CustomerID"   
                           type="xsd:string" />   
  
            <xsd:attribute name="ContactName"    
                           sql:field="ContactName"   
                           type="xsd:string" />  
  
            <xsd:attribute name="LastUpdated"   
                           sql:field="LastUpdated"   
                           type="xsd:hexBinary"   
                 sql:datatype="timestamp" />  
  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
4.  Copie o seguinte código de diagrama de atualização no Bloco de Notas e salve como ConcurrencySampleTemplate.xml, no mesmo diretório em que você salvou o esquema criado na etapa anterior. (Observe que o seguinte valor de carimbo de data e hora para LastUpdated será diferente na sua tabela Customer de exemplo, portanto copie o valor real de LastUpdated da tabela e cole-o no diagrama de atualização.)  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
    <updg:before>  
       <Customer CustomerID="C1"   
                 LastUpdated = "0x00000000000007D1" />  
    </updg:before>  
    <updg:after>  
       <Customer ContactName="Robert King" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
5.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="ContactName" />  
    <AttributeType name="LastUpdated"  dt:type="bin.hex"   
                                       sql:datatype="timestamp" />  
    <attribute type="CustomerID" />  
    <attribute type="ContactName" />  
    <attribute type="LastUpdated" />  
</ElementType>  
</Schema>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações de segurança do updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
