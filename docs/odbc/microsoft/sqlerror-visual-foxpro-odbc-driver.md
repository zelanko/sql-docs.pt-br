---
title: SQLError (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLError function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8315ec16-1c22-447a-a577-39bd94f61070
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 46696509f9276ac4974604c931c4d77acbaae15b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do Driver ODBC do Visual FoxPro. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 ODBC API conformidade: Nível de núcleo  
  
 Retorna informações de erro ou de status sobre o último erro. O driver mantém uma pilha ou a lista de erros que podem ser retornadas para o *hstmt*, *hdbc*, e *henv* argumentos, dependendo de como a chamada para **SQLError ** é feita. A fila de erros é liberada após cada instrução.  
  
 A tabela a seguir descreve o **SQLError** argumentos e valores de retorno usados pelo driver.  
  
|Argumento SQLError|Descrição do valor de retorno|  
|-----------------------|------------------------------|  
|*szSQLState*|O valor para o SQLSTATE representado pelo erro.|  
|*pfNativeError*|Um valor diferente de zero indica um [Visual FoxPro ODBC Driver nativo mensagem de erro](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md). Um valor de zero indica o erro foi detectado pelo driver e mapeado para as [código de erro de ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).|  
|*szErrorMsg*|O texto do erro nativo ou um erro de ODBC.|  
|*pcbErrorMsg*|O comprimento do texto da mensagem mais o comprimento dos identificadores.|  
  
 Para obter mais informações sobre mensagens de erro do driver, consulte [visão geral de mensagens de erro](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md). Para obter mais informações sobre essa função, consulte [SQLError](../../odbc/reference/syntax/sqlerror-function.md) no *referência do programador de ODBC*.
