---
title: Gramática SQL mínima | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3e31f53abf8d8788f719adc9e00e180ca7aa96f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-minimum-grammar"></a>Gramática SQL mínima
Esta seção descreve a sintaxe SQL mínima que deve dar suporte a um driver ODBC. A sintaxe descrita nesta seção é um subconjunto da sintaxe de nível de entrada do SQL-92.  
  
 Um aplicativo pode usar qualquer da sintaxe nesta seção e ter certeza de que nenhum driver compatível com ODBC serão compatíveis com essa sintaxe. Para determinar se os recursos adicionais do SQL-92, não nesta seção têm suporte, o aplicativo deve chamar **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Mesmo que o driver não está de acordo com qualquer nível de conformidade de SQL-92, um aplicativo ainda pode usar a sintaxe descrita nesta seção. Se um driver compatível com um nível de SQL-92, por outro lado, ele dá suporte a toda a sintaxe incluída nesse nível. Isso inclui a sintaxe desta seção porque a gramática mínima descrita aqui é um subconjunto puro do nível mais baixo de conformidade do SQL-92. Depois que o aplicativo saiba que o nível de SQL-92 com suporte, ele pode determinar se um recurso de nível mais alto é suportado (se houver) chamando **SQLGetInfo** com o tipo de informações individuais correspondente a esse recurso.  
  
 Drivers que funcionam apenas com fontes de dados somente leitura podem não oferecer suporte a essas partes da gramática incluídos nesta seção que lidam com dados de alteração. Um aplicativo pode determinar se uma fonte de dados é somente leitura chamando **SQLGetInfo** com o tipo de informação SQL_DATA_SOURCE_READ_ONLY.  
  
## <a name="statement"></a>de  
 *instrução CREATE de tabela* :: =  
  
 CREATE TABLE *nome da tabela de base*  
  
 (*tipo de dados da coluna de identificador* [*, tipo de dados da coluna de identificador*]...)  
  
> [!IMPORTANT]  
>  Como um *tipo de dados* em uma *criar tabela-instrução*, aplicativos devem usar um tipo de dados da coluna de TYPE_NAME do conjunto de resultados retornado por **SQLGetTypeInfo**.  
  
 *pesquisa de instrução de exclusão* :: =  
  
 DELETE FROM *nome de tabela* [onde *critério de pesquisa*]  
  
 *instrução drop-table* :: =  
  
 DROP TABLE *nome da tabela de base*  
  
 *instrução INSERT* :: =  
  
 INSERT INTO *nome de tabela* [( *identificador de coluna* [, *identificador de coluna*]...)]      VALORES (*Inserir valor*[, *Inserir valor*]...)  
  
 *instrução Select* :: =  
  
 Selecione [todos os &#124; DISTINCT] *lista de select*  
  
 DE *lista de referências de tabela*  
  
 [Onde *critério de pesquisa*]  
  
 [*ordem por cláusula*]  
  
 *instrução* :: = *instrução create de tabela*  
  
 &#124;*pesquisados de instrução de exclusão*  
  
 &#124;*descarte de tabela de instrução*  
  
 &#124;*instrução insert*  
  
 &#124;*instrução select*  
  
 &#124;*pesquisados de instrução de atualização*  
  
 *pesquisa de instrução de atualização*  
  
 ATUALIZAÇÃO *nome de tabela*  
  
 DEFINIR *identificador de coluna* = {*expressão* &#124; nulo}  
  
 [, *identificador de coluna* = {*expressão* &#124; nulo}]...  
  
 [Onde *critério de pesquisa*]  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Elementos usados em instruções SQL](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Suporte do tipo de dados](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Tipos de dados do parâmetro](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Marcadores de parâmetro](../../../odbc/reference/appendixes/parameter-markers.md)
