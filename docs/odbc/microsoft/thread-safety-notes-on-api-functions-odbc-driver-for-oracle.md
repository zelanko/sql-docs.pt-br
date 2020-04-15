---
title: Notas de segurança de rosca em funções de API (Driver ODBC para Oracle) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 489f0e99ea53d419ff94dddfeb22e37573abb874
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303067"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>Observações de segurança do thread em funções de API (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Driver Microsoft ODBC para Oracle é seguro para threads; no entanto, a Oracle não permite várias instruções simultâneas em uma única conexão. O motorista impõe essa restrição. Em outras palavras, em aplicativos multithreaded, embora qualquer segmento possa chamar o Driver ODBC para Oracle a qualquer momento, o driver bloqueia qualquer outro segmento do driver na mesma conexão até que o segmento original deixe o driver.  
  
 O motorista não bloqueia se houver duas declarações em duas conexões diferentes. No entanto, se houver uma única conexão com duas declarações, há potencial para bloqueio.
