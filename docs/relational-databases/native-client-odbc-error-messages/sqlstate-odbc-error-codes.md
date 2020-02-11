---
title: SQLSTATE (códigos de erro ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 162f6ff15a95c1839ef59b10c659935b687aeb59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783216"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de erro ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSTATE fornece informações detalhadas sobre a causa de um aviso ou um erro. Para erros que ocorrem na fonte de dados detectada e retornada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]pelo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o driver ODBC do Native Client mapeia o número de erro nativo retornado para o SQLSTATE apropriado. Se um número de erro nativo não tiver um código de erro ODBC para mapear, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o driver ODBC do Native Client retornará SQLSTATE 42000 ("erro de sintaxe ou violação de acesso"). Para erros detectados pelo driver, o driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Native Client gera o SQLSTATE apropriado.  
  
 Para obter mais informações sobre códigos de erro de estado, consulte os seguintes tópicos:  
  
-   [Apêndice A: Códigos de erro ODBC](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [Mapeamentos de SQLSTATE](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>Consulte Também  
 [Tratando de erros e mensagens](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
