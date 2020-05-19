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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b9612fbd7dd50ffeec812532e25a63eecca26571
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705359"
---
# <a name="native-error-numbers"></a>Números de erro nativos
  Para erros que ocorrem na fonte de dados (retornada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client retorna o número de erro nativo retornado a ele pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para erros detectados pelo driver, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client retorna um número de erro nativo de 0. Para obter mais informações sobre uma lista de números de erro nativos, consulte a coluna erro da tabela do sistema **sysmessages** no banco de dados **mestre** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obter informações sobre os códigos de erro de estado, consulte [SQLSTATE &#40;códigos de erro ODBC&#41;](sqlstate-odbc-error-codes.md). Para erros retornados pela Biblioteca de Rede, o número de erro nativo é do software de rede subjacente.  
  
## <a name="see-also"></a>Consulte Também  
 [Tratando de erros e mensagens](handling-errors-and-messages.md)  
  
  
