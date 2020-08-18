---
description: SQLSetConnectOption (Driver ODBC do Visual FoxPro)
title: SQLSetConnectOption (driver ODBC do Visual FoxPro) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 683e767454d4056fd1114fc8796594aa91845ed3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411602"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: parcial  
  
 Conformidade da API ODBC: nível 1  
  
 Define opções que regem aspectos de conexões. Esta função tem suporte parcial: o driver dá suporte a todos os valores para o argumento *fOption* , mas não dá suporte a alguns valores de *vParam* para o argumento *fOption* SQL_TXN_ISOLATION.  
  
 A tabela a seguir descreve somente os argumentos com comportamento específico para a implementação do driver ODBC do Visual FoxPro de **SQLSetConnectOption**.  
  
|*fOption*|Comentários|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Se você escolher SQL_AUTOCOMMIT_OFF, seu aplicativo deverá confirmar explicitamente ou reverter transações com [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); o driver ODBC do Visual FoxPro não confirma automaticamente uma instrução de transação após a conclusão. O Driver iniciará uma transação se a instrução for proficada.|  
|SQL_CURRENT_QUALIFIER|Pode ser um nome de [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) totalmente qualificado ou um caminho totalmente qualificado para um diretório que contém zero ou mais [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SQL_LOGINTIMEOUT|Retorna o erro "driver sem capacidade".|  
|SQL_CURSORS|Retorna o erro "driver sem capacidade".|  
|SQL_PACKET_SIZE|Retorna o erro "driver sem capacidade".|  
|SQL_TXN_ISOLATION|O driver permite apenas SQL_TXN_READ_COMMITTED.<br /><br /> Os seguintes *vParam*s não têm suporte:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obter mais informações, consulte [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) na *referência do programador de ODBC*.
