---
title: Descoberta de metadados | Microsoft Docs
description: Descoberta de metadados no OLE DB Driver para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 4277773fd45be05980ec32b710f41ea0836315c6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="metadata-discovery"></a>Descoberta de metadados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A melhoria de descoberta de metadados no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permite que o OLE DB Driver para aplicativos do SQL Server garantir que essa coluna ou retornados da execução de uma consulta de metadados de parâmetro sejam idênticos ou compatíveis com o formato de metadados especificado antes de execução da consulta. Você receberá um erro se os metadados retornados depois da execução da consulta não forem compatíveis com o formato de metadados especificado antes da execução da consulta.  
  
 No bcp e interfaces IBCPSession e IBCPSession2, agora você pode especificar um atraso leitura (descoberta de metadados atrasada) para evitar a descoberta de metadados para operações de saída de consulta. Isso melhora o desempenho e elimina falhas de descoberta de metadados.  
  
 Se você desenvolver um aplicativo usando o Driver do OLE DB para SQL Server, mas se conectar a uma versão de servidor anterior ao [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], descoberta de metadados corresponderá a funcionalidade para a versão do servidor.  
  
## <a name="remarks"></a>Remarks   
 As funções de membros OLE DB a seguir foram aperfeiçoadas no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] para fornecer descoberta de metadados aprimorada:  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters:: Getparameterinfo (consulte [ICommandWithParameters](../../oledb/ole-db-interfaces/icommandwithparameters.md) para obter mais informações)  
  
 Você também verá uma melhoria de desempenho ao especificar o formato de metadados usando IBCPSession::BCPSetBulkMode  
  
 A descoberta de metadados aprimorada no OLE DB Driver para SQL Server é possível devido à adição de dois procedimentos armazenados em [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
