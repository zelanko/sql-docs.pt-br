---
title: SQLSetScrollOptions (Drivers do banco de dados de área de trabalho) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6014ce55b2de2279c060361ed7e6131fd7e8b030
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (Drivers do banco de dados de área de trabalho)
Há suporte para cursores de avanço e estáticos para SQL_CONCUR_READ_ONLY.  
  
 Somente os cursores controlados por conjuntos de chaves com suporte para um *fConcurrency* argumento de SQL_CONCUR_LOCK.  
  
 Um *fConcurrency* não há suporte para o argumento de SQL_CONCUR_ROWVER.  
  
 Não há suporte para cursores Dynamic e cursores mistos.
