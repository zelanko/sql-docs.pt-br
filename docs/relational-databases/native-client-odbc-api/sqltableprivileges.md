---
title: SQLTablePrivileges | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLTablePrivileges function
ms.assetid: 8cce22d5-28b1-4b50-a5bc-1de03e0ffd6b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d7a77eb5ea151c3a85f2235f48bb03d0e98dd9ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291894"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLTablePrivileges** pode ser executado em um cursor estático. Uma tentativa de executar **sqltablePrivileges** em um retorno updatable (orientado por keyset ou dinâmico) SQL_SUCCESS_WITH_INFO indicando que o tipo de cursor foi alterado.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte ao relatório de informações de tabelas em servidores vinculados, aceitando um nome de duas partes para o parâmetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLTablePrivileges] (https://go.microsoft.com/fwlink/?LinkId=59373\)   
 [ODBC API Implementation Details](~/relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
