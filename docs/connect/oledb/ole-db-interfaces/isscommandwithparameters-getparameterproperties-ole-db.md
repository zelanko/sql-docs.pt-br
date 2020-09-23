---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB) | Microsoft Docs
description: ISSCommandWithParameters::GetParameterProperties retorna uma matriz de estruturas do conjunto de propriedades no Driver do OLE DB para SQL Server, uma para cada parâmetro UDT ou XML.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8631c9c1beed054b57fd368dd567e3568c213b50
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862143"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Retorna uma matriz de estruturas de conjuntos de propriedades SSPARAMPROPS, um conjunto de propriedades SSPARAMPROPS para cada parâmetro XML ou UDT.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pcParams*[out][in]  
 Um ponteiro para a memória que contém o número de estruturas SSPARAMPROPS retornadas em *prgParamProperties*.  
  
 *prgParamProperties*[out]  
 Um ponteiro para memória na qual uma matriz de estrutura SSPARAMPROPS é retornada. O provedor aloca memória para as estruturas e retorna o endereço dessa memória; o consumidor libera essa memória com `IMalloc::Free` quando as estruturas não são mais necessárias. Antes de chamar `IMalloc::Free` para *prgParamProperties*, o consumidor também precisa chamar `VariantClear` para a propriedade *vValue* de cada estrutura DBPROP a fim de evitar a perda de memória, nos casos em que a variante contém um tipo de referência como um BSTR. Se *pcParams* for zero na saída ou se ocorrer um erro diferente de DB_E_ERRORSOCCURRED, o provedor não alocará nenhuma memória e garantirá que *prgParamProperties* seja um ponteiro nulo na saída.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O método `GetParameterProperties` retorna os mesmos códigos de erro do método `ICommandProperties::GetProperties` principal do OLE DB, exceto quando não é possível acionar DB_S_ERRORSOCCURRED e DB_E_ERRORSOCCURED.  
  
## <a name="remarks"></a>Comentários  
 O método `ISSCommandWithParameters::GetParameterProperties` se comporta de forma consistente em relação a `GetParameterInfo`. Se [`ISSCommandWithParameters::SetParameterProperties`](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) ou `SetParameterInfo` não tiver sido chamado ou se tiver sido chamado com cParams igual a zero, `GetParameterInfo` obterá e retornará as informações de parâmetro. Se `ISSCommandWithParameters::SetParameterProperties` ou `SetParameterInfo` tiver sido chamado para pelo menos um parâmetro, o método `ISSCommandWithParameters::GetParameterProperties` retornará propriedades apenas para os parâmetros para os quais `ISSCommandWithParameters::SetParameterProperties` foi chamado. Se `ISSCommandWithParameters::SetParameterProperties` for chamado após `ISSCommandWithParameters::GetParameterProperties` ou `GetParameterInfo`, as chamadas posteriores a `ISSCommandWithParameters::GetParameterProperties` retornarão os valores substituídos desses parâmetros para os quais o método `ISSCommandWithParameters::SetParameterProperties` foi chamado.  
  
 A estrutura SSPARAMPROPS é definida da seguinte maneira:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|*iOrdinal*|O ordinal do parâmetro passado.|  
|*cPropertySets*|O número de estruturas DBPROPSET em *rgPropertySets*.|  
|*rgPropertySets*|Um ponteiro para a memória no qual uma matriz de estruturas DBPROPSET deve ser retornada.|  
  
## <a name="see-also"></a>Consulte Também  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
