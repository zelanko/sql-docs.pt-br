---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d492a64b6d8a4e8ddf7de27067f1f0bcfef205e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62638078"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
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
 Um ponteiro para memória na qual uma matriz de estrutura SSPARAMPROPS é retornada. O provedor aloca memória para as estruturas e retorna o endereço para essa memória; o consumidor libera essa memória com **IMalloc:: Free** quando ela não precisa mais das estruturas. Antes de chamar **IMalloc:: Free** para *prgParamProperties*, o consumidor também deve chamar **VariantClear** para a propriedade *vValue* de cada estrutura DBPROP para evitar um vazamento de memória nos casos em que a variante contém um tipo de referência (como um BSTR). Se *pcParams* for zero na saída ou um erro diferente de DB_E_ERRORSOCCURRED ocorrer, o provedor não alocará memória e garantirá que *prgParamProperties* seja um ponteiro nulo na saída.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O método **ParameterProperties** retorna os mesmos códigos de erro que o método principal OLE DB **ICommandProperties:: GetProperties** , exceto que DB_S_ERRORSOCCURRED e DB_E_ERRORSOCCURED não podem ser gerados.  
  
## <a name="remarks"></a>Comentários  
 **ISSCommandWithParameters:: ParameterProperties** se comporta consistentemente em relação a **GetParameterInfo**. Se [ISSCommandWithParameters:: ParameterProperties](isscommandwithparameters-setparameterproperties-ole-db.md) ou **SetParameterInfo** não tiver sido chamado ou tiver sido chamado com cParams igual a zero, **GetParameterInfo** derivará informações de parâmetro e retornará isso. Se **ISSCommandWithParameters:: ParameterProperties** ou **SetParameterInfo** tiver sido chamado para pelo menos um parâmetro, **ISSCommandWithParameters:: ParameterProperties** retornará propriedades somente para os parâmetros para os quais **ISSCommandWithParameters:: ParameterProperties** foi chamado. Se **ISSCommandWithParameters:: ParameterProperties** for chamado após **ISSCommandWithParameters:: ParameterProperties** ou **GetParameterInfo**, as chamadas subsequentes para **ISSCommandWithParameters:: ParameterProperties** retornarão os valores substituídos para esses parâmetros para os quais **ISSCommandWithParameters:: ParameterProperties** foi chamado.  
  
 A estrutura SSPARAMPROPS é definida da seguinte maneira:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Membro|Descrição|  
|------------|-----------------|  
|*iOrdinal*|O ordinal do parâmetro passado.|  
|*cPropertySets*|O número de estruturas DBPROPSET em *rgPropertySets*.|  
|*rgPropertySets*|Um ponteiro para a memória no qual uma matriz de estruturas DBPROPSET deve ser retornada.|  
  
## <a name="see-also"></a>Consulte Também  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
