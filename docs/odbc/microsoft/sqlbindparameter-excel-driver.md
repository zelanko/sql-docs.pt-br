---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8b33200e0628566bc88f770ca1fe8fd895ecbf2a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063252"
---
# <a name="sqlbindparameter-excel-driver"></a>SQLBindParameter (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do Excel. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando o driver do Microsoft Excel é usado, a execução de uma instrução INSERT que usa um parâmetro para inserir um NULL em uma coluna SQL_CHAR retornará SQL_SUCCESS_WITH_INFO com SQLSTATE 01004, "dados truncados".
