---
title: As mensagens retornadas pelo Driver ODBC para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- error messages [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], error messages
ms.assetid: 150bde1d-adb6-4e77-90e9-4dc93499a746
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 067300b35282b39c63504f6f8e3a16fd3e1a8c00
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>Mensagens retornadas pelo Driver ODBC para Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Se uma mensagem de erro do Oracle estiver disponível, ele será retornado precedidas pelo [Microsoft], [ODBC Driver for Oracle] e as marcas [Oracle]; Caso contrário, a mensagem for retornada sem a marca [Oracle] como nos exemplos a seguir:  
  
## <a name="oracle-error-message"></a>Mensagem de erro do Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>Driver ODBC para mensagem de erro do Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle]  
```
