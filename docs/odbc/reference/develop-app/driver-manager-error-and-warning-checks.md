---
description: Verificações de aviso e de erro do Gerenciador de Driver
title: Verificações de erro e aviso do Gerenciador de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 99a99e1dfeb6cb6993a6967d5d93748afbd44b83
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483049"
---
# <a name="driver-manager-error-and-warning-checks"></a>Verificações de aviso e de erro do Gerenciador de Driver
O Gerenciador de Driver implementa de forma completa ou parcial várias funções e, portanto, verifica todos os erros e avisos nessas funções.  
  
-   O Gerenciador de Driver implementa **SQLDataSources** e **sqldriveers** e verifica todos os erros e avisos nessas funções.  
  
-   O Gerenciador de driver verifica se um driver implementa **SQLGetFunctions**. Se o driver não implementar **SQLGetFunctions**, o Gerenciador de Driver implementa e verifica todos os erros e avisos nele.  
  
-   O Gerenciador de Driver implementa parcialmente **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**, **SQLFreeHandle**, **SQLGetDiagRec**e **SQLGetDiagField** e verifica alguns erros nessas funções. Ele pode retornar os mesmos erros que o driver para algumas dessas funções porque ambos executam operações semelhantes. Por exemplo, o driver ou o Gerenciador de driver pode retornar SQLSTATE IM008 (falha na caixa de diálogo) se qualquer um não puder exibir uma caixas de diálogo de logon para **SQLDriverConnect**.
