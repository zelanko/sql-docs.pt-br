---
title: Suporte a SQLGetInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a21c035a14814f51d4344894ef253b2cc844f4c2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307797"
---
# <a name="sqlgetinfo-support"></a>Suporte SQLGetInfo
Quando um ODBC 2. *x* o aplicativo chama **SQLGetInfo** para um driver ODBC 3 *. x* , os argumentos *InfoType* na tabela a seguir devem ter suporte.  
  
|*InfoType*|Retornos|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2,0) **Observação:** esse tipo de informação não é preterido; os bitmasks na coluna à direita são preteridos.|Um bitmask sqlinteiro que enumera as cláusulas na instrução **ALTER TABLE** com suporte da fonte de dados.<br /><br /> As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:<br /><br /> SQL_AT_DROP_COLUMN = há suporte para a capacidade de descartar colunas. Se isso resulta em cascata ou o comportamento restrito é definido pelo driver. (ODBC 2,0)<br /><br /> SQL_AT_ADD_COLUMN = há suporte para a capacidade de adicionar várias colunas em uma única instrução ALTER TABLE. Esse bit não é combinado com outros bits de SQL_AT_ADD_COLUMN_XXX ou bits de SQL_AT_CONSTRAINT_XXX. (ODBC 2,0)|  
|SQL_FETCH_DIRECTION (ODBC 1,0)<br /><br /> O tipo de informação foi introduzido no ODBC 1,0; cada bitmask é rotulado com a versão na qual foi introduzido.|Um bitmask sqlinteiro que enumera as opções de direção de busca com suporte.<br /><br /> As seguintes bitmasks são usadas em conjunto com o sinalizador para determinar quais opções têm suporte:<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1,0) SQL_FD_FETCH_FIRST (ODBC 1,0) SQL_FD_FETCH_LAST (ODBC 1,0) SQL_FD_FETCH_PRIOR (ODBC 1,0) SQL_FD_FETCH_ABSOLUTE (ODBC 1,0) SQL_FD_FETCH_RELATIVE (ODBC 1,0) SQL_FD_FETCH_BOOKMARK (ODBC 2,0)|  
|SQL_LOCK_TYPES (ODBC 2,0)|Um bitmask sqlinteiro que enumera os tipos de bloqueio com suporte para o argumento *Flock* em **SQLSetPos**.<br /><br /> As seguintes bitmasks são usadas em conjunto com o sinalizador para determinar quais tipos de bloqueio têm suporte:<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1,0)|Um valor SQLSMALLINT que indica o nível de conformidade ODBC.<br /><br /> SQL_OAC_NONE = nenhum<br /><br /> SQL_OAC_LEVEL1 = nível 1 com suporte<br /><br /> SQL_OAC_LEVEL2 = nível 2 com suporte|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1,0)|Um valor SQLSMALLINT que indica a gramática SQL suportada pelo driver. Consulte o [Apêndice C: SQL Grammar](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) para obter uma definição de níveis de conformidade do SQL.<br /><br /> SQL_OSC_MINIMUM = suporte mínimo à gramática<br /><br /> SQL_OSC_CORE = suporte à gramática básica<br /><br /> SQL_OSC_EXTENDED = suporte à gramática estendida|  
|SQL_POS_OPERATIONS (ODBC 2,0)|Um bitmask sqlinteiro que enumera as operações com suporte no **SQLSetPos**.<br /><br /> As seguintes bitmasks são usadas em conjunto com o sinalizador para determinar quais opções têm suporte:<br /><br /> SQL_POS_POSITION (ODBC 2,0) SQL_POS_REFRESH (ODBC 2,0) SQL_POS_UPDATE (ODBC 2,0) SQL_POS_DELETE (ODBC 2,0) SQL_POS_ADD (ODBC 2,0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2,0)|Um bitmask sqlinteiro que enumera as instruções SQL posicionadas com suporte.<br /><br /> As seguintes bitmasks são usadas para determinar quais instruções têm suporte:<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1,0)|Um bitmask sqlinteiro que enumera as opções de controle de simultaneidade com suporte para o cursor.<br /><br /> As seguintes bitmasks são usadas para determinar quais opções têm suporte:<br /><br /> SQL_SCCO_READ_ONLY = o cursor é somente leitura. Nenhuma atualização é permitida.<br /><br /> SQL_SCCO_LOCK = o cursor usa o nível mais baixo de bloqueio suficiente para garantir que a linha possa ser atualizada.<br /><br /> SQL_SCCO_OPT_ROWVER = cursor usa controle de simultaneidade otimista, comparando versões de linha, como SQLBase ROWID ou Sybase TIMESTAMP.<br /><br /> SQL_SCCO_OPT_VALUES = cursor usa controle de simultaneidade otimista, comparando valores.|  
|SQL_STATIC_SENSITIVITY (ODBC 2,0)|Um bitmask sqlinteiro que enumera se as alterações feitas por um aplicativo em um cursor estático ou controlado por conjunto de chaves por meio de instruções **SQLSetPos** ou Update ou DELETE posicionadas podem ser detectadas por esse aplicativo.<br /><br /> SQL_SS_ADDITIONS = as linhas adicionadas são visíveis para o cursor; o cursor pode rolar para essas linhas. Onde essas linhas são adicionadas ao cursor depende do driver.<br /><br /> SQL_SS_DELETIONS = as linhas excluídas não estão mais disponíveis para o cursor e não deixam um "buraco" no conjunto de resultados; Depois que o cursor rolar de uma linha excluída, ele não poderá retornar a essa linha.<br /><br /> SQL_SS_UPDATES = atualizações para linhas são visíveis para o cursor; Se o cursor rolar de e retornar para uma linha atualizada, os dados retornados pelo cursor serão os dados atualizados, não os dados originais. Essa opção se aplica somente a cursores estáticos ou atualizações em cursores controlados por conjunto de chaves que não atualizam a chave. Essa opção não se aplica a um cursor dinâmico ou no caso em que uma chave é alterada em um cursor misto.<br /><br /> Se um aplicativo pode detectar alterações feitas no conjunto de resultados por outros usuários, incluindo outros cursores no mesmo aplicativo, depende do tipo de cursor.|  
  
 Um aplicativo ODBC*3. x* trabalhando com um driver ODBC*3. x* não deve chamar **SQLGetInfo** com os argumentos *InfoType* descritos na tabela anterior, mas deve usar os argumentos *InfoType* do ODBC 3 *. x* listados no parágrafo a seguir. Não há uma correspondência um-para-um entre os argumentos *InfoType* usados no ODBC 2. *x* e os usados no ODBC 3 *. x*. Um aplicativo ODBC 3 *. x* trabalhando com um ODBC 2. *x* Driver, por outro lado, deve usar os argumentos *InfoType* descritos anteriormente.  
  
 Alguns dos tipos de informações na tabela anterior foram preteridos em favor dos tipos de informações de atributos de cursor. Esses tipos de informações preteridos são SQL_FETCH_DIRECTION, SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY e SQL_STATIC_SENSITIVITY. Os novos tipos de atributos de cursor são SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2, em que XXX é igual a dinâmico, FORWARD_ONLY, KEYSET_DRIVEN ou estático. Cada um dos novos tipos indica os recursos do driver para um único tipo de cursor. Para obter mais informações sobre essas opções, consulte a descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .
