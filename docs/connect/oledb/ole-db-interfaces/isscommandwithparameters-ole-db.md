---
title: ISSCommandWithParameters (OLE DB) | Microsoft Docs
description: ISSCommandWithParameters (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 948650b7b50c4f79c46871900422ca44ea9e1455
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694134"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A interface **ISSCommandWithParameters** expõe o suporte a XML e UDTs (tipos definidos pelo usuário) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. É uma interface opcional que herda da interface OLE DB principal **ICommandWithParameters**. Além dos três métodos herdados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**e **SetParameterInfo**; **ISSCommandWithParameters** fornece dois novos métodos usados para identificar os tipos de dados específicos de servidor.  
  
> [!NOTE]  
>  A interface **ISSCommandWithParameters** pode ser usada quando os Componentes de Serviço são usados, mas os próprios Componentes de Serviço não usarão essa interface.  
  
|Método|Descrição|  
|------------|-----------------|  
|[Isscommandwithparameters:: Getparameterproperties &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|Retorna uma estrutura de conjunto de propriedades **SSPARAMPROPS** na matriz para cada parâmetro UDT ou XML passado ao comando, mas nenhum é retornado para os outros tipos de parâmetros.|  
|[Isscommandwithparameters:: SetParameterProperties &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|Define as propriedades de cada parâmetro por ordinal ou define as propriedades de parâmetro em massa especificando uma matriz de estruturas **SSPARAMPROPS** .|  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [Usando tipos de dados XML](../../oledb/features/using-xml-data-types.md)   
 [Usando tipos definidos pelo usuário](../../oledb/features/using-user-defined-types.md)  
  
  
