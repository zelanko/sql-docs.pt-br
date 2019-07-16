---
title: SQLGetConnectOption (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5703eb39-f3b2-4f3a-8676-a5625ae29a41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c17cd473d3c96032817c2b183bf65fe360cf3cdc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053679"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Parcial  
  
 Conformidade com a API ODBC: Nível 1  
  
 Retorna a configuração atual de uma opção de conexão. Essa função tem suporte parcial: O driver dá suporte a todos os valores para o *fOption* argumento mas não oferece suporte a alguns dos *vParam* os valores para o *fOption* SQL_TXN_ISOLATION do argumento.  
  
 A tabela a seguir descreve apenas os argumentos com comportamento específico à implementação do Driver ODBC do Visual FoxPro **SQLGetConnectOption**.  
  
|*fOption*|Comentários|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Se você escolher SQL_AUTOCOMMIT_OFF, seu aplicativo deve confirmar ou reverter transações com explicitamente [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); o Driver de ODBC do Visual FoxPro não confirme automaticamente uma instrução transacionáveis após a conclusão. O driver de iniciar uma transação se a instrução for transacionáveis.|  
|SQL_CURRENT_QUALIFIER|Pode ser um nome de banco de dados (arquivo. dbc) totalmente qualificado ou um caminho totalmente qualificado para um diretório que contém zero ou mais tabelas (arquivos. dbf).|  
|SQL_LOGINTIMEOUT|Retorna o erro "Driver não têm a capacidade".|  
|SQL_CURSORS|Retorna o erro "Driver não têm a capacidade".|  
|SQL_PACKET_SIZE|Retorna o erro "Driver não têm a capacidade".|  
|SQL_TXN_ISOLATION|O driver permite apenas SQL_TXN_READ_COMMITTED.<br /><br /> O seguinte *vParam*s não têm suporte:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obter mais informações, consulte [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) na *referência do programador de ODBC*.
