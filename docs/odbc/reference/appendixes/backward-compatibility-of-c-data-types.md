---
description: Compatibilidade com versões anteriores de tipos de dados do C
title: Compatibilidade com versões anteriores de tipos de dados C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e50a07d3c49438fcdfbc0b57ec70380d20c88440
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411312"
---
# <a name="backward-compatibility-of-c-data-types"></a>Compatibilidade com versões anteriores de tipos de dados do C
SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT foram substituídos em ODBC por tipos assinados e sem sinal: SQL_C_SSHORT e SQL_C_USHORT, SQL_C_SLONG e SQL_C_ULONG e SQL_C_STINYINT e SQL_C_UTINYINT. Um driver ODBC *3. x* que deve funcionar com aplicativos ODBC *2. x* deve dar suporte a SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT, porque quando eles são chamados, o Gerenciador de driver os passa para o driver.
