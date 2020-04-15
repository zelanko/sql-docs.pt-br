---
title: SQLSETConnectOption (driver Visual FoxPro ODBC) | Microsoft Docs
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
ms.openlocfilehash: 2af208663f1e91250faad0ca9538b76bcec43b06
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301497"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Parcial  
  
 Conformidade da API ODBC: Nível 1  
  
 Define opções que regem aspectos das conexões. Esta função é parcialmente suportada: O driver suporta todos os valores para o argumento *fOption,* mas não suporta alguns dos valores *vParam* para o argumento *fOption* SQL_TXN_ISOLATION.  
  
 A tabela a seguir descreve apenas os argumentos com comportamento específico para a implementação do Driver Visual FoxPro ODBC do **SQLSetConnectOption**.  
  
|*fOpção*|Comentários|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Se você escolher SQL_AUTOCOMMIT_OFF, seu aplicativo deve confirmar ou reverter explicitamente as transações com [o SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); o Visual FoxPro ODBC Driver não comete automaticamente uma declaração transacível após a conclusão. O motorista inicia uma transação se a declaração for transacível.|  
|SQL_CURRENT_QUALIFIER|Pode ser um nome de [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) totalmente qualificado ou caminho totalmente qualificado para um diretório contendo zero ou mais [tabelas gratuitas](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SQL_LOGINTIMEOUT|Retorna erro "Driver não é capaz".|  
|SQL_CURSORS|Retorna erro "Driver não é capaz".|  
|SQL_PACKET_SIZE|Retorna erro "Driver não é capaz".|  
|SQL_TXN_ISOLATION|O motorista só permite SQL_TXN_READ_COMMITTED.<br /><br /> Os *seguintes vParam*s não são suportados:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obter mais informações, consulte [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) na *referência do programador ODBC*.
