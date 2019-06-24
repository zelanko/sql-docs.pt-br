---
title: ICommandWithParameters | Microsoft Docs
description: Interface ICommandWithParameters
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 7194b886ed972937c30b775bb6ec093e1b4fe612
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66790617"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Melhorias no início de mecanismo de banco de dados com [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permitir ICommandWithParameters:: Getparameterinfo Obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por CommandWithParameters::GetParameterInfo nas versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Descoberta de metadados](../../oledb/features/metadata-discovery.md).  
  
 Além disso, do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] em diante, ao chamar ICommandWithParameters::SetParameterInfo, o valor passado para o parâmetro *pwszName* precisa ser um identificador válido. Para obter mais informações, consulte [Database Identifiers](../../../relational-databases/databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
