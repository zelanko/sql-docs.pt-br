---
title: Suporte de API do OLE DB para data e hora aprimoramentos | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: adfe174cd86bc99880d6942b8c83910f759eec38
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Suporte de API do OLE DB para data e hora aprimoramentos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O suporte das APIs do OLE DB a seguir aprimorou os recursos de data/hora.  
  
|Função|Description|  
|--------------|-----------------|  
|IAccessor:: CreateAccessor|Um sinalizador é adicionado na estrutura DBBINDING para permitir que aplicativos façam discriminação entre **datetime**, **datetime2**, e **smalldatetime** valores. Para obter mais informações, consulte [parâmetro e Rowset Metadata](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|Ibcpsession:: BCPColFmt|Para obter mais informações, consulte [alterações de cópia em massa para aprimorados de data e hora tipos &#40; OLE DB e ODBC &#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).|  
|ICommandWithParameters::GetParameterInfo|Para obter mais informações, consulte[parâmetro e Rowset Metadata](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|ICommandWithParameters:: SetParameterInfo|Para obter mais informações, consulte[parâmetro e Rowset Metadata](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para obter mais informações, consulte[parâmetro e Rowset Metadata](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para obter mais informações, consulte[parâmetro e Rowset Metadata](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset:: Getrowset|Para obter detalhes sobre os conjuntos de linhas de esquema afetados, consulte[data e hora e conjuntos de linhas de esquema](../../relational-databases/native-client-ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md).|  
|IRowsetFastLoad|Essa interface dá suporte aos novos tipos de data/hora, mas não passou por nenhuma alteração.|  
|Itabledefinition:: CreateTable|Para obter mais informações, consulte [suporte de tipo de dados para aprimoramentos de hora e data do OLE DB](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Data e hora melhorias &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
