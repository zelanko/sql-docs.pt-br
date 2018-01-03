---
title: 'Etapa 2: Inicializar o aplicativo | Microsoft Docs'
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
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64ef3dea2a8403af43cc03a3deeee47ff16dd2b6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="step-2-initialize-the-application"></a>Etapa 2: Inicializar o aplicativo
A segunda etapa é inicializar o aplicativo, conforme mostrado na ilustração a seguir. Exatamente o que é feito aqui varia de acordo com o aplicativo.  
  
 ![Mostra a inicialização de um aplicativo ODBC](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 Neste ponto, é comum usar **SQLGetInfo** para descobrir os recursos do driver. Para obter mais informações, consulte [considerar os recursos de banco de dados para uso](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Todos os aplicativos precisam alocar um identificador de instrução com **SQLAllocHandle**, e muitos aplicativos definem atributos de instrução, como o tipo de cursor com **SQLSetStmtAttr**. Para obter mais informações, consulte [alocar um identificador de instrução](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) e [atributos de instrução](../../../odbc/reference/develop-app/statement-attributes.md).
