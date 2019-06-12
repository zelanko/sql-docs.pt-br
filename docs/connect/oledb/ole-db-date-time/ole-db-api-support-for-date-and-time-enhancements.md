---
title: Suporte da API do OLE DB para melhorias de data e hora | Microsoft Docs
description: Suporte da API do OLE DB para melhorias de data e hora
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 9819a16a60cc453b8f4277c0fe49053aeca59f48
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66769300"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Suporte da API do OLE DB para melhorias de data e hora
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O suporte das APIs do OLE DB a seguir aprimorou os recursos de data/hora.  
  
|Função|Descrição|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Um sinalizador é adicionado na estrutura DBBINDING para permitir que aplicativos façam discriminação entre **datetime**, **datetime2**, e **smalldatetime** valores. Para obter mais informações, consulte [Parameter and Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Para obter mais informações, consulte [alterações de cópia em massa para tipos aprimorada de data e hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md).|  
|ICommandWithParameters::GetParameterInfo|Para obter mais informações, consulte[Parameter and Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Para obter mais informações, consulte[Parameter and Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para obter mais informações, consulte[Parameter and Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para obter mais informações, consulte[Parameter and Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Para obter detalhes sobre os conjuntos de linhas de esquema afetados, consulte[data e hora e conjuntos de linhas de esquema](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md).|  
|IRowsetFastLoad|Essa interface dá suporte aos novos tipos de data/hora, mas não passou por nenhuma alteração.|  
|ITableDefinition::CreateTable|Para obter mais informações, consulte [suporte de tipo de dados para OLE DB aprimoramentos de data e hora](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Melhorias de data e hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
