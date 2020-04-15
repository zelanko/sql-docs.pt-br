---
title: Implementando SQLGetDiagRec e SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c090af19a9296e46e3036ca23f6c97298bcb1b8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300136"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementar SQLGetDiagRec e SQLGetDiagField
**SQLGetDiagRec** e **SQLGetDiagField** são implementados pelo Driver Manager e cada driver. O Driver Manager e cada driver mantêm registros de diagnóstico para cada ambiente, conexão, declaração e alça descritor, e liberam esses registros somente quando outra função é chamada com essa alça ou a alça é liberada.  
  
 Embora o Driver Manager e cada driver devam determinar o primeiro registro de status de acordo com os rankings em [Seqüência de Registros de Status,](../../../odbc/reference/develop-app/sequence-of-status-records.md)o Driver Manager determina a seqüência final de registros.  
  
 **SQLGetDiagRec** e **SQLGetDiagField** não postam registros de diagnóstico sobre si mesmos.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Regras de tratamento de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Função do Gerenciador do Driver](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Função do driver](../../../odbc/reference/develop-app/role-of-the-driver.md)
