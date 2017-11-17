---
title: "Diretrizes para usar os métodos de tipo de dados xml | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: 1a483aa1-42de-4c88-a4b8-c518def3d496
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e02d385d699c1c26d44f2e7383584416c2d9dd5c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="guidelines-for-using-xml-data-type-methods"></a>Diretrizes para usar métodos de tipo de dados xml
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve as diretrizes para usar o **xml** métodos de tipo de dados.  
  
## <a name="the-print-statement"></a>A instrução PRINT  
 O **xml** métodos de tipo de dados não podem ser usados na instrução PRINT, conforme mostrado no exemplo a seguir. O **xml** métodos de tipo de dados são tratados como subconsultas e subconsultas não são permitidas na instrução PRINT. Como resultado, o exemplo seguinte retorna um erro:  
  
```  
DECLARE @x xml  
SET @x = '<root>Hello</root>'  
PRINT @x.value('/root[1]', 'varchar(20)') -- will not work because this is treated as a subquery (select top 1 col from table)   
```  
  
 Uma solução é primeiramente atribuir o resultado da **Value ()** método para uma variável de **xml** digite e, em seguida, especifique a variável na consulta.  
  
```  
DECLARE @x xml  
DECLARE @c varchar(max)  
SET @x = '<root>Hello</root>'  
SET @c = @x.value('/root[1]', 'varchar(11)')  
PRINT @c                                                        
```  
  
## <a name="the-group-by-clause"></a>A Cláusula GROUP BY  
 O **xml** métodos de tipo de dados são tratados internamente como subconsultas. Como GROUP BY exige um valor escalar e não permite agregações e subconsultas, não é possível especificar o **xml** métodos de tipo de dados na cláusula GROUP BY. Uma solução é chamar uma função definida pelo usuário que usa métodos XML internamente.  
  
## <a name="reporting-errors"></a>Relatório de erros  
 Quando o relatório de erros, **xml** métodos de tipo de dados geram um único erro no seguinte formato:  
  
```  
Msg errorNumber, Level levelNumber, State stateNumber:  
XQuery [database.table.method]: description_of_error  
```  
  
 Por exemplo:  
  
```  
Msg 2396, Level 16, State 1:  
XQuery [xmldb_test.xmlcol.query()]: Attribute may not appear outside of an element  
```  
  
## <a name="singleton-checks"></a>Verificações de singleton  
 As etapas de local, os parâmetros de função e os operadores que exigem singletons retornarão um erro se o compilador não puder determinar se um singleton está garantido no momento da execução. Este problema costuma acontecer com dados não digitados. Por exemplo, a pesquisa de um atributo requer um elemento pai de singleton. Um ordinal que selecione um único nó pai é suficiente. A avaliação de uma **Node ()**-**Value ()** combinação para extrair valores de atributo não pode requerer a especificação ordinal. Isso é demonstrado no próximo exemplo.  
  
### <a name="example-known-singleton"></a>Exemplo: Singleton conhecido  
 Neste exemplo, o **Nodes ()** método gera uma linha separada para cada <`book`> elemento. O **Value ()** método que é avaliado em um <`book`> nó extrai o valor de @genre e, sendo um atributo é um singleton.  
  
```  
SELECT nref.value('@genre', 'varchar(max)') LastName  
FROM   T CROSS APPLY xCol.nodes('//book') AS R(nref)  
```  
  
 O esquema de XML é usado para verificação de tipo de XML digitado. Se um nó é especificado como um singleton no esquema XML, o compilador usa essa informação e não ocorre nenhum erro. Caso contrário, um ordinal que selecione um único nó é obrigatório. Em particular, o uso de eixo descendente ou independente (/ /) eixo, como em/livro / / título, desobriga a inferência de cardinalidade de singleton para o \<título > elemento, mesmo se o esquema XML especifica dessa forma. Portanto, você deve reescrevê-lo como (/livro//título)[1].  
  
 É importante ficar atento à diferença entre //nome[1] e (//nome)[1] para a verificação de tipo. O primeiro retorna uma sequência de \<-nome > nós em que cada nó é o mais à esquerda \<-nome > nó entre seus irmãos. O segundo retorna o primeiro singleton \<-nome > nó na ordem do documento na instância XML.  
  
### <a name="example-using-value"></a>Exemplo: Usando value()  
 A consulta a seguir em uma coluna XML não digitada resulta em um erro de compilação estático. Isso ocorre porque **Value ()** espera um nó de singleton, como o primeiro argumento e o compilador não pode determinar se apenas um \<sobrenome > nó ocorrerá em tempo de execução:  
  
```  
SELECT xCol.value('//author/last-name', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 A seguir temos uma solução a ser considerada:  
  
```  
SELECT xCol.value('//author/last-name[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 Porém, a solução não resolve o erro, porque é possível a ocorrência de múltiplos nós <`author`> em cada instância de XML. A nova gravação a seguir funciona:  
  
```  
SELECT xCol.value('(//author/last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 Esta consulta retorna o valor do primeiro elemento `<last-name>` em cada instância de XML.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos de Tipos de Dados XML](../../t-sql/xml/xml-data-type-methods.md)  
  
  

