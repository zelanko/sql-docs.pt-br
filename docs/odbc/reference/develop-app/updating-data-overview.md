---
title: Atualização da visão geral dos dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9972ab61f041385ae4ca616df093ae63ad7a47d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300382"
---
# <a name="updating-data-overview"></a>Atualizar a visão geral de dados
Os aplicativos podem atualizar dados executando declarações SQL ou ligando para **SQLSetPos** ou **SQLBulkOperations**. **ATUALIZAR,** **EXCLUIR**e **INSERIR** declarações atuam diretamente na fonte de dados e geralmente são suportadas por drivers. As instruções de atualização e exclusão pesquisadas contêm uma especificação das linhas a serem alterantes. As declarações de atualização e exclusão posicionadas e os **SQLSetPos** atuam na fonte de dados através de um cursor e são menos amplamente suportados.  
  
 Se os cursores podem detectar alterações feitas no conjunto de resultados com os métodos descritos nesta seção depende do tipo do cursor e de como ele é implementado. Os cursores somente para frente não revisitam linhas e, portanto, não detectarão alterações. Para obter informações sobre se os cursores roláveis podem detectar alterações, consulte [Cursors Roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Instruções UPDATE, DELETE e INSERT](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [Instruções de atualização e exclusão posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [Simular instruções de exclusão e atualização posicionadas](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [Determinar o número de linhas afetadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [Atualizar dados com SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [Atualizar dados com SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Dados Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
