---
title: SQLGetConnectOption (driver ODBC do Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053679"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: parcial  
  
 Conformidade da API ODBC: nível 1  
  
 Retorna a configuração atual de uma opção de conexão. Esta função tem suporte parcial: o driver dá suporte a todos os valores para o argumento *fOption* , mas não dá suporte a alguns valores de *vParam* para o argumento *fOption* SQL_TXN_ISOLATION.  
  
 A tabela a seguir descreve somente os argumentos com comportamento específico para a implementação do driver ODBC do Visual FoxPro de **SQLGetConnectOption**.  
  
|*fOption*|Comentários|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Se você escolher SQL_AUTOCOMMIT_OFF, seu aplicativo deverá confirmar explicitamente ou reverter transações com [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); o driver ODBC do Visual FoxPro não confirma automaticamente uma instrução de transação após a conclusão. O Driver iniciará uma transação se a instrução for proficada.|  
|SQL_CURRENT_QUALIFIER|Pode ser um nome de banco de dados totalmente qualificado (arquivo. DBC) ou um caminho totalmente qualificado para um diretório que contém zero ou mais tabelas (arquivos. dbf).|  
|SQL_LOGINTIMEOUT|Retorna o erro "driver sem capacidade".|  
|SQL_CURSORS|Retorna o erro "driver sem capacidade".|  
|SQL_PACKET_SIZE|Retorna o erro "driver sem capacidade".|  
|SQL_TXN_ISOLATION|O driver permite apenas SQL_TXN_READ_COMMITTED.<br /><br /> Os seguintes *vParam*s não têm suporte:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obter mais informações, consulte [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) na *referência do programador de ODBC*.
