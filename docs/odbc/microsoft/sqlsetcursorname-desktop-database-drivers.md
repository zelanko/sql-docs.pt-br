---
title: SQLSetCursorName (drivers de banco de dados de desktop) | Microsoft Docs
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
ms.openlocfilehash: 53ef01423ad14cb5606e14ca004ca614e68101e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905506"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (Drivers de banco de dados de área de trabalho)
Como o driver não dá suporte a uma atualização posicionada ou exclusão pelo local em que a sintaxe de *cursorname* , **SQLSetCursorName** tem suporte, mas não pode ser usada para atualizações posicionadas. Ele só pode ser usado quando a biblioteca de cursores está habilitada e o aplicativo está usando **SQLExtendedFetch**.
