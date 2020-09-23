---
title: ICommandWithParameters (driver do OLE DB) | Microsoft Docs
description: Saiba como os aprimoramentos permitem que ICommandWithParameters::GetParameterInfo obtenha descrições mais precisas dos resultados esperados para o Driver do OLE DB para SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21f3643737d1d6682133a252d52a072f73e81dfb
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861374"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Aprimoramentos no mecanismo de banco de dados desde o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permitem que ICommandWithParameters::GetParameterInfo obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por CommandWithParameters::GetParameterInfo em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Descoberta de metadados](../../oledb/features/metadata-discovery.md).  
  
 Além disso, do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] em diante, ao chamar ICommandWithParameters::SetParameterInfo, o valor passado para o parâmetro *pwszName* precisa ser um identificador válido. Para obter mais informações, consulte [Database Identifiers](../../../relational-databases/databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces do &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
