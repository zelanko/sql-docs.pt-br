---
title: ISSCommandWithParameters (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bbdef1bda50ae2d5ace31b56f003e48f8b4bc86b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290084"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSCommandWithParameters** dá suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML e UDTs (tipos definidos pelo usuário). Esta é uma interface opcional que herda da interface OLE DB principal **ICommandWithParameters**. Além dos três métodos herdados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**e **SetParameterInfo**; **ISSCommandWithParameters** fornece dois novos métodos usados para identificar os tipos de dados específicas de servidor.  
  
> [!NOTE]  
>   A interface **ISSCommandWithParameters** pode ser usada quando são usados Componentes de Serviço, mas os próprios Componentes de Serviço não usarão esta interface.  
  
|Método|Descrição|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|Retorna uma estrutura de conjunto de propriedades **SSPARAMPROPS** na matriz para cada parâmetro UDT ou XML passado ao comando, mas nenhum é retornado para os outros tipos de parâmetros.|  
|[ISSCommandWithParameters::SetParameterProperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|Define as propriedades de parâmetro por parâmetro por ordinal ou define as propriedades de parâmetro em massa, especificando uma matriz de estruturas **SSPARAMPROPS** .|  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [Usando tipos de dados XML](../../relational-databases/native-client/features/using-xml-data-types.md)   
 [Usando tipos definidos pelo usuário](../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
