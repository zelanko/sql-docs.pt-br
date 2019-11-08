---
title: Alocando um identificador de ambiente | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eae9e11006a8a832523a7f72bdade6e943e57f50
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784740"
---
# <a name="allocating-an-environment-handle"></a>Alocando um identificador de ambiente
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Antes que um aplicativo possa chamar qualquer função ODBC, ele deve inicializar o ambiente de ODBC e alocar um identificador de ambiente. Trata-se do identificador de contexto global e do espaço reservado para os demais identificadores no ODBC. Faça isso chamando **SQLAllocHandle** com o parâmetro *HandleType* definido como SQL_HANDLE_ENV e *InputHandle* definido como SQL_NULL_HANDLE.  
  
 Depois de alocar o identificador de ambiente, o aplicativo deve definir atributos de ambiente para indicar qual versão das chamadas de função ODBC será usada. Para usar o ODBC 3. *x* functions, chame [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) com o parâmetro *Attribute* definido como SQL_ATTR_ODBC_VERSION e *ValuePtr* definido como SQL_OV_ODBC3.  
  
## <a name="see-also"></a>Consulte também  
 [Comunicando- &#40;se com SQL Server ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
