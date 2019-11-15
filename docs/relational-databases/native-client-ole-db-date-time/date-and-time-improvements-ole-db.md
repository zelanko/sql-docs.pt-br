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
author: MightyPen
ms.author: genemi
ms.custom: seo-dt-2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 35b7629b6c31da805c8284c7c1a7c80d561fe7e3
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095445"
---
# <a name="date-and-time-improvements-ole-db"></a>Melhorias de data e hora (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] apresenta novos tipos de dados de data e hora. Esta seção descreve como esses novos tipos são expostos como extensões no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para obter uma visão geral do suporte ao cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para os novos tipos de dados de data e hora, consulte [melhorias de data e hora](../../relational-databases/native-client/features/date-and-time-improvements.md). Para obter um exemplo, consulte [ &#40;usar recursos aprimorados de data&#41;e hora OLE DB](../../relational-databases/native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md).  
  
 Para obter mais informações gerais sobre tipos de dados de data e hora, consulte [ &#40;DateTime&#41;Transact-SQL](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Suporte a tipos de dados para melhorias de data e hora do OLE DB](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 Fornece informações sobre tipos de OLE DB ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) que dão suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados de data e hora.  
  
 [OLE DB &#40;de metadados&#41;](https://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
 Contém informações sobre a estrutura DBBINDING, **ICommandWithParameters:: GetParameterInfo**, **ICommandWithParameters:: SetParameterInfo**, **IColumnsRowset:: GetColumnsRowset**e I**ColumnsInfo:: GetColumnInfo** . Também fornece informações sobre atualizações de conjuntos de linhas de esquemas OLE DB.  
  
 [Associações e conversões &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 Descreve as regras para conversão entre servidor e cliente de tipos de data novos e existentes.  
  
 [Alterações de cópia em massa para tipos &#40;de data e hora aprimorados OLE DB e ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Descreve aprimoramentos de data/hora para dar suporte a operações de cópia em massa.  
  
 [Suporte da API do OLE DB para aprimoramentos de data e hora](../../relational-databases/native-client-ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 Descreve as APIs OLE DB que dão suporte a recursos de data/hora aprimorados.  
  
 [Comparações de IRowsetFind](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 Descreve os tipos de data/hora e **IRowsetFind**.  
  
 [Novos recursos de data e hora com versões &#40;anteriores do SQL Server OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 Descreve o comportamento esperado quando um aplicativo cliente que usa recursos de data e hora aprimorados se comunica com uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quando um cliente compilado com uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client envia comandos para um servidor que dá suporte a recursos de data e hora aprimorados.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
