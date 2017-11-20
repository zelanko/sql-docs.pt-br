---
title: Para SQLParamOptions (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 17a82974d8531d0524f4bac89701d6c97a05198d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>Para SQLParamOptions (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do Driver ODBC do Visual FoxPro. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade de API de ODBC: Nível 1  
  
 Permite que um aplicativo especificar vários valores para o conjunto de parâmetros atribuído por [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). A capacidade de especificar vários valores para um conjunto de parâmetros é útil para inserções em massa e outro trabalho que exija a fonte de dados para processar a mesma instrução SQL várias vezes com vários valores de parâmetro. Por exemplo, um aplicativo pode especificar três conjuntos de valores para o conjunto de parâmetros associados a um **inserir** instrução e, em seguida, execute o **inserir** Inserir instrução uma vez para executar os três operações.  
  
 Para obter mais informações, consulte [para SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) no *referência do programador de ODBC*.

