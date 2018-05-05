---
title: ICommandWithParameters | Microsoft Docs
description: Interface ICommandWithParameters
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 52f14f27b313db701108f537b126fa9321fab971
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Melhorias no início de mecanismo de banco de dados com [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permitir ICommandWithParameters:: Getparameterinfo obter descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por CommandWithParameters::GetParameterInfo nas versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Metadata Discovery](../../oledb/features/metadata-discovery.md).  
  
 Também a partir do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], ao chamar ICommandWithParameters:: SetParameterInfo, o valor passado para o *pwszName* parâmetro deve ser um identificador válido. Para obter mais informações, consulte [Database Identifiers](../../../relational-databases/databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
