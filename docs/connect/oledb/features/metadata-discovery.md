---
title: Descoberta de metadados | Microsoft Docs
description: Descoberta de metadados no Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 9c25ec01087c5a4808f7143f1e3d8706129c46ae
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47842904"
---
# <a name="metadata-discovery"></a>Descoberta de metadados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A melhoria na descoberta de metadados no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permite que aplicativos do OLE DB Driver for SQL Server garantam que os metadados de colunas ou de parâmetro retornados da execução de uma consulta sejam idênticos ou compatíveis com o formato de metadados especificado antes da execução da consulta. Você receberá um erro se os metadados retornados depois da execução da consulta não forem compatíveis com o formato de metadados especificado antes da execução da consulta.  
  
 Em interfaces bcp, IBCPSession e IBCPSession2, agora você pode especificar uma leitura atrasada (descoberta de metadados atrasada) para evitar a descoberta de metadados para operações de saída de consulta. Isso melhora o desempenho e elimina falhas de descoberta de metadados.  
  
 Se você desenvolver um aplicativo usando o OLE DB Driver for SQL Server, mas se conectar a uma versão de servidor anterior ao [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], a funcionalidade de descoberta de metadados corresponderá à versão do servidor.  
  
## <a name="remarks"></a>Remarks   
 As funções de membros OLE DB a seguir foram aperfeiçoadas no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] para fornecer descoberta de metadados aprimorada:  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters:: Getparameterinfo (consulte [ICommandWithParameters](../../oledb/ole-db-interfaces/icommandwithparameters.md) para obter mais informações)  
  
 Você também verá uma melhoria no desempenho ao especificar o formato de metadados usando IBCPSession::BCPSetBulkMode  
  
 A descoberta de metadados aprimorada no Driver do OLE DB para SQL Server é possível devido à adição de dois procedimentos armazenados no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
