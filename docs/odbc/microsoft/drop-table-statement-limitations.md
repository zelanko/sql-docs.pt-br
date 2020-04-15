---
title: Limitações da declaração da TABELA DROP | Microsoft Docs
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
ms.openlocfilehash: c296108b9ab26a6361d12ad71a1f21b21d5bea1e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303397"
---
# <a name="drop-table-statement-limitations"></a>Limitações da instrução DROP TABLE
Quando o driver do Microsoft Excel 5.0, 7.0 ou 97 é usado, a declaração TABELA DE GOTA limpa a planilha, mas não exclui o nome da planilha. Como o nome da planilha ainda existe na planilha, outra planilha não pode ser criada com o mesmo nome.
