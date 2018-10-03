---
title: Suporte SQLGetInfo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6eb6bedb20e1f61c48776d03df59aa6865cfb2a3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680772"
---
# <a name="sqlgetinfo-support"></a>Suporte SQLGetInfo
Quando um ODBC 2. *x* aplicativo chamará **SQLGetInfo** para um ODBC 3 *. x* driver, o *tipo de informação* argumentos na tabela a seguir devem ser suportados.  
  
|*tipo de informação*|Retorna|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **Observação:** este tipo de informação não é preterido; as máscaras de bits na coluna à direita são preteridas.|Um bitmask sqlinteger que contém enumerando as cláusulas na **ALTER TABLE** instrução tem suportada pela fonte de dados.<br /><br /> As máscaras de bits a seguir são usadas para determinar quais cláusulas têm suporte:<br /><br /> SQL_AT_DROP_COLUMN = há suporte para a capacidade para descartar colunas. Se isso resulta em cascata ou restringir o comportamento é definido pelo driver. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = a capacidade de adicionar várias colunas em uma única instrução ALTER TABLE é suportado. Esse bit não combina com outros SQL_AT_ADD_COLUMN_XXX ou SQL_AT_CONSTRAINT_XXX bits. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> O tipo de informação foi introduzido no ODBC 1.0; cada máscara de bits é rotulada com a versão na qual ele foi introduzido.|Um bitmask sqlinteger que contém enumerando as opções de direção de busca com suporte.<br /><br /> As máscaras de bits a seguir são usadas em conjunto com o sinalizador para determinar quais opções têm suporte:<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|Os tipos de um bitmask sqlinteger que contém Enumerando o bloqueio com suporte para o *usam* argumento **SQLSetPos**.<br /><br /> As máscaras de bits a seguir são usadas em conjunto com o sinalizador para determinar quais tipos de bloqueio têm suporte:<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|Um valor de SQLSMALLINT, que indica o nível de conformidade do ODBC.<br /><br /> SQL_OAC_NONE = nenhum<br /><br /> SQL_OAC_LEVEL1 = 1 de nível de suporte<br /><br /> SQL_OAC_LEVEL2 = 2 de nível de suporte|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|Um valor SQLSMALLINT indicando a gramática SQL com suporte pelo driver. Ver [apêndice c: SQL gramática](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) para obter uma definição de níveis de conformidade do SQL.<br /><br /> SQL_OSC_MINIMUM = gramática mínima com suporte<br /><br /> SQL_OSC_CORE = gramática Core com suporte<br /><br /> SQL_OSC_EXTENDED = gramática estendido com suporte|  
|SQL_POS_OPERATIONS (ODBC 2.0)|Um bitmask sqlinteger que contém enumerando as operações com suporte no **SQLSetPos**.<br /><br /> Seguir as máscaras de bits são usadas em conjunto com o sinalizador para determinar quais opções têm suporte:<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|Um bitmask de sqlinteger que contém a enumeração com o suporte posicionado instruções SQL.<br /><br /> As máscaras de bits a seguir são usadas para determinar quais declarações são suportadas:<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|Um bitmask sqlinteger que contém enumerando as opções de controle de simultaneidade com suporte para o cursor.<br /><br /> As máscaras de bits a seguir são usadas para determinar quais opções têm suporte:<br /><br /> SQL_SCCO_READ_ONLY = Cursor é somente leitura. Não são permitidas atualizações.<br /><br /> SQL_SCCO_LOCK = Cursor usa o nível mais baixo de bloqueio suficiente para garantir que a linha pode ser atualizada.<br /><br /> SQL_SCCO_OPT_ROWVER = controle de simultaneidade otimista de usos do Cursor, comparando as versões de linha, como SQLBase ROWID ou Sybase TIMESTAMP.<br /><br /> SQL_SCCO_OPT_VALUES = controle de simultaneidade otimista de usos do Cursor, comparar valores.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|Um bitmask de sqlinteger que contém enumerando se as alterações feitas por um aplicativo para um cursor estático ou controlado por meio **SQLSetPos** ou instruções de exclusão ou atualização posicionada podem ser detectadas pelo aplicativo.<br /><br /> SQL_SS_ADDITIONS = adicionado linhas são visíveis para o cursor; o cursor pode rolar a essas linhas. Em que essas linhas são adicionadas ao cursor é dependente do driver.<br /><br /> SQL_SS_DELETIONS = Deleted linhas não estão mais disponíveis para o cursor e não deixe uma "brecha" no conjunto de resultados; Depois que rola o cursor de uma linha excluída, ela não pode retornar a essa linha.<br /><br /> SQL_SS_UPDATES = atualizações para linhas são visíveis para o cursor; Se o cursor rolará do e retorna para uma linha atualizada, os dados retornados pelo cursor são os dados atualizados, não os dados originais. Essa opção se aplica a Cursores estáticos somente para ou atualizações em cursores controlados por que não atualizar a chave. Essa opção não se aplica para um cursor dinâmico ou no caso em que uma chave é alterada em um cursor misto.<br /><br /> Se um aplicativo pode detectar as alterações feitas em um conjunto de resultados por outros usuários, incluindo outros cursores no mesmo aplicativo, depende do tipo cursor.|  
  
 Um ODBC 3 *. x* aplicativo trabalhar com um ODBC 3 *. x* driver não deve chamar **SQLGetInfo** com o *tipo de informação* argumentos descritos nas anterior de tabela, mas deve usar o ODBC 3 *. x* *tipo de informação* argumentos listados no parágrafo a seguir. Não há uma correspondência direta entre *tipo de informação* argumentos usados no ODBC 2. *x* quanto os usados no ODBC 3 *. x*. Um ODBC 3 *. x* aplicativo trabalhar com um ODBC 2. *x* driver, por outro lado, deve usar o *tipo de informação* argumentos descritos anteriormente.  
  
 Alguns dos tipos de informações na tabela anterior são preteridos a favor dos tipos de informação de atributos de cursor. Eles preterido informações tipos são SQL_FETCH_DIRECTION, SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY e SQL_STATIC_SENSITIVITY. Os novos tipos de atributos de cursor são SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2, onde XXX é igual a DYNAMIC, FORWARD_ONLY, KEYSET_DRIVEN ou estático. Cada um dos novos tipos indica os recursos de driver para um tipo de cursor único. Para obter mais informações sobre essas opções, consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.
