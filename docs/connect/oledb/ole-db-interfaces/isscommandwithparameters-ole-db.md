---
title: ISSCommandWithParameters (OLE DB) | Microsoft Docs
description: ISSCommandWithParameters (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd350eb8c63a95d0ba64950be2ab689696fef0e5
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2018
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSCommandWithParameters** interface expõe o suporte para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML e tipos definidos pelo usuário (UDT). É uma interface opcional que herda da interface OLE DB **ICommandWithParameters**. Além dos três métodos herdados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, e **SetParameterInfo**; **ISSCommandWithParameters** fornece dois novos métodos que são usados para manipular tipos de dados específicos do servidor.  
  
> [!NOTE]  
>  O **ISSCommandWithParameters** interface pode ser usada quando os componentes de serviço são usados, mas os componentes de serviço não usar essa interface.  
  
|Método|Description|  
|------------|-----------------|  
|[Isscommandwithparameters:: Getparameterproperties &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|Retorna uma estrutura de conjunto de propriedades **SSPARAMPROPS** na matriz para cada parâmetro UDT ou XML passado ao comando, mas nenhum é retornado para os outros tipos de parâmetros.|  
|[Isscommandwithparameters:: &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|Define as propriedades de cada parâmetro por ordinal ou define as propriedades de parâmetro em massa especificando uma matriz de estruturas **SSPARAMPROPS** .|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [Usando tipos de dados XML](../../oledb/features/using-xml-data-types.md)   
 [Usando tipos definidos pelo usuário](../../oledb/features/using-user-defined-types.md)  
  
  
