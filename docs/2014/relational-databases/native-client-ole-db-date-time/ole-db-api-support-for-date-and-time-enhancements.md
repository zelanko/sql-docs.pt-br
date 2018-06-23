---
title: Suporte de API do OLE DB para data e hora aprimoramentos | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, date/time improvements
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2bf7eee4dd2517d4ff9c9f871160ba0515b18ce8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122824"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Suporte de API do OLE DB para data e hora aprimoramentos
  O suporte das APIs do OLE DB a seguir aprimorou os recursos de data/hora.  
  
|Função|Description|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Um sinalizador é adicionado à estrutura DBBINDING para permitir que aplicativos façam discriminação entre valores `datetime`, `datetime2` e `smalldatetime`. Para obter mais informações, consulte [parâmetro e Rowset Metadata](metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Para obter mais informações, consulte [alterações de cópia em massa para tipos aprimorados de data e hora &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).|  
|ICommandWithParameters::GetParameterInfo|Para obter mais informações, consulte[parâmetro e Rowset Metadata](metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Para obter mais informações, consulte[parâmetro e Rowset Metadata](metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para obter mais informações, consulte[parâmetro e Rowset Metadata](metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para obter mais informações, consulte[parâmetro e Rowset Metadata](metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Para obter detalhes sobre os conjuntos de linhas de esquema afetados, consulte[data e hora e conjuntos de linhas de esquema](../native-client-ole-db-rowsets/rowsets.md).|  
|IRowsetFastLoad|Essa interface dá suporte aos novos tipos de data/hora, mas não passou por nenhuma alteração.|  
|ITableDefinition::CreateTable|Para obter mais informações, consulte [suporte de tipo de dados para aprimoramentos de hora e data do OLE DB](data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Data e hora melhorias &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  