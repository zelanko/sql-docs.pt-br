---
title: SQLError (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLError function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8315ec16-1c22-447a-a577-39bd94f61070
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3014c5c2af1a0ef8e5f485c790089e4807834446
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47634044"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade com a API ODBC: Nível de núcleo  
  
 Retorna informações de erro ou de status sobre o último erro. O driver mantém uma pilha ou a lista de erros que podem ser retornadas para o *hstmt*, *hdbc*, e *henv* argumentos, dependendo de como a chamada para **SQLError**  é feita. A fila de erros é liberada após cada instrução.  
  
 A tabela a seguir descreve o **SQLError** argumentos e valores de retorno usados pelo driver.  
  
|Argumento SQLError|Descrição do valor de retorno|  
|-----------------------|------------------------------|  
|*szSQLState*|O valor para o SQLSTATE representado pelo erro.|  
|*pfNativeError*|Um valor diferente de zero indica um [Visual FoxPro ODBC Driver nativo mensagem de erro](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md). Um valor de zero indica o erro foi detectado pelo driver e mapeado para o apropriada [código de erro de ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).|  
|*szErrorMsg*|O texto do erro nativo ou um erro de ODBC.|  
|*pcbErrorMsg*|O comprimento do texto da mensagem mais o comprimento dos identificadores.|  
  
 Para obter mais informações sobre mensagens de erro de driver, consulte [visão geral de mensagens de erro](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md). Para obter mais informações sobre essa função, consulte [SQLError](../../odbc/reference/syntax/sqlerror-function.md) na *referência do programador de ODBC*.
