---
title: SQLSetScrollOptions (Drivers de banco de dados da área) | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299426"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (Drivers de banco de dados de área de trabalho)
Cursores dianteiros e estáticos são suportados para SQL_CONCUR_READ_ONLY.  
  
 Apenas os cursores orientados por keyset são suportados para um argumento *fConcurrency* de SQL_CONCUR_LOCK.  
  
 Um *argumento fConcurrency* de SQL_CONCUR_ROWVER não é suportado.  
  
 Não são suportados cursores dinâmicos e cursores mistos.
