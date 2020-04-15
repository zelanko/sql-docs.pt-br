---
title: Retrocompatibilidade dos tipos de dados C | Microsoft Docs
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
ms.openlocfilehash: 4a89b282a2229b6f34833b4371081661ea51b231
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304581"
---
# <a name="backward-compatibility-of-c-data-types"></a>Compatibilidade com versões anteriores de tipos de dados do C
SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT foram substituídos na ODBC por tipos assinados e não assinados: SQL_C_SSHORT e SQL_C_USHORT, SQL_C_SLONG e SQL_C_ULONG, e SQL_C_STINYINT e SQL_C_UTINYINT. Um driver ODBC *3.x* que deve funcionar com aplicativos ODBC *2.x* deve suportar SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT, porque quando eles são chamados, o Driver Manager passa para o motorista.
