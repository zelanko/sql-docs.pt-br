---
title: "Visão geral de dados de atualização | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3da35917f3979b041d6eb5b61d6554d4ef4c4585
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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

