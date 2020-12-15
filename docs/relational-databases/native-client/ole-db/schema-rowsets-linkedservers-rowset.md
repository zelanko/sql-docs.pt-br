---
description: Conjunto de linhas de esquema-LINKEDSERVERS Rowset no SQL Server Native Client
title: Conjunto de linhas LINKEDSERVERS (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- LINKEDSERVERS rowset
- enumerating data sources [OLE DB]
ms.assetid: 2633fd8a-65e7-498d-9aed-8e4b1cca2381
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c46ab596b058aa31254138d3454a1248c986f64e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467567"
---
# <a name="schema-rowsets---linkedservers-rowset-in-sql-server-native-client"></a>Conjunto de linhas de esquema-LINKEDSERVERS Rowset no SQL Server Native Client
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O conjunto de linhas **LINKEDSERVERS** enumera fontes de dados da organização que podem participar de consultas distribuídas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 O conjunto de linhas **LINKEDSERVERS** contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|DESCRIÇÃO|  
|-----------------|--------------------|-----------------|  
|SVR_NAME|DBTYPE_WSTR|Nome de um servidor vinculado.|  
|SVR_PRODUCT|DBTYPE_WSTR|Fabricante ou outro nome que identifique o tipo de repositório de dados representado pelo nome do servidor vinculado.|  
|SVR_PROVIDERNAME|DBTYPE_WSTR|Nome amigável do provedor OLE DB usado para consumir dados do servidor.|  
|SVR_DATASOURCE|DBTYPE_WSTR|Cadeia de caracteres OLE DB DBPROP_INIT_DATASOURCE usada para adquirir uma fonte de dados do provedor.|  
|SVR_PROVIDERSTRING|DBTYPE_WSTR|Valor DBPROP_INIT_PROVIDERSTRING do OLE DB usado para adquirir uma fonte de dados do provedor.|  
|SVR_LOCATION|DBTYPE_WSTR|Cadeia de caracteres de DBPROP_INIT_LOCATION do OLE DB usada para adquirir uma fonte de dados do provedor.|  
  
 O conjunto de linhas é classificado em SRV_NAME, havendo suporte a uma única restrição em SRV_NAME.  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte ao conjunto de linhas de esquema &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)  
  
  
