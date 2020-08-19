---
description: SQLBindParameter (Driver do Excel)
title: SQLBindParameter (driver do Excel) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2f18d34bb17f6f6b039bac5f6842ff837c22f362
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483369"
---
# <a name="sqlbindparameter-excel-driver"></a>SQLBindParameter (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do Excel. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando o driver do Microsoft Excel é usado, a execução de uma instrução INSERT que usa um parâmetro para inserir um NULL em uma coluna SQL_CHAR retornará SQL_SUCCESS_WITH_INFO com SQLSTATE 01004, "dados truncados".
