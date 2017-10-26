---
title: "Opções de conexão | Microsoft Docs"
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
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bb45857d47ef145c5693f6718696cbf75ccd666
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="connect-options"></a>Opções de conexão
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Essas opções permitem a personalização da conexão de banco de dados dentro de um aplicativo.  
  
|Opção de conexão|Observações|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|Se você escolher SQL_AUTOCOMMIT_OFF, seu aplicativo deve confirmar ou reverter transações com explicitamente [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md).|  
|SQL_ODBC_CURSORS|Esse atributo de conexão é implementado no Gerenciador de Driver.|  
|SQL_OPT_TRACE|Esse atributo de conexão é implementado no Gerenciador de Driver.|  
|SQL_OPT_TRACEFILE|Esse atributo de conexão é implementado no Gerenciador de Driver.|  
|SQL_TRANSLATE_DLL|Retorna o erro: "O Driver não funciona."|  
|SQL_TRANSLATE_OPTION|Um valor de 32 bits é passado para o arquivo. dll de conversão.|  
|SQL_TXN_ISOLATION|O driver permite apenas SQL_TXN_READ_COMMITTED.<br /><br /> Não há suporte para os vParams a seguir:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|Esse atributo de conexão ODBC 3.0 permite que você use o Driver ODBC para Oracle em transações distribuídas coordenadas por serviços de componentes da Microsoft (ou MTS, se você estiver usando o Windows NT). Ele fornece o ponteiro de interface *pITransaction* para a transação como o *vParam* argumento.|  
|SQL_ATTR_CONNECTION_DEAD|Esse atributo de conexão ODBC 3.5 somente leitura permite que você determine se a conexão para o servidor Oracle falhou. Obter. não é possível definir.|

