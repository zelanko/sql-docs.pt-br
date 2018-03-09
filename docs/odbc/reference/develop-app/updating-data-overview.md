---
title: "Visão geral de dados de atualização | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 587233467dbc265be12a009b34ce0376acfd0911
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="updating-data-overview"></a>Visão geral sobre atualização de dados
Aplicativos podem atualizar dados, executando instruções SQL ou chamando **SQLSetPos** ou **SQLBulkOperations**. **ATUALIZAÇÃO**, **excluir**, e **inserir** instruções atuar diretamente na fonte de dados e geralmente têm suporte pelos drivers. Pesquisado atualização e instruções delete contém uma especificação de linhas para alterar. Posicionado atualização e instruções delete e **SQLSetPos** agir na fonte de dados através de um cursor e têm menos amplamente suporte.  
  
 Se os cursores podem detectar alterações feitas ao conjunto de resultados com os métodos descritos nesta seção depende do tipo de cursor e como ele é implementado. Cursores de somente avanço não revisitar linhas e, portanto, não detectará as alterações. Para obter informações sobre se os cursores roláveis podem detectar alterações, consulte [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Instruções UPDATE, DELETE e INSERT](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [Instruções de atualização e exclusão posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [Simulando instruções de exclusão e atualização posicionadas](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [Determinando o número de linhas afetadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [Atualizando dados com SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [Atualizando dados com SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Dados Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
