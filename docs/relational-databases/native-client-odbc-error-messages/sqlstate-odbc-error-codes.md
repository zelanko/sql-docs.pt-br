---
title: SQLSTATE (códigos de erro ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 40ff6e7e20eab35aabeddec634aa2939484cfdd2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414925"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de erro ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLSTATE fornece informações detalhadas sobre a causa de um aviso ou um erro. Para erros que ocorrem nos dados de origem detectados e retornados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client mapeia o número de erro nativo retornado para o SQLSTATE apropriado. Se um número de erro nativo não tiver um código de erro ODBC para mapear para o, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client retornará SQLSTATE 42000 ("sintaxe ou violação de acesso"). Para erros que são detectados pelo driver, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client gera o SQLSTATE apropriado.  
  
 Para obter mais informações sobre códigos de erro de estado, consulte os seguintes tópicos:  
  
-   [Apêndice A: Códigos de erro ODBC](http://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [Mapeamentos SQLSTATE](http://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>Consulte também  
 [Tratando de erros e mensagens](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
