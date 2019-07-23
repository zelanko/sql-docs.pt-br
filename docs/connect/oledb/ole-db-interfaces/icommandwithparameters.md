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
ms.openlocfilehash: 205a93fe5ce57a8b4c10fffb8648a1ef4c7b6506
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015464"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Melhorias no mecanismo de banco de dados [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] começando com permitir ICommandWithParameters:: GetParameterInfo para obter descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por CommandWithParameters:: GetParameterInfo em versões anteriores [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]do. Para obter mais informações, veja [Descoberta de metadados](../../oledb/features/metadata-discovery.md).  
  
 Além disso, do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] em diante, ao chamar ICommandWithParameters::SetParameterInfo, o valor passado para o parâmetro *pwszName* precisa ser um identificador válido. Para obter mais informações, consulte [Database Identifiers](../../../relational-databases/databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
