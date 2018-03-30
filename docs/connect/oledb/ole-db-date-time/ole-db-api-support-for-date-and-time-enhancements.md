---
title: Suporte de API do OLE DB para data e hora aprimoramentos | Microsoft Docs
description: Suporte da API OLE DB para aprimoramentos de data e hora
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b246db74888f8296a587d9edb38a224306baca92
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Suporte de API do OLE DB para data e hora aprimoramentos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O suporte das APIs do OLE DB a seguir aprimorou os recursos de data/hora.  
  
|Função|Description|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Um sinalizador é adicionado na estrutura DBBINDING para permitir que aplicativos façam discriminação entre **datetime**, **datetime2**, e **smalldatetime** valores. Para obter mais informações, consulte [parâmetro e Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Para obter mais informações, consulte [alterações de cópia em massa para tipos aprimorados de data e hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md).|  
|ICommandWithParameters::GetParameterInfo|Para obter mais informações, consulte[parâmetro e Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Para obter mais informações, consulte[parâmetro e Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para obter mais informações, consulte[parâmetro e Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para obter mais informações, consulte[parâmetro e Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Para obter detalhes sobre os conjuntos de linhas de esquema afetados, consulte[data e hora e conjuntos de linhas de esquema](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md).|  
|IRowsetFastLoad|Essa interface dá suporte aos novos tipos de data/hora, mas não passou por nenhuma alteração.|  
|ITableDefinition::CreateTable|Para obter mais informações, consulte [suporte de tipo de dados para aprimoramentos de hora e data do OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Data e hora melhorias &#40; OLE DB &#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
