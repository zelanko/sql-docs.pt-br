---
title: SQLProcedureColumns (Driver do Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a438823d1aa71eecb25c4935026c1b43e45842d1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812694"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Access. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Os desenvolvedores de aplicativos devem procurar colunas definidos pelo driver iniciando pelo final do conjunto de resultados e continuar para trás.  
  
|coluna|Comentários|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT ou SQL_RESULT_COL|  
|ORDINAL|Esta é uma coluna de driver específico que é retornada no final do conjunto de resultados. O tipo SQL da coluna é um inteiro.|
