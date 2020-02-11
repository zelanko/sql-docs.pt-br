---
title: Usar funções de conversão em consultas XPath (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit conversion functions [SQLXML]
- string function
- number function
- XPath queries [SQLXML], explicit conversion functions
ms.assetid: 1111cb5d-2bd9-4bdb-8de2-dc0e47452dd6
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 58611edabcfeaeb9a97de3da6c7305fb169c14ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75252561"
---
# <a name="specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-40"></a>Especificando funções de conversão explícitas em consultas XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Os seguintes exemplos mostram como funções de conversão explícitas são especificadas em consultas XPath. As consultas XPath nesses exemplos são especificadas com relação ao esquema de mapeamento contido em SampleSchema1.xml. Para obter informações sobre este esquema de exemplo, consulte [exemplo de esquema XSD anotado para exemplos de XPath &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-use-the-number-explicit-conversion-function"></a>a. Use a função de conversão explícita number()  
 A função **Number ()** converte um argumento em um número.  
  
 Supondo que o valor de **ContactID** seja não numérico, a consulta a seguir converte **ContactID** em um número e o compara com o valor 4. Em seguida, a consulta ** \<** retorna todos os elementos filho de>de funcionários do nó de contexto com o atributo **ContactID** que tem um valor numérico de 4:  
  
```  
/child::Contact[number(attribute::ContactID)= 4]  
```  
  
 Um atalho para o eixo de **atributo** (@) pode ser especificado e, como o eixo **filho** é o padrão, ele pode ser omitido da consulta:  
  
```  
/Contact[number(@ContactID) = 4]  
```  
  
 Em termos relacionais, a consulta retorna um funcionário com um **ContactID** de 4.  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para testar a consulta XPath com relação ao esquema de mapeamento  
  
1.  Copie o [código do esquema de exemplo](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e cole-o em um arquivo de texto. Salve o arquivo como SampleSchema1.xml.  
  
2.  Crie o seguinte modelo (ExplicitConversionA.xml) e salve-o no diretório onde SampleSchema1.xml foi salvo.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Contact[number(@ContactID)=4]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho do diretório especificado para o esquema de mapeamento (SampleSchema1.xml) é relativo ao diretório em que o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 O conjunto de resultados da execução do modelo é:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
### <a name="b-use-the-string-explicit-conversion-function"></a>B. Use a função de conversão explícita string()  
 A função **String ()** converte um argumento em uma cadeia de caracteres.  
  
 A consulta a seguir converte **ContactID** em uma cadeia de caracteres e a compara com o valor de cadeia de caracteres "4". A consulta retorna todos ** \<** os elementos de>do funcionário do nó de contexto com um **ContactID** com um valor de cadeia de caracteres de "4":  
  
```  
/child::Contact[string(attribute::ContactID)="4"]  
```  
  
 Um atalho para o eixo de **atributo** (@) pode ser especificado e, como o eixo **filho** é o padrão, ele pode ser omitido da consulta:  
  
```  
/Contact[string(@ContactID)="4"]  
```  
  
 Funcionalmente, essa consulta retorna os mesmos resultados da consulta de exemplo anterior, ainda que a avaliação seja feita em relação ao valor de uma cadeia de caracteres, e não um valor numérico (ou seja, o número 4).  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para testar a consulta XPath com relação ao esquema de mapeamento  
  
1.  Copie o [código do esquema de exemplo](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e cole-o em um arquivo de texto. Salve o arquivo como SampleSchema1.xml.  
  
2.  Crie o seguinte modelo (ExplicitConversionB.xml) e salve-o no diretório onde SampleSchema1.xml foi salvo.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Contact[string(@ContactID)="4"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho do diretório especificado para o esquema de mapeamento (SampleSchema1.xml) é relativo ao diretório em que o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Aqui está o conjunto de resultados da execução do modelo:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
  
