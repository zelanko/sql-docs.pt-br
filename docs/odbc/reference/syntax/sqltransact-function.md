---
title: "Função SQLTransact | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLTransact
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLTransact
helpviewer_keywords: SQLTransact function [ODBC]
ms.assetid: 496249e0-8eff-4c60-8358-5543bc3ead9c
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4aa10349035d7a9d5d16c979701c39ead96e8f2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqltransact-function"></a>Função SQLTransact
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: Deprecated  
  
 **Resumo**  
 Em ODBC 3. *x*, o ODBC 2*. x* função **SQLTransact** foi substituído pelo **SQLEndTran**. Para obter mais informações, consulte [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  Não há suporte para o atributo SQL_ASYNC_DBC_FUNCTION_ENABLE, que foi introduzida no ODBC 3.8, por **SQLTransact**. Aplicativos usando uma operação assíncrona em um identificador de conexão devem usar **SQLEndTran**.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
