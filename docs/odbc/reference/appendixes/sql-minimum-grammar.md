---
title: Gramática SQL mínima | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26cf76200010edae7f85993ec33eb3722f35e94e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270494"
---
# <a name="sql-minimum-grammar"></a>Gramática SQL mínima
Esta seção descreve a sintaxe SQL mínima que deve dar suporte a um driver ODBC. A sintaxe descrita nesta seção é um subconjunto da sintaxe de nível de entrada do SQL-92.  
  
 Um aplicativo pode usar qualquer um da sintaxe nesta seção e ter certeza de que nenhum driver compatível com ODBC será compatível com essa sintaxe. Para determinar se os recursos adicionais do SQL-92 não nesta seção têm suporte, o aplicativo deve chamar **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Mesmo se o driver não está em conformidade com qualquer nível de compatibilidade do SQL-92, um aplicativo ainda pode usar a sintaxe descrita nesta seção. Se um driver está de acordo com um nível de SQL-92, por outro lado, ele dá suporte a toda a sintaxe incluída nesse nível. Isso inclui a sintaxe nesta seção, porque a gramática mínima descrita aqui é um subconjunto puro de nível mais baixo de conformidade do SQL-92. Depois que o aplicativo sabe que o nível de SQL-92 com suporte, ele pode determinar se um recurso de nível superior tem suporte (se houver), chamando **SQLGetInfo** com o tipo de informação individuais correspondente a esse recurso.  
  
 Drivers que funcionam somente com fontes de dados somente leitura podem não oferecer suporte a essas partes da gramática incluídos nesta seção que lidam com dados de alteração. Um aplicativo pode determinar se uma fonte de dados é somente leitura, chamando **SQLGetInfo** com o tipo de informação SQL_DATA_SOURCE_READ_ONLY.  
  
## <a name="statement"></a>de  
 *create-table-statement* ::=  
  
 CREATE TABLE *nome da tabela de base*  
  
 (*tipo de dados da coluna identificador* [ *, tipo de dados da coluna identificador*]...)  
  
> [!IMPORTANT]  
>  Como uma *tipo de dados* em um *-instrução create table*, aplicativos devem usar um tipo de dados da coluna de TYPE_NAME do conjunto de resultados retornado pela **SQLGetTypeInfo**.  
  
 *delete-statement-searched* ::=  
  
 DELETE FROM *table-name* [WHERE *search-condition*]  
  
 *drop-table-statement* ::=  
  
 DROP TABLE *nome da tabela de base*  
  
 *insert-statement* ::=  
  
 INSERT INTO *nome da tabela* [( *identificador de coluna* [, *identificador de coluna*]...)]      VALORES (*valor de inserção*[, *Inserir valor*]...)  
  
 *select-statement* ::=  
  
 SELECT [ALL &#124; DISTINCT] *select-list*  
  
 FROM *table-reference-list*  
  
 [Onde *critério de pesquisa*]  
  
 [*order-by-clause*]  
  
 *statement* ::= *create-table-statement*  
  
 &#124; *delete-statement-searched*  
  
 &#124; *drop-table-statement*  
  
 &#124; *insert-statement*  
  
 &#124; *select-statement*  
  
 &#124; *update-statement-searched*  
  
 *update-statement-searched*  
  
 UPDATE *table-name*  
  
 SET *column-identifier* = {*expression* &#124; NULL }  
  
 [, *column-identifier* = {*expression* &#124; NULL}]...  
  
 [Onde *critério de pesquisa*]  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Elementos usados em instruções SQL](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Suporte do tipo de dados](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Tipos de dados do parâmetro](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Marcadores de parâmetro](../../../odbc/reference/appendixes/parameter-markers.md)
