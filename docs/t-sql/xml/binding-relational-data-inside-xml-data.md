---
title: Associando dados relacionais dentro de dados XML | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: db924e662687ab79d207fe3e1e33ccc75aecd059
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="binding-relational-data-inside-xml-data"></a>Associando dados relacionais dentro de dados XML
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifique [Métodos de Tipo de Dados xml](../../t-sql/xml/xml-data-type-methods.md) em uma variável ou coluna de tipo de dados **xml**. Por exemplo, o [Método query&#40;&#41; &#40;tipo de dados xml&#41;](../../t-sql/xml/query-method-xml-data-type.md) executa o XQuery especificado em uma instância XML. Quando você cria um XML dessa maneira, é recomendável utilizar um valor de uma coluna que não seja do tipo XML ou uma variável Transact-SQL. Esse processo refere-se à associação de dados relacionais dentro do XML.  
  
 Para associar os dados relacionais de um não XML dentro do XML, o Mecanismo de Banco de Dados do SQL Server fornece as seguintes pseudofunções:  
  
-   [Função sql:column&#40;&#41; &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-column.md) Permite usar os valores de uma coluna relacional na expressão XQuery ou XML DML.  
  
-   [Função sql:variable&#40;&#41; &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-variable.md). Permite usar o valor de uma variável SQL variável na expressão XML DML ou XQuery.  
  
 Use essas funções com métodos de tipo de dados **xml** sempre que desejar expor um valor relacional dentro do XML.  
  
 Não é possível usar essas funções para referenciar dados em colunas ou variáveis dos tipos **xml**, tipos CLR definidos pelo usuário, datetime, smalldatetime, **text**, **ntext**, **sql_variant** e **image**.  
  
 Além disso, essa associação destina-se apenas a finalidades somente leitura. Isto é, você não pode gravar dados em colunas que usam essas funções. Por exemplo, sql:variable("@x")="*some expression"* não é permitido.  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>Exemplo: Consulta entre domínios que usam sql:variable ()  
 Este exemplo mostra como **sql:variable()** pode permitir que um aplicativo parametrize uma consulta. O ISBN é passado usando uma variável SQL @isbn. Substituindo a constante por **sql:variable()**, a consulta pode ser usada para pesquisar qualquer ISBN e não apenas aquele cujo ISBN é 0-7356-1588-2.  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **sql:column()** pode ser usado de maneira semelhante e oferece outros benefícios. Os índices sobre a coluna podem ser usados para eficiência, conforme decidido pelo otimizador de consulta baseado no custo. Além disso, a coluna computada pode armazenar uma propriedade promovida.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos de Tipos de Dados XML](../../t-sql/xml/xml-data-type-methods.md)  
  
  
