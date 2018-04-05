---
title: SQLSetScrollOptions (Drivers do banco de dados de área de trabalho) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ddac617904825a5ad324ad991a0721b505f704a5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (Drivers do banco de dados de área de trabalho)
Há suporte para cursores de avanço e estáticos para SQL_CONCUR_READ_ONLY.  
  
 Somente os cursores controlados por conjuntos de chaves com suporte para um *fConcurrency* argumento de SQL_CONCUR_LOCK.  
  
 Um *fConcurrency* não há suporte para o argumento de SQL_CONCUR_ROWVER.  
  
 Não há suporte para cursores Dynamic e cursores mistos.
