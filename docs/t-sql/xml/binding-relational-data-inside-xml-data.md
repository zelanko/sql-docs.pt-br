---
title: Associando dados relacionais dentro de dados XML | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef249a7482610419873604637290cab3ef18e34b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="binding-relational-data-inside-xml-data"></a>Associando dados relacionais dentro de dados XML
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Você pode especificar [métodos de tipo de dados xml](../../t-sql/xml/xml-data-type-methods.md) contra um **xml** variável ou coluna de tipo de dados. Por exemplo, o [consulta &#40; &#41; Método &#40; tipo de dados xml &#41; ](../../t-sql/xml/query-method-xml-data-type.md) executa o XQuery especificado em uma instância XML. Quando você cria um XML dessa maneira, é recomendável utilizar um valor de uma coluna que não seja do tipo XML ou uma variável Transact-SQL. Esse processo refere-se à associação de dados relacionais dentro do XML.  
  
 Para associar os dados relacionais de um não XML dentro do XML, o Mecanismo de Banco de Dados do SQL Server fornece as seguintes pseudofunções:  
  
-   [SQL: Column &#40; &#41; Função &#40; XQuery &#41; ](../../xquery/xquery-extension-functions-sql-column.md) Permite que você use os valores de uma coluna relacional na expressão XML DML ou XQuery.  
  
-   [SQL: Variable &#40; &#41; Função &#40; XQuery &#41; ](../../xquery/xquery-extension-functions-sql-variable.md) . Permite usar o valor de uma variável SQL variável na expressão XML DML ou XQuery.  
  
 Você pode usar essas funções com **xml** métodos de tipo de dados sempre que você deseja expor um valor relacional dentro do XML.  
  
 Você não pode usar essas funções para fazer referência a dados em colunas ou variáveis do **xml**, CLR definido pelo usuário tipos, datetime, smalldatetime, **texto**, **ntext**, **sql_variant**, e **imagem** tipos.  
  
 Além disso, essa associação destina-se apenas a finalidades somente leitura. Isto é, você não pode gravar dados em colunas que usam essas funções. Por exemplo, sql:variable("@x") = "*alguma expressão"* não é permitido.  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>Exemplo: Consulta entre domínios que usam sql:variable ()  
 Este exemplo mostra como **SQL: Variable** pode permitir que um aplicativo parametrizar uma consulta. O ISBN é passado usando uma variável SQL @isbn. Substituindo a constante com **SQL: Variable**, a consulta pode ser usada para pesquisar qualquer ISBN e não apenas aquele cujo ISBN é 0-7356-1588-2.  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **SQL: Column** pode ser usado de maneira semelhante e oferece benefícios adicionais. Os índices sobre a coluna podem ser usados para eficiência, conforme decidido pelo otimizador de consulta baseado no custo. Além disso, a coluna computada pode armazenar uma propriedade promovida.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos de Tipos de Dados XML](../../t-sql/xml/xml-data-type-methods.md)  
  
  
