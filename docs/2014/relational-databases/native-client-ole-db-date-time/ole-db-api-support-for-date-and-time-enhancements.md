---
title: Suporte da API do OLE DB para melhorias de data e hora | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, date/time improvements
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef6334f6fe4671f2563add857f6dd58ce67a2840
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63237843"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Suporte da API do OLE DB para melhorias de data e hora
  O suporte das APIs do OLE DB a seguir aprimorou os recursos de data/hora.  
  
|Função|DESCRIÇÃO|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Um sinalizador é adicionado à estrutura DBBINDING para permitir que aplicativos façam discriminação entre valores `datetime`, `datetime2` e `smalldatetime`. Para obter mais informações, consulte [parâmetros e metadados de conjunto de linhas](metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Para obter mais informações, consulte [alterações de cópia em massa para tipos de data e hora aprimorados &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).|  
|ICommandWithParameters::GetParameterInfo|Para obter mais informações, consulte[parâmetros e metadados de conjunto de linhas](metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Para obter mais informações, consulte[parâmetros e metadados de conjunto de linhas](metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para obter mais informações, consulte[parâmetros e metadados de conjunto de linhas](metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para obter mais informações, consulte[parâmetros e metadados de conjunto de linhas](metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Para obter detalhes dos conjuntos de linhas de esquema afetados, consulte[data e hora e conjuntos de linhas de esquema](../native-client-ole-db-rowsets/rowsets.md).|  
|IRowsetFastLoad|Essa interface dá suporte aos novos tipos de data/hora, mas não passou por nenhuma alteração.|  
|ITableDefinition::CreateTable|Para obter mais informações, consulte [suporte de tipo de dados para OLE DB aprimoramentos de data e hora](data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Melhorias de data e hora &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
