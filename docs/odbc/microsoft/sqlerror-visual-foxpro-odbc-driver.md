---
title: SQLError (driver ODBC do Visual FoxPro) | Microsoft Docs
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
ms.openlocfilehash: d7e8a60030e9c5c7666ce3b25488cfc6adf00783
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053857"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível de núcleo  
  
 Retorna informações de erro ou de status sobre o último erro. O driver mantém uma pilha ou lista de erros que podem ser retornados para os argumentos *HSTMT*, *HDBC*e *HENV* , dependendo de como a chamada a **SqlError** é feita. A fila de erros é liberada após cada instrução.  
  
 A tabela a seguir descreve os argumentos do **SqlError** e os valores de retorno usados pelo driver.  
  
|Argumento SQLError|Descrição do valor de retorno|  
|-----------------------|------------------------------|  
|*szSQLState*|O valor para o SQLSTATE representado pelo erro.|  
|*pfNativeError*|Um valor diferente de zero indica uma [mensagem de erro nativo do driver ODBC do Visual FoxPro](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md). Um valor de zero indica que o erro foi detectado pelo driver e mapeado para o código de [erro ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)apropriado.|  
|*szErrorMsg*|O texto do erro nativo ou erro de ODBC.|  
|*pcbErrorMsg*|O comprimento do texto da mensagem mais o comprimento dos identificadores.|  
  
 Para obter mais informações sobre mensagens de erro de driver, consulte [visão geral de mensagens de erro](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md). Para obter mais informações sobre essa função, consulte [SqlError](../../odbc/reference/syntax/sqlerror-function.md) na *referência do programador de ODBC*.
