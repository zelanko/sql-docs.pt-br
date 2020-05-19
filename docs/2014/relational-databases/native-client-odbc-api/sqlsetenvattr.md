---
title: SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 113c4508489e0f1dad8d134db7f86fc42371b456
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702155"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
  A [referência do programador de ODBC](https://go.microsoft.com/fwlink/?LinkId=45250) define como os drivers de ODBC devem interpretar as especificações de atributos de **SQLSetEnvAttr** de aplicativos criados para a API do ODBC 2.*x* ou do ODBC 3.*x* . O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client obedece a essas regras.  
  
 Um dos atributos controlados por **SQLSetEnvAttr** é se o pool de conexões deve ser usado. Se o pool de conexões for usado com o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, o parâmetro *DriverCompletion* deverá ser definido como SQL_DRIVER_NOPROMPT ao fazer a conexão com [SQLDriverConnect](sqldriverconnect.md) ou **SQLConnect**.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLSetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
