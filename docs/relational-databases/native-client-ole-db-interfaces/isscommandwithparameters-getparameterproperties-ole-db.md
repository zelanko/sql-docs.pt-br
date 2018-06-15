---
title: 'Isscommandwithparameters:: Getparameterproperties (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 713169c273466260872ba29d65ab9c691dc5baf6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32949001"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Retorna uma matriz de estruturas de conjuntos de propriedades SSPARAMPROPS, um conjunto de propriedades SSPARAMPROPS para cada parâmetro XML ou UDT.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pcParams*[out] [in]  
 Um ponteiro de memória que contém o número de estruturas SSPARAMPROPS retornadas em *prgParamProperties*.  
  
 *prgParamProperties*[out]  
 Um ponteiro para memória na qual uma matriz de estrutura SSPARAMPROPS é retornada. O provedor aloca memória para as estruturas e retorna o endereço de memória; o consumidor libera esta memória com **IMalloc:: Free** quando ele não precisa mais as estruturas. Antes de chamar **IMalloc:: Free** para *prgParamProperties*, o consumidor também deve chamar **VariantClear** para o *vValue* propriedade de cada estrutura DBPROP para evitar um vazamento de memória nos casos em que a variante contém um tipo de referência (como um BSTR.) Se *pcParams* é zero na saída ou ocorrer um erro diferente de DB_E_ERRORSOCCURRED, o provedor não alocará nenhuma memória e assegurará que *prgParamProperties* é um ponteiro nulo na saída.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O **GetParameterProperties** método retorna os mesmos códigos de erro como o núcleo de OLE DB **icommandproperties:: GetProperties** método, exceto que DB_S_ERRORSOCCURRED e DB_E_ERRORSOCCURED não pode ser gerado.  
  
## <a name="remarks"></a>Comentários  
 **Isscommandwithparameters:: Getparameterproperties** se comporta de forma consistente em relação ao **GetParameterInfo**. Se [isscommandwithparameters::](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) ou **SetParameterInfo** não foram chamados ou foram chamados com cParams igual a zero, **GetParameterInfo** derivará informações de parâmetro e retorna essa. Se **isscommandwithparameters::** ou **SetParameterInfo** tiverem sido chamados para pelo menos um parâmetro, **isscommandwithparameters:: Getparameterproperties** retorna propriedades apenas para os parâmetros para o qual **isscommandwithparameters::** foi chamado. Se **isscommandwithparameters::** é chamado após **isscommandwithparameters:: Getparameterproperties** ou **GetParameterInfo**, subsequentes chamadas para **isscommandwithparameters:: Getparameterproperties** retornar os valores substituídos desses parâmetros para o qual **isscommandwithparameters::** foi chamado.  
  
 A estrutura SSPARAMPROPS é definida da seguinte maneira:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Membro|Description|  
|------------|-----------------|  
|*iOrdinal*|O ordinal do parâmetro passado.|  
|*cPropertySets*|O número de estruturas DBPROPSET em *rgPropertySets*.|  
|*rgPropertySets*|Um ponteiro para a memória no qual uma matriz de estruturas DBPROPSET deve ser retornada.|  
  
## <a name="see-also"></a>Consulte também  
 [ISSCommandWithParameters & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
