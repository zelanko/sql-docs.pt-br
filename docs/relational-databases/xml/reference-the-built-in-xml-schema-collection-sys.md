---
title: Referenciar a coleção de esquemas XML interna (sys) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sys XML schema collections [SQL Server]
- schema collections [SQL Server], predefined
- predefined XML schema collections [SQL Server]
- XML schema collections [SQL Server], predefined
- built-in XML schema collections [SQL Server]
ms.assetid: 1e118303-5df0-4ee4-bd8d-14ced7544144
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4e0c3e8619db6d5f6c325b6762ca3bc4976f223b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="reference-the-built-in-xml-schema-collection-sys"></a>Referenciar a coleção de esquemas XML interna (sys)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Todo banco de dados que você cria tem uma coleção de esquema XML **sys** predefinido no esquema relacional **sys** . Ele reserva esses esquemas predefinidos que podem ser acessados de qualquer outra coleção de esquema XML criada pelo usuário. Os prefixos usados nesses esquemas predefinidos são significativos em XQuery. Apenas **xml** é um prefixo reservado.  
  
```  
xml = http://www.w3.org/XML/1998/namespace  
xs = http://www.w3.org/2001/XMLSchema  
xsi = http://www.w3.org/2001/XMLSchema-instance  
fn = http://www.w3.org/2004/07/xpath-functions  
sqltypes = http://schemas.microsoft.com/sqlserver/2004/sqltypes  
xdt = http://www.w3.org/2004/07/xpath-datatypes  
(no prefix) = urn:schemas-microsoft-com:xml-sql  
(no prefix) = http://schemas.microsoft.com/sqlserver/2004/SOAP  
```  
  
 Observe que o namespace **sqltypes** contém componentes que podem ser referidos de qualquer coleção de esquema XML criada pelo usuário. Você pode baixar o esquema **sqltypes** deste [site da Microsoft](http://go.microsoft.com/fwlink/?linkid=31850). Os componentes internos incluem o seguinte:  
  
-   Tipos XSD  
  
-   Atributos XML **lang**, **base**e **space**  
  
-   Componentes do namespace **sqltypes**  
  
 A consulta a seguir retorna componentes internos que podem ser referidos a partir de uma coleção de esquema XML:  
  
```  
SELECT C.name, N.name, C.symbol_space_desc from sys.xml_schema_components C join sys.xml_schema_namespaces N  
on ((C.xml_namespace_id = N.xml_namespace_id) AND (C.xml_collection_id = N.xml_collection_id))  
join sys.xml_schema_collections SC  
on SC.xml_collection_id = C.xml_collection_id  
where ((C.xml_collection_id = 1) AND (C.name is not null) AND (C.scoping_xml_component_id is null)   
AND (SC.schema_id = 4))  
GO  
```  
  
 O exemplo a seguir mostra como esses componentes são referenciados em um esquema de usuário. `CREATE XML SCHEMA COLLECTION` cria uma coleção de esquemas XML que referencia o tipo `varchar` definido no namespace `sqltypes` . O exemplo também referencia o atributo `lang` que está definido no namespace `xml` .  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema   
   xmlns="http://www.w3.org/2001/XMLSchema"   
   targetNamespace="myNS"  
   xmlns:ns="myNS"  
   xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
   <import namespace="http://www.w3.org/XML/1998/namespace"/>  
   <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
   <element name="root">  
      <complexType>  
          <sequence>  
             <element name="a" type="string"/>  
             <element name="b" type="string"/>  
             <!-- varchar type is defined in the sys.sys collection and   
                  can be referenced in any user-defined schema -->  
             <element name="c" type="s:varchar"/>  
          </sequence>  
          <attribute name="att" type="int"/>  
          <!-- xml:lang attribute is defined in the sys.sys collection   
               and can be referenced in any user-defined schema -->  
          <attribute ref="xml:lang"/>  
      </complexType>  
    </element>  
 </schema>'  
GO  
 -- Cleanup  
DROP xml schema collection SC   
GO  
```  
  
 Você deve observar o seguinte:  
  
-   Não é possível modificar esquemas XML com esses namespaces em nenhuma coleção de esquema XML definida pelo usuário. Por exemplo, há uma falha na seguinte coleção de esquema XML porque ela está adicionando um componente ao namespace `sqltypes` protegido:  
  
    ```  
    CREATE XML SCHEMA COLLECTION SC AS '  
    <schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace    
        ="http://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
          <element name="root" type="string"/>  
    </schema>'  
    GO  
    ```  
  
-   Não é possível usar a coleção de esquema XML `sys` para digitar colunas, variáveis ou parâmetros `xml` . Por exemplo, o seguinte código retorna um erro:  
  
    ```  
    DECLARE @x xml (sys.sys)  
    ```  
  
-   Não há suporte para serialização desses esquemas internos. Por exemplo, o seguinte código retorna um erro:  
  
    ```  
    SELECT XML_SCHEMA_NAMESPACE(N'sys',N'sys')  
    GO  
    ```  
  
 O código a seguir é outro exemplo no qual uma coleção de esquema XML que usa o tipo `varchar` definido no namespace `sqltypes` é criada:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="myNS" xmlns:ns="myNS"  
        xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
   <import     
     namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
            <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
go  
```  
  
 Conforme mostrado a seguir, é possível criar uma variável `XML` com tipo, atribuir uma instância XML a ela e verificar se o valor do tipo do elemento <`root`> é de um tipo `varchar`.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "http://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
GO  
```  
  
 A expressão `instance of sqltypes:varchar?` retorna TRUE, porque o valor do elemento <`root`> é de um tipo derivado de **varchar** de acordo com o esquema associado à variável `@var`.  
  
## <a name="see-also"></a>Consulte Também  
 [Coleções de esquemas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
