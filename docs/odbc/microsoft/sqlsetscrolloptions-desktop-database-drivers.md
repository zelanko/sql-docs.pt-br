---
title: SQLSetScrollOptions (Drivers de banco de dados da área de trabalho) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e74a3207691aca001dcf334c1ee50d53d4f34d69
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809544"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (Drivers de banco de dados de área de trabalho)
Para SQL_CONCUR_READ_ONLY, há suporte para cursores de avanço e estáticos.  
  
 Somente os cursores controlados por têm suporte para um *fConcurrency* argumento de SQL_CONCUR_LOCK.  
  
 Uma *fConcurrency* não há suporte para o argumento de SQL_CONCUR_ROWVER.  
  
 Não há suporte para cursores Dynamic e cursores mistos.
