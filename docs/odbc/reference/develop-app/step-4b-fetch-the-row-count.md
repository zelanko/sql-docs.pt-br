---
title: 'Etapa 4B: buscar a contagem de linhas | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9455c6589ed93a51e404f3e50d1cb86a0c0c8476
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114156"
---
# <a name="step-4b-fetch-the-row-count"></a>Etapa 4b: Buscar a contagem de linhas
A próxima etapa é buscar a contagem de linhas, conforme mostrado na ilustração a seguir.  
  
 ![Mostra a busca da contagem de linhas](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 Se a instrução executada na etapa 3 fosse uma instrução **Update**, **delete**ou **Insert** , o aplicativo recuperará a contagem de linhas afetadas com **SQLRowCount**. Para obter mais informações, consulte [determinando o número de linhas afetadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
 O aplicativo agora retorna à etapa 3 para executar outra instrução na mesma transação ou prossegue para a etapa 5 para confirmar ou reverter a transação.
