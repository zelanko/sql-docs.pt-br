---
description: 'Etapa 2: Inicializar o aplicativo'
title: 'Etapa 2: inicializar o aplicativo | Microsoft Docs'
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
ms.openlocfilehash: 26d20a5b10ee7b414b9285a388359b3a93029f16
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482879"
---
# <a name="step-2-initialize-the-application"></a>Etapa 2: Inicializar o aplicativo
A segunda etapa é inicializar o aplicativo, conforme mostrado na ilustração a seguir. Exatamente o que é feito aqui varia de acordo com o aplicativo.  
  
 ![Mostra a inicialização de um aplicativo ODBC](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 Neste ponto, é comum usar o **SQLGetInfo** para descobrir os recursos do driver. Para obter mais informações, consulte [considerando os recursos de banco de dados a serem usados](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Todos os aplicativos precisam alocar um identificador de instrução com **SQLAllocHandle**e muitos aplicativos definem atributos de instrução, como o tipo de cursor, com **SQLSetStmtAttr**. Para obter mais informações, consulte [alocando um identificador de instrução](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) e [atributos de instrução](../../../odbc/reference/develop-app/statement-attributes.md).
