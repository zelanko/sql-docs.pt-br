---
title: SQLSTATE (códigos de erro ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 253841e26ab7ecbeafb2cfeeed8c090c91650d14
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62805860"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de erro ODBC)
  SQLSTATE fornece informações detalhadas sobre a causa de um aviso ou um erro. Para erros que ocorrem na fonte de dados detectada e retornada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]pelo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o driver ODBC do Native Client mapeia o número de erro nativo retornado para o SQLSTATE apropriado. Se um número de erro nativo não tiver um código de erro ODBC para mapear, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o driver ODBC do Native Client retornará SQLSTATE 42000 ("erro de sintaxe ou violação de acesso"). Para erros detectados pelo driver, o driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Native Client gera o SQLSTATE apropriado.  
  
 Para obter mais informações sobre códigos de erro de estado, consulte os seguintes tópicos:  
  
-   [Apêndice A: Códigos de erro ODBC](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [Mapeamentos de SQLSTATE](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>Consulte Também  
 [Tratando de erros e mensagens](handling-errors-and-messages.md)  
  
  
