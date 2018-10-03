---
title: SQLColumns (Driver do Paradox) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0bf6d08859c0ea8fb71ce398dbf4b71fe0d0a1c1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705884"
---
# <a name="sqlcolumns-paradox-driver"></a>SQLColumns (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Paradox. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|coluna|Comentários|  
|------------|--------------|  
|TABLE_QUALIFIER|O caminho para um diretório é retornado.|  
|TABLE_OWNER|NULL será retornado nessa coluna porque não há suporte para o nome do proprietário.|  
|NULLABLE|SQL_NO_NULLS é retornado para colunas que participam em uma chave primária ou índice exclusivo.|
