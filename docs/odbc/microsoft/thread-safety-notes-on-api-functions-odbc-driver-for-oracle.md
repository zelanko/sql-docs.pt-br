---
title: Notas de segurança de thread em funções de API (driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 926b2285bcce9a28579fffc4004c5454b2837392
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912432"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>Observações de segurança do thread em funções de API (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Microsoft ODBC driver for Oracle é thread-safe; no entanto, o Oracle não permite várias instruções simultâneas em uma única conexão. O driver impõe essa restrição. Em outras palavras, em aplicativos multissegmentados, embora qualquer thread possa chamar o driver ODBC para Oracle a qualquer momento, o driver bloqueia qualquer outro thread do driver na mesma conexão até que o thread original saia do driver.  
  
 O driver não bloqueará se houver duas instruções em duas conexões diferentes. No entanto, se houver uma única conexão com duas instruções, haverá potencial para o bloqueio.
