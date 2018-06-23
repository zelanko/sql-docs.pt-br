---
title: Especificando funções de conversão explícitas em consultas XPath (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- explicit conversion functions [SQLXML]
- string function
- number function
- XPath queries [SQLXML], explicit conversion functions
ms.assetid: 1111cb5d-2bd9-4bdb-8de2-dc0e47452dd6
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 59a2a54b1a3fe7a8136fa2ab0cb56f4cd215c245
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013064"
---
# <a name="specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-40"></a>Especificando funções de conversão explícitas em consultas XPath (SQLXML 4.0)
  Os seguintes exemplos mostram como funções de conversão explícitas são especificadas em consultas XPath. As consultas XPath nesses exemplos são especificadas com relação ao esquema de mapeamento contido em SampleSchema1.xml. Para obter informações sobre esse esquema de exemplo, consulte [anotado de exemplo de esquema XSD para obter exemplos de XPath &#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-use-the-number-explicit-conversion-function"></a>A. Use a função de conversão explícita number()  
 A função `number()` converte um argumento em um número.  
  
 Supondo que o valor de **ContactID** não for numérico, a seguinte consulta converte **ContactID** para um número e o compara com o valor 4. A consulta retorna todos os  **\<funcionário >** elementos filhos do nó de contexto com o **ContactID** atributo que tem um valor numérico de 4:  
  
```  
/child::Contact[number(attribute::ContactID)= 4]  
```  
  
 Um atalho para o `attribute` eixo (@) podem ser especificados e porque o `child` eixo é o padrão, ele pode ser omitido da consulta:  
  
```  
/Contact[number(@ContactID) = 4]  
```  
  
 Em termos relacionais, a consulta retorna um funcionário com um **ContactID** de 4.  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para testar a consulta XPath com relação ao esquema de mapeamento  
  
1.  Copie o [código de esquema de exemplo](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e cole-o em um arquivo de texto. Salve o arquivo como SampleSchema1.xml.  
  
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
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 O conjunto de resultados da execução do modelo é:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
### <a name="b-use-the-string-explicit-conversion-function"></a>B. Use a função de conversão explícita string()  
 A função `string()` converte um argumento em uma cadeia de caracteres.  
  
 A seguinte consulta converte **ContactID** para uma cadeia de caracteres e compara-o com a cadeia de caracteres de valor "4". A consulta retorna todos os  **\<funcionário >** elementos filhos do nó de contexto com um **ContactID** com um valor de cadeia de caracteres de "4":  
  
```  
/child::Contact[string(attribute::ContactID)="4"]  
```  
  
 Um atalho para o `attribute` eixo (@) podem ser especificados e porque o `child` eixo é o padrão, ele pode ser omitido da consulta:  
  
```  
/Contact[string(@ContactID)="4"]  
```  
  
 Funcionalmente, essa consulta retorna os mesmos resultados da consulta de exemplo anterior, ainda que a avaliação seja feita em relação ao valor de uma cadeia de caracteres, e não um valor numérico (ou seja, o número 4).  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para testar a consulta XPath com relação ao esquema de mapeamento  
  
1.  Copie o [código de esquema de exemplo](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e cole-o em um arquivo de texto. Salve o arquivo como SampleSchema1.xml.  
  
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
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Aqui está o conjunto de resultados da execução do modelo:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
  