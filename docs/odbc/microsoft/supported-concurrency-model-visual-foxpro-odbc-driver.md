---
title: Modelo de Concurrency suportado (Visual FoxPro ODBC Driver) | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307712"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Modelo de simultaneidade com suporte (Driver ODBC do Visual FoxPro)
O Driver Visual FoxPro ODBC suporta *concorrência somente leitura*. Seu aplicativo pode chamar [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) com uma opção SQL_CONCURRENCY de SQL_CONCUR_READ_ONLY.  
  
 Para obter mais informações, consulte a [referência do programador ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>conmoeda somente leitura  
 O cursor não pode ser atualizado.  
  
## <a name="row-versioning"></a>controle de versão de linha  
 Essencialmente suporte a carimbo de tempo, no qual as versões de linha são comparadas na hora da atualização.
