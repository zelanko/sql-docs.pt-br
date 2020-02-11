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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597d1022fa6946e0ae768cb9600a3f4534c67a25
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68080690"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Modelo de simultaneidade com suporte (Driver ODBC do Visual FoxPro)
O driver ODBC do Visual FoxPro dá suporte à *simultaneidade somente leitura*. Seu aplicativo pode chamar [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) com uma opção SQL_CONCURRENCY de SQL_CONCUR_READ_ONLY.  
  
 Para obter mais informações, consulte a [referência do programador de ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>simultaneidade somente leitura  
 O cursor não pode ser atualizado.  
  
## <a name="row-versioning"></a>controle de versão de linha  
 Essencialmente suporte a carimbo de data/hora, em que versões de linha são comparadas no momento da atualização.
