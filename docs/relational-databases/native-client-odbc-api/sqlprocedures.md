---
title: Procedimentos SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 14ff76504c9a36657be60ba4855cf252474071d7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302352"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Todos os procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornam um valor. **SQLProcedures** relata SQL_PT_FUNCTION para a coluna de resultados PROCEDURE_TYPE.  
  
 **O SQLProcedures** retorna SQL_SUCCESS se existem ou não valores para os parâmetros *CatalogName, SchemaName* ou *ProcName.* **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 **SQLProcedimentoes** podem ser executados em um cursor de servidor estático. Uma tentativa de executar **SQLProcedures** em um cursor updatable (dinâmico ou keyset) retornará SQL_SUCCESS_WITH_INFO, indicando que o tipo de cursor foi alterado.  
  
 **O SQLProcedures** retorna informações sobre quaisquer procedimentos cujos nomes correspondam ao *ProcName* e podem ser executados pelo usuário atual, ou para os quais o usuário atual recebeu permissão DE DEFINIÇÃO DE EXIBIÇÃO.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLProcedures](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
