---
title: SQLSetPos (Drivers do banco de dados de área de trabalho) | Microsoft Docs
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
- SQLSetPos function [ODBC], Desktop Database Drivers
ms.assetid: 8ef027ec-8512-48fe-8fe2-2ff7cd81e331
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ea42a3d23d04246779beb5d312238e79ee79368
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (Drivers do banco de dados de área de trabalho)
A semântica do modelo em massa para **SQLSetPos** chamadas com o *irow* argumento igual a 0 são suportados.  
  
 Há suporte para SQL_LOCK_NO_CHANGE para *fLock*. Não há suporte para SQL_LOCK_EXCLUSIVE e SQL_LOCK_UNLOCK.  
  
 **SQLSetPos** oferece suporte a junções atualizáveis. (Para obter mais informações, consulte o *guia do programador do Microsoft Jet Database Engine*.)
