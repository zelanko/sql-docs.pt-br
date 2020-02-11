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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4358756deaa595ee5e10df0490522631201b9c87
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023368"
---
# <a name="connect-options"></a>Opções de conexão
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Essas opções permitem a personalização da conexão de banco de dados em um aplicativo.  
  
|Opção de conexão|Observações|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|Se você escolher SQL_AUTOCOMMIT_OFF, seu aplicativo deverá confirmar explicitamente ou reverter transações com [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md).|  
|SQL_ODBC_CURSORS|Esse atributo de conexão é implementado no Gerenciador de driver.|  
|SQL_OPT_TRACE|Esse atributo de conexão é implementado no Gerenciador de driver.|  
|SQL_OPT_TRACEFILE|Esse atributo de conexão é implementado no Gerenciador de driver.|  
|SQL_TRANSLATE_DLL|Retorna o erro: "driver sem capacidade".|  
|SQL_TRANSLATE_OPTION|Um valor de 32 bits passado para o translation. dll.|  
|SQL_TXN_ISOLATION|O driver permite apenas SQL_TXN_READ_COMMITTED.<br /><br /> Não há suporte para os seguintes vParams:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|Esse atributo de conexão ODBC 3,0 permite que você use o driver ODBC para Oracle em transações distribuídas coordenadas pelos serviços de componentes da Microsoft (ou MTS, se você estiver usando o Windows NT). Ele fornece o ponteiro de interface *pITransaction* para a transação como o argumento *vParam* .|  
|SQL_ATTR_CONNECTION_DEAD|Esse atributo de conexão ODBC 3,5 somente leitura permite que você determine se a conexão com o servidor Oracle falhou. Somente obtenção; Não é possível definir.|
