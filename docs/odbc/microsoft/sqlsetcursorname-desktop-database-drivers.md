---
title: SQLSetCursorName (Drivers de banco de dados da área de trabalho) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e433e6aee341085965f361992fc8ea9ac8744353
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305627"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (Drivers de banco de dados de área de trabalho)
Porque o driver não oferece suporte a uma atualização posicionada ou exclua o WHERE CURRENT OF *cursorname* sintaxe **SQLSetCursorName** tem suporte, mas não pode ser usado para atualizações posicionadas. Ele só pode ser usado quando a biblioteca de cursores está habilitada e o aplicativo está usando **SQLExtendedFetch**.
