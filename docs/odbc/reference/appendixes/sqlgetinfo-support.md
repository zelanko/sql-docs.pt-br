---
title: Suporte de SQLGetInfo | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb9afa5b40ffa7628e04ee85e5ddc4f752e98935
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-support"></a>Suporte de SQLGetInfo
Quando um ODBC 2. *x* aplicativo chama **SQLGetInfo** para um ODBC 3*. x* driver, o *informação* devem ter suporte a argumentos na tabela a seguir.  
  
|*Tipo de informação*|Retorna|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **Observação:** esse tipo de informações não é preterido; bitmasks na coluna à direita são preteridos.|Um bitmask sqlinteger que contém enumerando as cláusulas no **ALTER TABLE** suporte pela fonte de dados.<br /><br /> Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:<br /><br /> SQL_AT_DROP_COLUMN = a capacidade de descartar colunas é suportada. Isso resulta em cascata ou restringir o comportamento é definido pelo driver. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = a capacidade de adicionar várias colunas em uma única instrução ALTER TABLE é suportado. Esse bit não combinar com outros SQL_AT_ADD_COLUMN_XXX ou SQL_AT_CONSTRAINT_XXX bits. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> O tipo de informações foi introduzido no ODBC 1.0; cada máscara de bits é rotulada com a versão na qual ele foi introduzido.|Uma máscara de bits de sqlinteger que contém enumerando as opções de direção de busca com suporte.<br /><br /> Bitmasks a seguir são usados em conjunto com o sinalizador para determinar quais opções são suportadas:<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|Os tipos de um bitmask de sqlinteger que contém enumerar o bloqueio com suporte para o *fLock* argumento **SQLSetPos**.<br /><br /> Bitmasks a seguir são usados em conjunto com o sinalizador para determinar quais tipos de bloqueio têm suporte:<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|Um valor SQLSMALLINT que indica o nível de conformidade do ODBC.<br /><br /> SQL_OAC_NONE = nenhum<br /><br /> SQL_OAC_LEVEL1 = 1 de nível de suporte<br /><br /> SQL_OAC_LEVEL2 = nível 2 com suporte|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|Um valor SQLSMALLINT indicando que a gramática SQL com suporte pelo driver. Consulte [gramática de SQL do apêndice c:](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) para uma definição dos níveis de conformidade do SQL.<br /><br /> SQL_OSC_MINIMUM = gramática mínima com suporte<br /><br /> SQL_OSC_CORE = gramática Core com suporte<br /><br /> SQL_OSC_EXTENDED = gramática estendido com suporte|  
|SQL_POS_OPERATIONS (ODBC 2.0)|Um bitmask sqlinteger que contém enumerando as operações com suporte no **SQLSetPos**.<br /><br /> Bitmasks a seguir são usados em conjunto com o sinalizador para determinar quais opções são suportadas:<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|Um bitmask de sqlinteger que contém a enumeração com suporte posicionado instruções SQL.<br /><br /> Bitmasks a seguir são usados para determinar quais declarações são suportadas:<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|Uma máscara de bits de sqlinteger que contém enumerando as opções de controle de simultaneidade tem suportadas para o cursor.<br /><br /> Bitmasks a seguir são usados para determinar quais opções são suportadas:<br /><br /> SQL_SCCO_READ_ONLY = Cursor é somente leitura. Não são permitidas atualizações.<br /><br /> SQL_SCCO_LOCK = o Cursor usa o nível mais baixo de bloqueio suficiente para garantir que a linha pode ser atualizada.<br /><br /> SQL_SCCO_OPT_ROWVER = controle de simultaneidade otimista usa Cursor, comparando versões de linha, como SQLBase ROWID ou Sybase TIMESTAMP.<br /><br /> SQL_SCCO_OPT_VALUES = controle de simultaneidade otimista usa Cursor, comparação de valores.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|Uma máscara de bits de sqlinteger que contém enumerando se as alterações feitas por um aplicativo para um cursor estático ou controlado por meio de **SQLSetPos** ou atualização posicionada ou instruções delete podem ser detectadas pelo aplicativo.<br /><br /> SQL_SS_ADDITIONS = adicionado linhas são visíveis para o cursor; o cursor pode rolar para essas linhas. Em que essas linhas são adicionadas ao cursor depende do driver.<br /><br /> SQL_SS_DELETIONS = excluídas linhas não estão mais disponíveis para o cursor e não deixe um "buraco" no conjunto de resultados; Após rola o cursor de uma linha excluída, ela não pode retornar a essa linha.<br /><br /> SQL_SS_UPDATES = atualizações para linhas são visíveis para o cursor; Se o cursor rola do e retorna para uma linha atualizada, os dados retornados pelo cursor são os dados atualizados, não os dados originais. Essa opção se aplica a Cursores estáticos somente para ou atualizações em cursores controlados por conjuntos de chaves que não atualizar a chave. Essa opção não se aplica para um cursor dinâmico ou no caso em que uma chave é alterada em um cursor misto.<br /><br /> Se um aplicativo pode detectar alterações feitas ao conjunto de resultados por outros usuários, incluindo outros cursores no mesmo aplicativo, dependendo do tipo de cursor.|  
  
 Um ODBC 3*. x* aplicativo trabalhando com um ODBC 3*. x* driver não deve chamar **SQLGetInfo** com o *informação* argumentos descrito em anterior da tabela, mas deve usar o ODBC 3*. x* *informação* argumentos listados no seguinte parágrafo. Não há uma correspondência entre *informação* argumentos usados no ODBC 2. *x* e usadas em ODBC 3*. x*. Um ODBC 3*. x* aplicativo trabalhando com um ODBC 2. *x* driver, por outro lado, deve usar o *informação* argumentos descritos anteriormente.  
  
 Alguns dos tipos de informações na tabela anterior são preteridos em favor de tipos de informações de atributos de cursor. Esses preterido informações tipos são SQL_FETCH_DIRECTION, SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY e SQL_STATIC_SENSITIVITY. Os novos tipos de atributos de cursor são SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2, onde XXX é igual a DYNAMIC, FORWARD_ONLY, KEYSET_DRIVEN ou STATIC. Cada um dos novos tipos indica os recursos de driver para um tipo de cursor único. Para obter mais informações sobre essas opções, consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.

