---
title: Colunas SQL (Driver Paradoxo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLColumns
ms.assetid: d7831c7d-8be9-40a7-bc70-8d89db8fe8c9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 66bc244089af548413046357aae6371ff0c39bbf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307857"
---
# <a name="sqlcolumns-paradox-driver"></a>SQLColumns (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas do Paradox Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Coluna|Comentários|  
|------------|--------------|  
|TABLE_QUALIFIER|O caminho para um diretório é devolvido.|  
|TABLE_OWNER|NULL é devolvido nesta coluna porque o nome do proprietário não é suportado.|  
|NULLABLE|SQL_NO_NULLS é devolvido para colunas que participam de uma chave primária ou índice único.|
