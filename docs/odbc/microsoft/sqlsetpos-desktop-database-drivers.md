---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d35a282acf3b672113ec71b534b4087aa3549285
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905458"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (Drivers de banco de dados de área de trabalho)
Há suporte para a semântica de modelo em massa para chamadas **SQLSetPos** com o argumento *IRow* igual a 0.  
  
 SQL_LOCK_NO_CHANGE tem suporte para *Flock*. Não há suporte para SQL_LOCK_EXCLUSIVE e SQL_LOCK_UNLOCK.  
  
 O **SQLSetPos** dá suporte a junções atualizáveis. (Para obter mais informações, consulte o *Guia do programador do Microsoft Jet mecanismo de banco de dados*.)
