---
description: Associando dados relacionais dentro de dados XML
title: Associando dados relacionais dentro de dados XML
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 519f0cb9e198e86705d412af20d9d939365ee834
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88356162"
---
# <a name="binding-relational-data-inside-xml-data"></a>Associando dados relacionais dentro de dados XML
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Especifique [Métodos de Tipo de Dados xml](../../t-sql/xml/xml-data-type-methods.md) em uma variável ou coluna de tipo de dados **xml**. Por exemplo, o [Método query&#40;&#41; &#40;tipo de dados xml&#41;](../../t-sql/xml/query-method-xml-data-type.md) executa o XQuery especificado em uma instância XML. Quando você cria um XML dessa maneira, é recomendável utilizar um valor de uma coluna que não seja do tipo XML ou uma variável Transact-SQL. Esse processo refere-se à associação de dados relacionais dentro do XML.  
  
 Para associar os dados relacionais de um não XML dentro do XML, o Mecanismo de Banco de Dados do SQL Server fornece as seguintes pseudofunções:  
  
-   [Função sql:column&#40;&#41; &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-column.md) Permite usar os valores de uma coluna relacional na expressão XQuery ou XML DML.  
  
-   [Função sql:variable&#40;&#41; &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-variable.md). Permite usar o valor de uma variável SQL variável na expressão XML DML ou XQuery.  
  
 Use essas funções com métodos de tipo de dados **xml** sempre que desejar expor um valor relacional dentro do XML.  
  
 Não é possível usar essas funções para referenciar dados em colunas ou variáveis dos tipos **xml**, tipos CLR definidos pelo usuário, datetime, smalldatetime, **text**, **ntext**, **sql_variant** e **image**.  
  
 Além disso, essa associação destina-se apenas a finalidades somente leitura. Isto é, você não pode gravar dados em colunas que usam essas funções. Por exemplo, sql:variable ("\@x") = "*alguma expressão"* não é permitido.  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>Exemplo: Consulta entre domínios que usam sql:variable()  
 Este exemplo mostra como **sql:variable()** pode permitir que um aplicativo parametrize uma consulta. O ISBN é passado usando uma variável SQL @isbn. Substituindo a constante por **sql:variable()** , a consulta pode ser usada para pesquisar qualquer ISBN e não apenas aquele cujo ISBN é 0-7356-1588-2.  
  
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
  
  
