---
title: Vários hstmts (driver do Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple hstmts [ODBC]
- Paradox driver [ODBC], multiple hstmts
ms.assetid: 66aecd94-092d-43d4-9583-74f5e2990eac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5e7a9a4ec0d6426779fb55d923bc7f0607089aad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68045034"
---
# <a name="multiple-hstmts-paradox-driver"></a>Vários hstmts (Driver do Paradox)
Quando o driver ODBC Paradox for usado, se você quiser usar mais de um *HSTMT* para executar consultas em uma tabela, a tabela deverá ter um índice exclusivo (chave primária do Paradox).
