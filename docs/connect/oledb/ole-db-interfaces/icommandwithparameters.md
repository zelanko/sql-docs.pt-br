---
title: ICommandWithParameters | Microsoft Docs
description: Interface ICommandWithParameters
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: ea2a3882a6f5b781df2ac42431d990e3ee1037f5
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43026645"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Melhorias no início de mecanismo de banco de dados com [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permitir ICommandWithParameters:: Getparameterinfo Obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por CommandWithParameters::GetParameterInfo nas versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Descoberta de metadados](../../oledb/features/metadata-discovery.md).  
  
 Além disso, do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] em diante, ao chamar ICommandWithParameters::SetParameterInfo, o valor passado para o parâmetro *pwszName* precisa ser um identificador válido. Para obter mais informações, consulte [Database Identifiers](../../../relational-databases/databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
