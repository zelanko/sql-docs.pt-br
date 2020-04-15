---
title: 'Passo 2: Inicialize a aplicação | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 843155ba6b641ea26717e63af55c8774f963a800
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288262"
---
# <a name="step-2-initialize-the-application"></a>Etapa 2: Inicializar o aplicativo
O segundo passo é inicializar a aplicação, como mostra a ilustração a seguir. Exatamente o que é feito aqui varia com a aplicação.  
  
 ![Mostra a inicialização de um aplicativo ODBC](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 Neste ponto, é comum usar **o SQLGetInfo** para descobrir as capacidades do driver. Para obter mais informações, consulte [Considerando recursos de banco de dados para usar](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Todos os aplicativos precisam alocar uma alça de declaração com **SQLAllocHandle**, e muitos aplicativos definem atributos de declaração, como o tipo de cursor, com **SQLSetStmtAttr**. Para obter mais informações, consulte [Alocando uma alça de declaração](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) e [atributos de declaração](../../../odbc/reference/develop-app/statement-attributes.md).
