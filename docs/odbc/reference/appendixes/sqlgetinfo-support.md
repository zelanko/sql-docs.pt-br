---
title: Suporte sqlgetinfo | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307797"
---
# <a name="sqlgetinfo-support"></a>Suporte SQLGetInfo
Quando um ODBC 2. *x* o aplicativo chama **SQLGetInfo** para um driver ODBC 3 *.x,* os argumentos *InfoType* na tabela a seguir devem ser suportados.  
  
|*Infotipo*|Retornos|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **Nota:** Este tipo de informação não é preterido; as máscaras de bit na coluna à direita são preteridas.|Uma máscara de bit SQLINTEGER enumerando as cláusulas na declaração **ALTER TABLE** suportada pela fonte de dados.<br /><br /> As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:<br /><br /> SQL_AT_DROP_COLUMN = A capacidade de soltar colunas é suportada. Se isso resulta em cascata ou comportamento restrito é definido pelo driver. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = A capacidade de adicionar várias colunas em uma única declaração ALTER TABLE é suportada. Este bit não combina com outros SQL_AT_ADD_COLUMN_XXX bits ou bits de SQL_AT_CONSTRAINT_XXX. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> O tipo de informação foi introduzido no ODBC 1.0; cada bitmask é rotulado com a versão em que foi introduzido.|Uma máscara de bit SQLINTEGER enumerando as opções de direção de busca suportadas.<br /><br /> As seguintes máscaras de bit são usadas em conjunto com o sinalizador para determinar quais opções são suportadas:<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|Uma máscara de bit SQLINTEGER enumerando os tipos de bloqueio suportados para o argumento *fLock* no **SQLSetPos**.<br /><br /> As seguintes máscaras de bit são usadas em conjunto com o sinalizador para determinar quais tipos de bloqueio são suportados:<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|Um valor SQLSMALLINT indicando o nível de conformidade ODBC.<br /><br /> SQL_OAC_NONE = Nenhum<br /><br /> SQL_OAC_LEVEL1 = Nível 1 suportado<br /><br /> SQL_OAC_LEVEL2 = Nível 2 suportado|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|Um valor SQLSMALLINT indicando gramática SQL suportada pelo driver. Consulte [o apêndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) para uma definição dos níveis de conformidade SQL.<br /><br /> SQL_OSC_MINIMUM = Gramática mínima suportada<br /><br /> SQL_OSC_CORE = Gramática do núcleo suportada<br /><br /> SQL_OSC_EXTENDED = Gramática estendida suportada|  
|SQL_POS_OPERATIONS (ODBC 2.0)|Uma máscara de bit SQLINTEGER enumerando as operações suportadas em **SQLSetPos**.<br /><br /> As seguintes máscaras de bit são usadas em conjunto com o sinalizador para determinar quais opções são suportadas:<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|Uma máscara de bit SQLINTEGER enumerando as instruções SQL posicionadas suportadas.<br /><br /> As seguintes máscaras de bit são usadas para determinar quais instruções são suportadas:<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|Uma máscara de bit SQLINTEGER enumerando as opções de controle de sicronia suportadas para o cursor.<br /><br /> As seguintes máscaras de bit são usadas para determinar quais opções são suportadas:<br /><br /> SQL_SCCO_READ_ONLY = Cursor é somente leitura. Não são permitidas atualizações.<br /><br /> SQL_SCCO_LOCK = O cursor usa o nível mais baixo de bloqueio suficiente para garantir que a linha possa ser atualizada.<br /><br /> SQL_SCCO_OPT_ROWVER = O Cursor usa um controle de concorrência otimista, comparando versões de linha, como SQLBase ROWID ou Sybase TIMESTAMP.<br /><br /> SQL_SCCO_OPT_VALUES = Cursor usa controle de concorrência otimista, comparando valores.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|Uma máscara de bit SQLINTEGER enumerando se as alterações feitas por um aplicativo para um cursor estático ou orientado por chave através de **SQLSetPos** ou instruções de atualização posicionadas ou excludentes podem ser detectadas por esse aplicativo.<br /><br /> SQL_SS_ADDITIONS = As linhas adicionadas são visíveis ao cursor; o cursor pode rolar até essas linhas. Quando essas linhas são adicionadas ao cursor é dependente do motorista.<br /><br /> SQL_SS_DELETIONS = As linhas excluídas não estão mais disponíveis no cursor e não deixam um "furo" no conjunto de resultados; depois que o cursor rola de uma linha excluída, ele não pode retornar a essa linha.<br /><br /> SQL_SS_UPDATES = As atualizações das linhas são visíveis ao cursor; se o cursor rolar e retornar a uma linha atualizada, os dados retornados pelo cursor são os dados atualizados, não os dados originais. Esta opção se aplica apenas a cursores estáticos ou atualizações em cursores orientados por conjuntos de chaves que não atualizam a chave. Esta opção não se aplica a um cursor dinâmico ou no caso em que uma chave é alterada em um cursor misto.<br /><br /> Se um aplicativo pode detectar alterações feitas no resultado definido por outros usuários, incluindo outros cursores no mesmo aplicativo, depende do tipo de cursor.|  
  
 Um aplicativo ODBC 3 *.x* que trabalha com um driver ODBC 3 *.x* não deve ligar para **o SQLGetInfo** com os argumentos *infoType* descritos na tabela anterior, mas deve usar os argumentos ODBC 3 *.x* *InfoType* listados no parágrafo a seguir. Não há uma correspondência um-para-um entre os argumentos *do InfoType* usados no ODBC 2. *x* e aqueles utilizados em ODBC 3 *.x*. Um aplicativo ODBC 3 *.x* trabalhando com um ODBC 2. *x* driver, por outro lado, deve usar os argumentos *InfoType* descritos anteriormente.  
  
 Alguns dos tipos de informação na tabela anterior são preteridos em favor dos tipos de informações dos atributos do cursor. Essas informações depreciativas são SQL_FETCH_DIRECTION, SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY e SQL_STATIC_SENSITIVITY. Os novos tipos de atributos do cursor são SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2, onde XXX é igual a DINÂMICA, FORWARD_ONLY, KEYSET_DRIVEN ou ESTática. Cada um dos novos tipos indica as capacidades do driver para um único tipo de cursor. Para obter mais informações sobre essas opções, consulte a descrição da função [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)
