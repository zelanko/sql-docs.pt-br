---
title: Gramática mínima do SQL | Microsoft Docs
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
ms.openlocfilehash: 85b1f59efd809c604458bd7b99882705db240e9a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057013"
---
# <a name="sql-minimum-grammar"></a>Gramática SQL mínima
Esta seção descreve a sintaxe SQL mínima para a qual um driver ODBC deve dar suporte. A sintaxe descrita nesta seção é um subconjunto da sintaxe de nível de entrada do SQL-92.  
  
 Um aplicativo pode usar qualquer uma das sintaxes nesta seção e ter certeza de que qualquer driver compatível com ODBC dará suporte a essa sintaxe. Para determinar se há suporte para os recursos adicionais do SQL-92 que não estão nesta seção, o aplicativo deve chamar **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Mesmo que o driver não esteja em conformidade com qualquer nível de conformidade do SQL-92, um aplicativo ainda poderá usar a sintaxe descrita nesta seção. Se um driver estiver em conformidade com um nível do SQL-92, por outro lado, ele dará suporte a toda a sintaxe incluída nesse nível. Isso inclui a sintaxe nesta seção porque a gramática mínima descrita aqui é um subconjunto puro do nível de conformidade do SQL-92 mais baixo. Depois que o aplicativo conhece o nível do SQL-92 com suporte, ele pode determinar se há suporte para um recurso de nível superior (se houver) chamando **SQLGetInfo** com o tipo de informações individual correspondente a esse recurso.  
  
 Os drivers que funcionam apenas com fontes de dados somente leitura podem não dar suporte a essas partes da gramática incluídas nesta seção que lidam com dados em alteração. Um aplicativo pode determinar se uma fonte de dados é somente leitura chamando **SQLGetInfo** com o tipo de informação SQL_DATA_SOURCE_READ_ONLY.  
  
## <a name="statement"></a>de  
 *criar tabela-instrução* :: =  
  
 *Nome da tabela de base* CREATE TABLE  
  
 (*tipo de dados de identificador de coluna* [*, tipo de dados de identificador de coluna*]...)  
  
> [!IMPORTANT]  
>  Como um *tipo de dados* em uma *instrução CREATE-TABLE-*, os aplicativos devem usar um tipo de dados da coluna type_name do conjunto de resultados retornado por **SQLGetTypeInfo**.  
  
 *delete-Statement-pesquised* :: =  
  
 EXCLUIR do *table-name* [em que *Search-Condition*]  
  
 *instrução DROP-TABLE-Statement* :: =  
  
 REMOVER tabela *base – nome da tabela*  
  
 *instrução INSERT* :: =  
  
 INSERIR em *table-name* [( *coluna-identificador* [, *coluna-identificador*]...)]      VALORES (*Inserir-valor*[, *Inserir valor*]...)  
  
 *Select-instrução* :: =  
  
 SELECT [todos os &#124; DISTINTOs] *Select-List*  
  
 Da *lista de referência de tabela*  
  
 [Onde *condição de pesquisa*]  
  
 [*ordem por cláusula*]  
  
 *instrução* :: = *CREATE-TABLE-Statement*  
  
 &#124; *delete-Statement-pesquised*  
  
 &#124; a *instrução DROP-TABLE*  
  
 &#124; *instrução INSERT*  
  
 *Instrução SELECT-* &#124;  
  
 &#124; *Update-Statement-pesquisado*  
  
 *Update-Statement-pesquised*  
  
 ATUALIZAR *tabela-nome*  
  
 DEFINIR *coluna-identificador* = {*expressão* &#124; NULL}  
  
 [, *coluna-Identifier* = {*expressão* &#124; NULL}]...  
  
 [Onde *condição de pesquisa*]  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Elementos usados em instruções SQL](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Suporte do tipo de dados](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Tipos de dados do parâmetro](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Marcadores de parâmetro](../../../odbc/reference/appendixes/parameter-markers.md)
