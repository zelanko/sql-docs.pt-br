---
description: Limitações da instrução DROP TABLE
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9d56e53d8a17c15736e9423e5920c81f864e2973
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412552"
---
# <a name="drop-table-statement-limitations"></a>Limitações da instrução DROP TABLE
Quando o driver do Microsoft Excel 5,0, 7,0 ou 97 for usado, a instrução DROP TABLE limpará a planilha, mas não excluirá o nome da planilha. Como o nome da planilha ainda existe na pasta de trabalho, outra planilha não pode ser criada com o mesmo nome.
