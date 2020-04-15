---
title: Opções de conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25cfe2a897b0c312f91cd0c1e41ad6fa11725ab8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281304"
---
# <a name="connect-options"></a>Opções de conexão
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Essas opções permitem a personalização da conexão de banco de dados dentro de um aplicativo.  
  
|Opção conectar|Observações|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|Se você escolher SQL_AUTOCOMMIT_OFF, seu aplicativo deve confirmar ou reverter explicitamente as transações com [o SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md).|  
|SQL_ODBC_CURSORS|Esse atributo de conexão é implementado no Driver Manager.|  
|SQL_OPT_TRACE|Esse atributo de conexão é implementado no Driver Manager.|  
|SQL_OPT_TRACEFILE|Esse atributo de conexão é implementado no Driver Manager.|  
|SQL_TRANSLATE_DLL|Erro de retorno: "Driver não é capaz".|  
|SQL_TRANSLATE_OPTION|Um valor de 32 bits passou para a tradução .dll.|  
|SQL_TXN_ISOLATION|O motorista só permite SQL_TXN_READ_COMMITTED.<br /><br /> Os seguintes vParams não são suportados:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|Este atributo de conexão ODBC 3.0 permite que você use o Driver ODBC para Oracle em transações distribuídas coordenadas pelo Microsoft Component Services (ou MTS, se você estiver usando o Windows NT). Ele fornece o ponteiro de interface *pITransaction* para a transação como o argumento *vParam.*|  
|SQL_ATTR_CONNECTION_DEAD|Este atributo de conexão ODBC 3.5 somente leitura permite determinar se a conexão com o servidor Oracle falhou. Obter apenas; não pode definir.|
