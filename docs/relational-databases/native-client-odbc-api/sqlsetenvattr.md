---
title: SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0c968499ab546d4e2aeb168cb6a039618eb3d5bc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63014208"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  A [referência do programador de ODBC](https://go.microsoft.com/fwlink/?LinkId=45250) define como os drivers de ODBC devem interpretar as especificações de atributos de **SQLSetEnvAttr** de aplicativos criados para a API do ODBC 2.*x* ou do ODBC 3.*x* . O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client obedece a essas regras.  
  
 Um dos atributos controlados por **SQLSetEnvAttr** é se o pool de conexões deve ser usado. Se o pool de conexões for usado com o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, o parâmetro *DriverCompletion* deverá ser definido como SQL_DRIVER_NOPROMPT ao fazer a conexão com [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) ou **SQLConnect**.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLSetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
