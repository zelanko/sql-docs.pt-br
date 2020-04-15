---
title: Gramática Mínima SQL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20eee34feadb8e3140f25019ec6b0d036ff02e14
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304987"
---
# <a name="sql-minimum-grammar"></a>Gramática SQL mínima
Esta seção descreve a sintaxe SQL mínima que um driver ODBC deve suportar. A sintaxe descrita nesta seção é um subconjunto da sintaxe de nível de entrada de SQL-92.  
  
 Um aplicativo pode usar qualquer sintaxe nesta seção e ter certeza de que qualquer driver compatível com ODBC suportará essa sintaxe. Para determinar se os recursos adicionais do SQL-92 que não estão nesta seção são suportados, o aplicativo deve ligar para **o SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Mesmo que o driver não esteja de acordo com qualquer nível de conformidade SQL-92, um aplicativo ainda pode usar a sintaxe descrita nesta seção. Se um driver estiver em conformidade com um nível SQL-92, por outro lado, ele suporta toda a sintaxe incluída nesse nível. Isso inclui a sintaxe nesta seção porque a gramática mínima descrita aqui é um subconjunto puro do nível de conformidade SQL-92 mais baixo. Uma vez que o aplicativo conhece o nível SQL-92 suportado, ele pode determinar se um recurso de nível superior é suportado (se houver) ligando para **o SQLGetInfo** com o tipo de informação individual correspondente a esse recurso.  
  
 Os drivers que trabalham apenas com fontes de dados somente leitura podem não suportar as partes da gramática incluídas nesta seção que lidam com a alteração de dados. Um aplicativo pode determinar se uma fonte de dados é somente leitura ligando para **o SQLGetInfo** com o SQL_DATA_SOURCE_READ_ONLY tipo de informação.  
  
## <a name="statement"></a>de  
 *declaração de tabela de criação* ::=  
  
 CRIAR *TABELA nome de tabela-base*  
  
 (tipo*de dados identificador de colunas* *[,tipo de dados identificador de*coluna]...)  
  
> [!IMPORTANT]  
>  Como um *tipo de dados* em uma *declaração de tabela de criação,* os aplicativos devem usar um tipo de dados da coluna TYPE_NAME do conjunto de resultados retornado pelo **SQLGetTypeInfo**.  
  
 *pesquisado por declaração de exclusão* ::=  
  
 EXCLUA do *nome da tabela* [ONDE a condição de *pesquisa]*  
  
 *drop-table-statement* ::=  
  
 NOME *da tabela de base* DROP TABLE  
  
 *inserção-instrução* ::=  
  
 INSIRA NO *nome da tabela* [(identificador de *coluna* [, *identificador de coluna*]...)]      VALORES *(valor de inserção*[, *valor de inserção*]... )  
  
 *select-statement* ::=  
  
 Selecionar a lista *de seleção* de [TODOS &#124; DISTINTOs]  
  
 DA *lista de referência da tabela*  
  
 [ONDE *condição de pesquisa]*  
  
 [*ordem por cláusula*]  
  
 *declaração* ::= *declaração de criação de tabela*  
  
 &#124; *pesquisado por declaração de exclusão*  
  
 &#124; *declaração de tabela de queda*  
  
 &#124; *inserção-instrução*  
  
 &#124; *declaração de seleção*  
  
 &#124; *pesquisado em declaração de atualização*  
  
 *atualização-declaração pesquisada*  
  
 ATUALIZAR *nome da tabela*  
  
 Identificador *de coluna* SET = {*expressão* &#124; NULL }  
  
 [, *foto-identificador =* {*expressão* &#124; NULL}]...  
  
 [ONDE *condição de pesquisa]*  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Elementos usados em instruções SQL](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Suporte ao tipo de dados](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Tipos de dados do parâmetro](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Marcadores de parâmetro](../../../odbc/reference/appendixes/parameter-markers.md)
