---
title: Suporte para o modelo de simultaneidade (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597d1022fa6946e0ae768cb9600a3f4534c67a25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080690"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Modelo de simultaneidade com suporte (Driver ODBC do Visual FoxPro)
O Driver de ODBC do Visual FoxPro suporta *simultaneidade somente leitura*. O aplicativo pode chamar [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) com uma opção de SQL_CONCURRENCY de SQL_CONCUR_READ_ONLY.  
  
 Para obter mais informações, consulte o [referência do programador de ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>simultaneidade de somente leitura  
 O cursor não pode ser atualizado.  
  
## <a name="row-versioning"></a>controle de versão de linha  
 Essencialmente, timestamp suporte, em qual linha versões são comparadas ao tempo de atualização.
