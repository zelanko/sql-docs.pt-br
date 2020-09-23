---
description: Diretrizes para usar métodos de tipo de dados xml
title: Diretrizes para usar métodos de tipo de dados xml
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: 1a483aa1-42de-4c88-a4b8-c518def3d496
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8a429071f406be0309d89bbb9ea0253b86905a8
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91112317"
---
# <a name="guidelines-for-using-xml-data-type-methods"></a>Diretrizes para usar métodos de tipo de dados xml

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este tópico descreve as diretrizes de uso dos métodos de tipo de dados **xml**.

## <a name="the-print-statement"></a>A instrução PRINT

Os métodos de tipo de dados **xml** não podem ser usados na instrução PRINT como mostra o exemplo a seguir. Os métodos de tipo de dados **xml** são tratados como subconsultas, que não são permitidas na instrução PRINT. Como resultado, o exemplo seguinte retorna um erro:

```sql
DECLARE @x XML
SET @x = '<root>Hello</root>'
PRINT @x.value('/root[1]', 'varchar(20)') -- will not work because this is treated as a subquery (select top 1 col from table)
```

Uma das soluções é primeiramente atribuir o resultado do método **value()** a uma variável do tipo **xml** e, em seguida, especificar a variável na consulta.

```sql
DECLARE @x XML
DECLARE @c VARCHAR(max)
SET @x = '<root>Hello</root>'
SET @c = @x.value('/root[1]', 'VARCHAR(11)')
PRINT @c
```

## <a name="the-group-by-clause"></a>A Cláusula GROUP BY

Os métodos de tipo de dados **xml** são tratados internamente como subconsultas. Como GROUP BY exige um escalar e não permite agregações e subconsultas, não é possível especificar os métodos de tipo de dados **xml** na cláusula GROUP BY. Uma solução é chamar uma função definida pelo usuário que usa métodos XML internamente.

## <a name="reporting-errors"></a>Relatório de erros

Ao relatar erros, os métodos de tipo de dados **xml** geram um único erro no seguinte formato:

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

As etapas de local, os parâmetros de função e os operadores que exigem singletons retornarão um erro se o compilador não puder determinar se um singleton está garantido no momento da execução. Este problema costuma acontecer com dados não digitados. Por exemplo, a pesquisa de um atributo requer um elemento pai de singleton. Um ordinal que selecione um único nó pai é suficiente. A avaliação de uma combinação **node()** -**value()** para extrair valores de atributo pode não exigir a especificação ordinal. Isso é demonstrado no próximo exemplo.

### <a name="example-known-singleton"></a>Exemplo: singleton conhecido

Neste exemplo, o método **nodes()** gera uma linha separada para cada elemento `<book>`. O método **value()** , avaliado em um nó `<book>`, extrai o valor de `@genre` e, sendo um atributo, é um singleton.

```sql
SELECT nref.value('@genre', 'VARCHAR(max)') LastName
FROM T CROSS APPLY xCol.nodes('//book') AS R(nref)
```

O esquema de XML é usado para verificação de tipo de XML digitado. Se um nó é especificado como um singleton no esquema XML, o compilador usa essa informação e não ocorre nenhum erro. Caso contrário, um ordinal que selecione um único nó é obrigatório. Particularmente, o uso de eixo descendente ou independente (//), como em `/book//title`, desobriga a inferência de cardinalidade singleton para o elemento `<title>`, ainda que o esquema XML o especifique dessa forma. Portanto, você deve reescrevê-lo como `(/book//title)[1]`.

É importante ficar atento à diferença entre `//first-name[1]` e `(//first-name)[1]` para a verificação de tipo. O primeiro retorna uma sequência de nós `<first-name>`, em que cada nó é o nó `<first-name>` na extremidade mais à esquerda entre seus irmãos. O segundo retorna o primeiro nó singleton `<first-name>` em ordem de documento na instância de XML.

### <a name="example-using-value"></a>Exemplo: usando value()

A seguinte consulta em uma coluna XML não tipada resulta em um erro estático e de compilação. Isso ocorre porque **value()** espera um nó singleton como o primeiro argumento e o compilador não pode determinar se apenas um nó de `<last-name>` ocorrerá em tempo de execução:

```sql
SELECT xCol.value('//author/last-name', 'NVARCHAR(50)') LastName
FROM T
```

A seguir temos uma solução a ser considerada:

```sql
SELECT xCol.value('//author/last-name[1]', 'NVARCHAR(50)') LastName
FROM T
```

Porém, a solução não resolve o erro, porque é possível a ocorrência de múltiplos nós `<author>` em cada instância de XML. A nova gravação a seguir funciona:

```sql
SELECT xCol.value('(//author/last-name/text())[1]', 'NVARCHAR(50)') LastName
FROM T
```

Esta consulta retorna o valor do primeiro elemento `<last-name>` em cada instância de XML.

## <a name="see-also"></a>Consulte Também

- [Métodos de Tipos de Dados XML](../../t-sql/xml/xml-data-type-methods.md)
