---
title: SQLSetEnvAttr | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 868c4131a4f221f8ac567decb9833a91f5705f70
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  A [referência do programador de ODBC](http://go.microsoft.com/fwlink/?LinkId=45250) define como os drivers de ODBC devem interpretar as especificações de atributos de **SQLSetEnvAttr** de aplicativos criados para a API do ODBC 2.*x* ou do ODBC 3.*x* . O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client obedece a essas regras.  
  
 Um dos atributos controlados por **SQLSetEnvAttr** é se o pool de conexões deve ser usado. Se o pool de conexões for usado com o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, o parâmetro *DriverCompletion* deverá ser definido como SQL_DRIVER_NOPROMPT ao fazer a conexão com [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) ou **SQLConnect**.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLSetEnvAttr](http://go.microsoft.com/fwlink/?LinkId=59369)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
