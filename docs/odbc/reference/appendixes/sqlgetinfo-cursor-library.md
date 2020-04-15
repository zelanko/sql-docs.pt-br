---
title: SQLGetInfo (Biblioteca Cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Cursor Library
ms.assetid: 1b4d220d-2c07-4f56-987e-36813bb1a6ce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9067fd8b33cb2408f1ef6f0e58603eb4f1f7eb09
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307807"
---
# <a name="sqlgetinfo-cursor-library"></a>SQLGetInfo (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLGetInfo** na biblioteca do cursor. Para obter informações gerais sobre **o SQLGetInfo,** consulte [SQLGetInfo Function](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 A biblioteca do cursor retorna valores para os seguintes valores do *InfoType* (&#124; representa um pouco de OR); para todos os outros valores do *InfoType,* ele chama **SQLGetInfo** no driver.  
  
|*Infotipo*|Valor retornado|  
|----------------|--------------------|  
|SQL_BOOKMARK_PERSISTENCE|SQL_BP_SCROLL|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|0|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|0|  
|SQL_FETCH_DIRECTION[1]|SQL_FD_FETCH_ABSOLUTE &#124; SQL_FD_FETCH_FIRST &#124; SQL_FD_FETCH_LAST &#124; SQL_FD_FETCH_NEXT &#124; SQL_FD_FETCH_PRIOR &#124; SQL_FD_FETCH_RELATIVE &#124; SQL_FD_FETCH_BOOKMARK|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT &#124; SQL_CA1_ABSOLUTE &#124; SQL_CA1_RELATIVE &#124; SQL_CA1_LOCK_NO_CHANGE &#124; SQL_CA1_POS_POSITION &#124; SQL_CA1_POSITIONED_DELETE &#124; SQL_CA1_POSITIONED_UPDATE &#124; SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &#124; SQL_CA2_OPT_VALUES_CONCURRENCY &#124; SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_GETDATA_EXTENSIONS|SQL_GD_BLOCK &#124; quaisquer valores devolvidos pelo driver **Nota:** Quando os dados são recuperados com **SQLFetchScroll,** **o SQLGetData** suporta a funcionalidade especificada com as máscaras de bits SQL_GD_ANY_COLUMN e SQL_GD_BOUND.|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES1|0|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES2|0|  
|SQL_LOCK_TYPES[1]|SQL_LCK_NO_CHANGE|  
|SQL_STATIC_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT &#124; SQL_CA1_ABSOLUTE &#124; SQL_CA1_RELATIVE &#124; SQL_CA1_BOOKMARK &#124; SQL_CA1_LOCK_NO_CHANGE &#124; SQL_CA1_POS_POSITION &#124; SQL_CA1_POSITIONED_DELETE &#124; SQL_CA1_POSITIONED_UPDATE &#124; SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_STATIC_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &#124; SQL_CA2_OPT_VALUES_ CONCURRENCY &#124; SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_POS_OPERATIONS[1]|SQL_POS_POSITION|  
|SQL_POSITIONED_STATEMENTS[1]|SQL_PS_POSITIONED_DELETE &#124; SQL_PS_POSITIONED_UPDATE &#124; SQL_PS_SELECT_FOR_UPDATE|  
|SQL_ROW_UPDATES|"Y"|  
|SQL_SCROLL_CONCURRENCY[1]|SQL_SCCO_READ_ONLY &#124; SQL_SCCO_OPT_VALUES|  
|SQL_SCROLL_OPTIONS|SQL_SO_FORWARD_ONLY &#124; SQL_SO_STATIC|  
|SQL_STATIC_SENSITIVITY[1]|SQL_SS_UPDATES|  
  
 [1] Usado somente quando a biblioteca do cursor é usada com um driver ODBC 2.x.  
  
> [!IMPORTANT]  
>  A biblioteca cursor implementa o mesmo comportamento do cursor quando as transações são cometidas ou revertidas como fonte de dados. Ou seja, cometer ou reverter uma transação, seja ligando para **o SQLEndTran** ou usando o atributo de conexão SQL_ATTR_AUTOCOMMIT, pode fazer com que a fonte de dados exclua os planos de acesso e feche os cursores para todas as declarações em uma conexão. Para obter mais informações, consulte os tipos de informações SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).
