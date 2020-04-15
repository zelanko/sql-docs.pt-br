---
title: 'Passo 4b: Buscar a Contagem de Linhas | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31ccbd15ae435165ea007fa9f3c0505c1dcc5aa0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302957"
---
# <a name="step-4b-fetch-the-row-count"></a>Etapa 4b: Buscar a contagem de linhas
O próximo passo é buscar a contagem de linhas, como mostrado na ilustração a seguir.  
  
 ![Mostra a busca da contagem de linhas](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 Se a instrução executada na Etapa 3 foi uma instrução **UPDATE**, **DELETE**ou **INSERT,** o aplicativo recuperará a contagem de linhas afetadas com **SQLRowCount**. Para obter mais informações, consulte [Determinar o número de linhas afetadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
 O aplicativo agora retorna à etapa 3 para executar outra declaração na mesma transação ou passa para a etapa 5 para cometer ou reverter a transação.
