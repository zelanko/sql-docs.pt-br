---
title: SQLSetPos (Drivers de banco de dados da área de trabalho) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d35a282acf3b672113ec71b534b4087aa3549285
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905458"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (Drivers de banco de dados de área de trabalho)
A semântica do modelo em massa para **SQLSetPos** chamadas com o *irow* argumento igual a 0 são suportados.  
  
 SQL_LOCK_NO_CHANGE há suporte para *usam*. Não há suporte para SQL_LOCK_EXCLUSIVE e SQL_LOCK_UNLOCK.  
  
 **SQLSetPos** dá suporte a junções atualizáveis. (Para obter mais informações, consulte o *guia do programador do Microsoft Jet banco de dados Engine*.)
