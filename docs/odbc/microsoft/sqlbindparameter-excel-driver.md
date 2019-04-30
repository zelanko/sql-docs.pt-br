---
title: SQLBindParameter (Excel Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLBindParameter
- SQLBindParameter function [ODBC], Excel Driver
ms.assetid: 40489bc5-3e2a-425e-892d-e0dc037f4d7a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84f6e44f4849db81c591a791674878190f21e486
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298034"
---
# <a name="sqlbindparameter-excel-driver"></a>SQLBindParameter (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Excel. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando o driver do Microsoft Excel é usado, a execução de uma instrução INSERT que usa um parâmetro para inserir um valor nulo em uma coluna SQL_CHAR retornará SQL_SUCCESS_WITH_INFO, com SQLSTATE 01004, "Dados truncados".
