---
title: Limitações da instrução DROP tabela | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, DROP TABLE statement limitations
- DROP TABLE statement limitations [ODBC]
ms.assetid: 0a1c80f5-c9f2-4655-9bfd-0131b2f015a9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a24a22a5e666421136780f3614db4df2233bc82
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128014"
---
# <a name="drop-table-statement-limitations"></a>Limitações da instrução DROP TABLE
Quando o driver do Microsoft Excel 97, 7.0 ou 5.0 é usado, a instrução DROP TABLE limpa a planilha, mas não exclui o nome da planilha. Como o nome da planilha ainda existe na pasta de trabalho, outra planilha não pode ser criada com o mesmo nome.
