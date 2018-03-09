---
title: 'Etapa 4b: buscar a contagem de linhas | Microsoft Docs'
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
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0eda22056173ea6ca90dd4ecc31146de54fbfae
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="step-4b-fetch-the-row-count"></a>Etapa 4b: buscar a contagem de linhas
A próxima etapa é obter a contagem de linhas, conforme mostrado na ilustração a seguir.  
  
 ![Mostra a busca a contagem de linhas](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 Se a instrução executada na etapa 3 foi um **atualização**, **excluir**, ou **inserir** instrução, o aplicativo recupera a contagem de linhas afetadas com  **SQLRowCount**. Para obter mais informações, consulte [determinando o número de linhas afetadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
 Agora, o aplicativo retorna para a etapa 3 para executar outra instrução na mesma transação ou vai para a etapa 5 para confirmar ou reverter a transação.
