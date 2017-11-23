---
title: SQLGetInfo (biblioteca de Cursor) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLGetInfo function [ODBC], Cursor Library
ms.assetid: 1b4d220d-2c07-4f56-987e-36813bb1a6ce
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fe270f6c939711d91a6b6c7a4ffd2a0a37479334
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetinfo-cursor-library"></a>SQLGetInfo (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLGetInfo** função na biblioteca de cursor. Para obter informações gerais sobre **SQLGetInfo**, consulte [função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 A biblioteca de cursores retorna valores para os seguintes valores de *informação* (&#124; representa um OR bit a bit); para todos os outros valores de *informação*, ele chama **SQLGetInfo** no driver.  
  
|*Tipo de informação*|Valor retornado|  
|----------------|--------------------|  
|SQL_BOOKMARK_PERSISTENCE|SQL_BP_SCROLL|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|0|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|0|  
|SQL_FETCH_DIRECTION [1]|SQL_FD_FETCH_ABSOLUTE &#124; SQL_FD_FETCH_FIRST &#124; SQL_FD_FETCH_LAST &#124; SQL_FD_FETCH_NEXT &#124; SQL_FD_FETCH_PRIOR &#124; SQL_FD_FETCH_RELATIVE &#124; SQL_FD_FETCH_BOOKMARK|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT &#124; SQL_CA1_ABSOLUTE &#124; SQL_CA1_RELATIVE &#124; SQL_CA1_LOCK_NO_CHANGE &#124; SQL_CA1_POS_POSITION &#124; SQL_CA1_POSITIONED_DELETE &#124; SQL_CA1_POSITIONED_UPDATE &#124; SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &#124; SQL_CA2_OPT_VALUES_CONCURRENCY &#124; SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_GETDATA_EXTENSIONS|SQL_GD_BLOCK &#124; os valores retornados pelo driver **Observação:** quando os dados são recuperados com **SQLFetchScroll**, **SQLGetData** oferece suporte a funcionalidade especificada com o SQL_GD_ANY_COLUMN e SQL_GD_BOUND bitmasks.|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES1|0|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES2|0|  
|SQL_LOCK_TYPES [1]|SQL_LCK_NO_CHANGE|  
|SQL_STATIC_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT &#124; SQL_CA1_ABSOLUTE &#124; SQL_CA1_RELATIVE &#124; SQL_CA1_BOOKMARK &#124; SQL_CA1_LOCK_NO_CHANGE &#124; SQL_CA1_POS_POSITION &#124; SQL_CA1_POSITIONED_DELETE &#124; SQL_CA1_POSITIONED_UPDATE &#124; SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_STATIC_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &#124; SQL_CA2_OPT_VALUES_ SIMULTANEIDADE &#124; SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_POS_OPERATIONS [1]|SQL_POS_POSITION|  
|SQL_POSITIONED_STATEMENTS [1]|SQL_PS_POSITIONED_DELETE &#124; SQL_PS_POSITIONED_UPDATE &#124; SQL_PS_SELECT_FOR_UPDATE|  
|SQL_ROW_UPDATES|"Y"|  
|SQL_SCROLL_CONCURRENCY [1]|SQL_SCCO_READ_ONLY &#124; SQL_SCCO_OPT_VALUES|  
|SQL_SCROLL_OPTIONS|SQL_SO_FORWARD_ONLY &#124; SQL_SO_STATIC|  
|SQL_STATIC_SENSITIVITY [1]|SQL_SS_UPDATES|  
  
 [1] usado apenas quando a biblioteca de cursores é usada com um driver de ODBC 2. x.  
  
> [!IMPORTANT]  
>  A biblioteca de cursores implementa o mesmo comportamento do cursor quando transações são confirmadas ou revertidas como a fonte de dados. Ou seja, confirmar ou reverter uma transação, ou chamando **SQLEndTran** ou usando o atributo de conexão SQL_ATTR_AUTOCOMMIT, pode fazer com que a fonte de dados excluir os planos de acesso e fechar os cursores para todas as instruções em uma conexão. Para obter mais informações, consulte os tipos de informações SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).
