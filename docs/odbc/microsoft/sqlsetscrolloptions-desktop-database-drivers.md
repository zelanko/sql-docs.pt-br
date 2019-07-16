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
ms.openlocfilehash: 0adedfb69cd4a7b5cf195916747687826805e8bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905388"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (Drivers de banco de dados de área de trabalho)
Para SQL_CONCUR_READ_ONLY, há suporte para cursores de avanço e estáticos.  
  
 Somente os cursores controlados por têm suporte para um *fConcurrency* argumento de SQL_CONCUR_LOCK.  
  
 Uma *fConcurrency* não há suporte para o argumento de SQL_CONCUR_ROWVER.  
  
 Não há suporte para cursores Dynamic e cursores mistos.
