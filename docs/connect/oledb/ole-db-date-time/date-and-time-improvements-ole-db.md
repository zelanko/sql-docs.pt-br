---
title: Aprimoramentos de data e hora (OLE DB) | Microsoft Docs
description: Melhorias de data e hora (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 5518461fade08e6f23e1594056c284865957274c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66769336"
---
# <a name="date-and-time-improvements-ole-db"></a>Melhorias de data e hora (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] apresenta novos tipos de dados de data e hora. Esta seção descreve como esses novos tipos são expostos como extensões no Driver do OLE DB para SQL Server. Para uma visão geral do Driver do OLE DB para o suporte do SQL Server para a nova data e tipos de dados de tempo, consulte [aprimoramentos de data e hora](../../oledb/features/date-and-time-improvements.md). Para obter um exemplo, consulte [aprimorados de data de uso e recursos de tempo &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md).  
  
 Para obter mais informações sobre tipos de dados de data e hora, consulte [datetime &#40;Transact-SQL&#41;](../../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Suporte a tipos de dados para melhorias de data e hora do OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 Fornece informações sobre o OLE DB (OLE DB Driver para SQL Server) tipos que oferecem suporte [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados de data e hora.  
  
 [Metadados &#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
 Contém informações sobre a estrutura DBBINDING **ICommandWithParameters:: Getparameterinfo**, **ICommandWithParameters:: SetParameterInfo**, **IColumnsRowset:: GetColumnsRowset**e eu**ColumnsInfo::GetColumnInfo**. Também fornece informações sobre atualizações de conjuntos de linhas de esquemas OLE DB.  
  
 [Associações e conversões &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
 Descreve as regras para conversão entre servidor e cliente de tipos de data novos e existentes.  
  
 [Alterações de cópia em massa para tipos avançados de data e hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)  
 Descreve aprimoramentos de data/hora para dar suporte a operações de cópia em massa.  
  
 [Suporte da API do OLE DB para aprimoramentos de data e hora](../../oledb/ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 Descreve as APIs OLE DB que dão suporte a recursos de data/hora aprimorados.  
  
 [Comparações de IRowsetFind](../../oledb/ole-db-date-time/comparability-for-irowsetfind.md)  
 Descreve os tipos de data/hora e **IRowsetFind**.  
 
  
## <a name="see-also"></a>Consulte Também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
