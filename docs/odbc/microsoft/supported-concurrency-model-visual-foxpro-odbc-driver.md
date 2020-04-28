---
title: Modelo de simultaneidade com suporte (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 253a6dd86f6dc974d53dd151636bb8b8132e4d02
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307712"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Modelo de simultaneidade com suporte (Driver ODBC do Visual FoxPro)
O driver ODBC do Visual FoxPro dá suporte à *simultaneidade somente leitura*. Seu aplicativo pode chamar [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) com uma opção SQL_CONCURRENCY de SQL_CONCUR_READ_ONLY.  
  
 Para obter mais informações, consulte a [referência do programador de ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>simultaneidade somente leitura  
 O cursor não pode ser atualizado.  
  
## <a name="row-versioning"></a>controle de versão de linha  
 Essencialmente suporte a carimbo de data/hora, em que versões de linha são comparadas no momento da atualização.
