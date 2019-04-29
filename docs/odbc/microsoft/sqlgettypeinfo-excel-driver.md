---
title: SQLGetTypeInfo (Excel Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Excel Driver
- Excel driver [ODBC], SQLGetTypeInfo
ms.assetid: 708845be-e6a1-4677-8113-c52819a43fa4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac7fe52ffdbb090e0b63a972e77c1a7f7a756446
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63034903"
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Excel. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O nome do tipo (TYPE_NAME) retornado na tabela produzida pelo **SQLGetTypeInfo** será o nome mais comumente usado pela fonte de dados.  
  
 SQL_ALL_EXCEPT_LIKE será retornado na coluna PESQUISÁVEL por Byte, contador, Double, tipos de dados único, longa e curta. (A capacidade de LIKE pode ser obtida ao converter o valor em um caractere usando as funções de conversão canônico do ODBC, em seguida, executar a comparação).  
  
 Quando o driver do Microsoft Excel for usado, os nomes de tipo ODBC são retornados na coluna TYPE_NAME que é retornada por **SQLGetTypeInfo**.
