---
title: As mensagens retornadas pelo Driver ODBC para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], error messages
ms.assetid: 150bde1d-adb6-4e77-90e9-4dc93499a746
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bb2fc54692a77441bb2516ad72c0c44951152f56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045183"
---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>Mensagens retornadas pelo Driver ODBC para Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Se uma mensagem de erro Oracle estiver disponível, ele será retornado precedidos pelo [Microsoft], [Driver ODBC para Oracle,] e [Oracle] marcas; Caso contrário, a mensagem é retornada sem a marca [Oracle] como nos exemplos a seguir:  
  
## <a name="oracle-error-message"></a>Mensagem de erro do Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>Driver ODBC para mensagem de erro do Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle]  
```
