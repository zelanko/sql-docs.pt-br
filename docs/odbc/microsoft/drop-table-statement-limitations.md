---
title: Limitações da instrução DROP TABLE | Microsoft Docs
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
ms.openlocfilehash: 49ee96941c69da962e7c000c33d6eb14f66d4dab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68031154"
---
# <a name="drop-table-statement-limitations"></a>Limitações da instrução DROP TABLE
Quando o driver do Microsoft Excel 5,0, 7,0 ou 97 for usado, a instrução DROP TABLE limpará a planilha, mas não excluirá o nome da planilha. Como o nome da planilha ainda existe na pasta de trabalho, outra planilha não pode ser criada com o mesmo nome.
