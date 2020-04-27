---
title: Aprimoramentos de data e hora (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1dec9e1281d2ff61dcab9312cdf5a7ad1ecb8da3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62866828"
---
# <a name="date-and-time-improvements-ole-db"></a>Melhorias de data e hora (OLE DB)
  O [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] apresenta novos tipos de dados de data e hora. Esta seção descreve como esses novos tipos são expostos como extensões no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para obter uma visão geral [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do suporte de cliente nativo para os novos tipos de dados de data e hora, consulte [melhorias de data e hora](../native-client/features/date-and-time-improvements.md). Para ver um exemplo, confira [Usar os recursos aprimorados de data e hora do &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md).  
  
 Para obter informações mais genéricas sobre os tipos de dados de data e hora, confira [datetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Suporte a tipos de dados para melhorias de data e hora do OLE DB](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 Fornece informações sobre os tipos[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB (cliente nativo) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que dão suporte aos tipos de dados de data e hora.  
  
 [Metadados &#40;OLE DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
 Contém informações sobre a estrutura DBBINDING, `ICommandWithParameters::GetParameterInfo` `ICommandWithParameters::SetParameterInfo` `IColumnsRowset::GetColumnsRowset`,, e I`ColumnsInfo::GetColumnInfo`. Também fornece informações sobre atualizações para OLE DB conjuntos de linhas de esquema.  
  
 [Associações e conversões &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 Descreve as regras para conversão entre servidor e cliente de tipos de data novos e existentes.  
  
 [Alterações de cópia em massa para tipos de data e hora aprimorados &#40;OLE DB e ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Descreve aprimoramentos de data/hora para dar suporte a operações de cópia em massa.  
  
 [Suporte da API do OLE DB para aprimoramentos de data e hora](ole-db-api-support-for-date-and-time-enhancements.md)  
 Descreve as APIs OLE DB que dão suporte a recursos de data/hora aprimorados.  
  
 [Comparações de IRowsetFind](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 Descreve os tipos de data/hora e `IRowsetFind`.  
  
 [Novos recursos de data e hora com versões anteriores do SQL Server &#40;OLE DB&#41;](new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 Descreve o comportamento esperado quando um aplicativo cliente que usa recursos de data e hora aprimorados se comunica com uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quando um cliente compilado com uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client envia comandos para um servidor que dá suporte a recursos de data e hora aprimorados.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
