---
title: Melhorias de data e hora (OLE DB)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
author: markingmyname
ms.author: maghan
ms.custom: seo-dt-2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7dadb038bcb77ee13abdbead023aed164cbe2a8b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306101"
---
# <a name="date-and-time-improvements-ole-db"></a>Melhorias de data e hora (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] apresenta novos tipos de dados de data e hora. Esta seção descreve como esses novos tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são expostos como extensões no Cliente Nativo. Para obter uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] visão geral do suporte ao Cliente Nativo para os novos tipos de dados de data e hora, consulte [Melhorias de data e hora](../../relational-databases/native-client/features/date-and-time-improvements.md). Para ver um exemplo, confira [Usar os recursos aprimorados de data e hora do &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md).  
  
 Para obter informações mais genéricas sobre os tipos de dados de data e hora, confira [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Suporte a tipos de dados para melhorias de data e hora do OLE DB](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 Fornece informações sobre os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos OLE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB (Native Client) que suportam tipos de dados de data e hora.  
  
 [Metadados &#40;OLE DB&#41;](https://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
 Contém informações sobre a estrutura DBBINDING, **ICommandWithParameters::GetParameterInfo**, **ICommandWithParameters::SetParameterInfo**, **IColumnsRowset::GetColumnsRowset** e I**ColumnsInfo::GetColumnInfo**. Também fornece informações sobre atualizações de conjuntos de linhas de esquemas OLE DB.  
  
 [Associações e conversões &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 Descreve as regras para conversão entre servidor e cliente de tipos de data novos e existentes.  
  
 [Alterações de cópia em massa para tipos de data e hora aprimorados &#40;OLE DB e ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Descreve aprimoramentos de data/hora para dar suporte a operações de cópia em massa.  
  
 [Suporte da API do OLE DB para aprimoramentos de data e hora](../../relational-databases/native-client-ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 Descreve as APIs OLE DB que dão suporte a recursos de data/hora aprimorados.  
  
 [Comparações de IRowsetFind](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 Descreve os tipos de data/hora e **IRowsetFind**.  
  
 [Novos recursos de data e hora com versões anteriores do servidor SQL &#40;o OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 Descreve o comportamento esperado quando um aplicativo cliente que usa recursos de data e hora aprimorados se comunica com uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quando um cliente compilado com uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client envia comandos para um servidor que dá suporte a recursos de data e hora aprimorados.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
