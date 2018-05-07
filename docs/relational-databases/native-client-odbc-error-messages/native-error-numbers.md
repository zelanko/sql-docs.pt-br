---
title: Números de erro nativo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-error-messages
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 54b70862d1fdcfff159f288a97f8031e6f26ff69
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="native-error-numbers"></a>Números de erro nativos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Para erros que ocorrem na fonte de dados (retornado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client retorna o número de erro nativo retornado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para erros detectados pelo driver, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client retorna um número de erro nativo 0. Para obter mais informações sobre uma lista de números de erro nativo, consulte a coluna de erro do **sysmessages** tabela do sistema de **mestre** banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter informações sobre os códigos de erro de estado, consulte [SQLSTATE &#40;códigos de erro de ODBC&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md). Para erros retornados pela Biblioteca de Rede, o número de erro nativo é do software de rede subjacente.  
  
## <a name="see-also"></a>Consulte também  
 [Tratando de erros e mensagens](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
