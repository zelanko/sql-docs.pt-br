---
description: SQLSetPos (Drivers de banco de dados de área de trabalho)
title: SQLSetPos (drivers de banco de dados de desktop) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Desktop Database Drivers
ms.assetid: 8ef027ec-8512-48fe-8fe2-2ff7cd81e331
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4aa126514bc84f5546e1f4a022d8d3e6235b2e7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421660"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (Drivers de banco de dados de área de trabalho)
Há suporte para a semântica de modelo em massa para chamadas **SQLSetPos** com o argumento *IRow* igual a 0.  
  
 SQL_LOCK_NO_CHANGE tem suporte para *Flock*. Não há suporte para SQL_LOCK_EXCLUSIVE e SQL_LOCK_UNLOCK.  
  
 O **SQLSetPos** dá suporte a junções atualizáveis. (Para obter mais informações, consulte o *Guia do programador do Microsoft Jet mecanismo de banco de dados*.)
