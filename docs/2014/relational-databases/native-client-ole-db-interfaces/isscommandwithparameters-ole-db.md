---
title: ISSCommandWithParameters (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4de7c6a99afcbd7db7c6e233fb737f129b536b8b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63209764"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters** dá suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML e UDTs (tipos definidos pelo usuário). Esta é uma interface opcional que herda da interface OLE DB principal **ICommandWithParameters**. Além dos três métodos herdados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**e **SetParameterInfo**; **ISSCommandWithParameters** fornece dois novos métodos usados para identificar os tipos de dados específicas de servidor.  
  
> [!NOTE]  
>   A interface **ISSCommandWithParameters** pode ser usada quando são usados Componentes de Serviço, mas os próprios Componentes de Serviço não usarão esta interface.  
  
|Método|Descrição|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|Retorna uma estrutura de conjunto de propriedades **SSPARAMPROPS** na matriz para cada parâmetro UDT ou XML passado ao comando, mas nenhum é retornado para os outros tipos de parâmetros.|  
|[ISSCommandWithParameters::SetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|Define as propriedades de parâmetro por parâmetro por ordinal ou define as propriedades de parâmetro em massa, especificando uma matriz de estruturas **SSPARAMPROPS** .|  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [Usando tipos de dados XML](../native-client/features/using-xml-data-types.md)   
 [Usando tipos definidos pelo usuário](../native-client/features/using-user-defined-types.md)  
  
  
