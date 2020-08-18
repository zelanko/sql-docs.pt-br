---
description: SQLSetCursorName (Drivers de banco de dados de área de trabalho)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14fe15c6cdbdf50e6d28ca7e9a1168f54626e83b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411544"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (Drivers de banco de dados de área de trabalho)
Como o driver não dá suporte a uma atualização posicionada ou exclusão pelo local em que a sintaxe de *cursorname* , **SQLSetCursorName** tem suporte, mas não pode ser usada para atualizações posicionadas. Ele só pode ser usado quando a biblioteca de cursores está habilitada e o aplicativo está usando **SQLExtendedFetch**.
