---
title: SQLError (visual FoxPro ODBC Driver) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0d1247217905187cfb2dbaca6d7b7b562d0175bd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298676"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível do núcleo  
  
 Retorna informações de erro ou status sobre o último erro. O driver mantém uma pilha ou lista de erros que podem ser devolvidos para os argumentos *hstmt*, *hdbc*e *henv,* dependendo de como a chamada para **SQLError** é feita. A fila de erros é lavada após cada declaração.  
  
 A tabela a seguir descreve os argumentos **sqlError** e os valores de retorno usados pelo driver.  
  
|Argumento SQLError|Descrição do valor de retorno|  
|-----------------------|------------------------------|  
|*szSQLState*|O valor do SQLSTATE representado pelo erro.|  
|*pfNativeError*|Um valor não zero indica uma [mensagem de erro nativa do driver Visual FoxPro ODBC](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md). Um valor de zero indica que o erro foi detectado pelo driver e mapeado para o [Código de Erro ODBC apropriado](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).|  
|*szErrorMsg*|O texto para o erro nativo ou erro ODBC.|  
|*pcbErrorMsg*|O comprimento do texto da mensagem mais o comprimento dos identificadores.|  
  
 Para obter mais informações sobre mensagens de erro do driver, consulte [Visão geral das mensagens de erro](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md). Para obter mais informações sobre essa função, consulte [SQLError](../../odbc/reference/syntax/sqlerror-function.md) na *referência do programador ODBC*.
