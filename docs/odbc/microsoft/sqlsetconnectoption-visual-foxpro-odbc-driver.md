---
title: SQLSetConnectOption (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 398d098615a0453cb016286867836388fd817540
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631784"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: parcial  
  
 Conformidade com a API ODBC: 1 de nível  
  
 Define as opções que controlam aspectos de conexões. Essa função tem suporte parcial: O driver dá suporte a todos os valores para o *fOption* argumento mas não oferece suporte a alguns dos *vParam* os valores para o *fOption* argumento SQL_TXN_ISOLATION.  
  
 A tabela a seguir descreve apenas os argumentos com comportamento específico à implementação do Driver ODBC do Visual FoxPro **SQLSetConnectOption**.  
  
|*fOption*|Comentários|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Se você escolher SQL_AUTOCOMMIT_OFF, seu aplicativo deve confirmar ou reverter transações com explicitamente [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); o Driver de ODBC do Visual FoxPro não confirme automaticamente uma instrução transacionáveis após a conclusão. O driver de iniciar uma transação se a instrução for transacionáveis.|  
|SQL_CURRENT_QUALIFIER|Pode ser totalmente qualificado [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) nome ou caminho totalmente qualificado para um diretório que contém zero ou mais [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SQL_LOGINTIMEOUT|Retorna o erro "Não têm a capacidade de Driver".|  
|SQL_CURSORS|Retorna o erro "Não têm a capacidade de Driver".|  
|SQL_PACKET_SIZE|Retorna o erro "Não têm a capacidade de Driver".|  
|SQL_TXN_ISOLATION|O driver permite apenas SQL_TXN_READ_COMMITTED.<br /><br /> O seguinte *vParam*s não têm suporte:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obter mais informações, consulte [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) na *referência do programador de ODBC*.
