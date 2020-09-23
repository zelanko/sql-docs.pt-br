---
title: Suporte da API para melhorias de data e hora (driver do OLE DB)
description: Saiba mais sobre as APIs do OLE DB que dão suporte a recursos avançados de data/hora, incluindo nomes e descrições de função.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8209c1b1ca6f3c00ce4cd10455c35c8b9d4dfad4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862356"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Suporte da API do OLE DB para melhorias de data e hora
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O suporte das APIs do OLE DB a seguir aprimorou os recursos de data/hora.  
  
|Função|DESCRIÇÃO|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Um sinalizador é adicionado à estrutura DBBINDING para permitir que os aplicativos façam a distinção entre valores **datetime**, **datetime2** e **smalldatetime**. Para obter mais informações, confira [Parâmetro e Metadados do Conjunto de linhas](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Para obter mais informações, confira [Efetuar a cópia em massa das alterações dos tipos avançados de data e hora no &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md).|  
|ICommandWithParameters::GetParameterInfo|Para obter mais informações, confira [Parâmetro e Metadados do Conjunto de Linhas](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Para obter mais informações, confira [Parâmetro e Metadados do Conjunto de Linhas](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para obter mais informações, confira [Parâmetro e Metadados do Conjunto de Linhas](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para obter mais informações, confira [Parâmetro e Metadados do Conjunto de Linhas](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Para obter detalhes sobre os conjuntos de linhas dos esquema afetados, confira [Data e hora e conjuntos de linhas do esquema](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md).|  
|IRowsetFastLoad|Essa interface dá suporte aos novos tipos de data/hora, mas não passou por nenhuma alteração.|  
|ITableDefinition::CreateTable|Para obter mais informações, confira [Suporte a tipos de dados para aprimoramentos de data e hora do OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Melhorias de data e hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
