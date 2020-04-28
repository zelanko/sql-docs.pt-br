---
title: SQLSetScrollOptions (drivers de banco de dados de desktop) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c47255b455354c49133d61c3546be63ab2380a1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299426"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (Drivers de banco de dados de área de trabalho)
Há suporte para cursores diretos e estáticos para SQL_CONCUR_READ_ONLY.  
  
 Somente cursores controlados por conjunto de chaves têm suporte para um argumento *fConcurrency* de SQL_CONCUR_LOCK.  
  
 Não há suporte para um argumento *fConcurrency* de SQL_CONCUR_ROWVER.  
  
 Não há suporte para cursores dinâmicos e mistos.
