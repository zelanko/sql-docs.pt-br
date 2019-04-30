---
title: Números de erro nativos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e7cd24a3eb1ccdeea1b6e6cbb97e2d0f222193f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63223495"
---
# <a name="native-error-numbers"></a>Números de erro nativos
  Para erros que ocorrem na fonte de dados (retornado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client retorna o número de erro nativo retornado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para erros detectados pelo driver, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client retorna um número de erro nativo 0. Para obter mais informações sobre uma lista de números de erro nativo, consulte a coluna de erro dos **sysmessages** tabela do sistema a **mestre** banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter informações sobre os códigos de erro de estado, consulte [SQLSTATE &#40;códigos de erro ODBC&#41;](sqlstate-odbc-error-codes.md). Para erros retornados pela Biblioteca de Rede, o número de erro nativo é do software de rede subjacente.  
  
## <a name="see-also"></a>Consulte também  
 [Tratando de erros e mensagens](handling-errors-and-messages.md)  
  
  
