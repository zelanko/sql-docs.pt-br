---
title: 'Isscommandwithparameters:: Getparameterproperties (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f8e13ede890599c7424c2bb181a966608b09b0b5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686635"
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
 *pcParams*[out][in]  
 Um ponteiro para a memória que contém o número de estruturas SSPARAMPROPS retornadas em *prgParamProperties*.  
  
 *prgParamProperties*[out]  
 Um ponteiro para memória na qual uma matriz de estrutura SSPARAMPROPS é retornada. O provedor aloca memória para as estruturas e retorna o endereço para essa memória; o consumidor libera esta memória com **IMalloc:: Free** quando ele não precisa mais as estruturas. Antes de chamar **IMalloc:: Free** para *prgParamProperties*, o consumidor também deve chamar **VariantClear** para o *vValue* propriedade de cada estrutura DBPROP para evitar a perda de memória em casos em que a variante contém uma referência de tipo (por exemplo, um BSTR.) Se *pcParams* for zero na saída ou ocorrer um erro diferente de DB_E_ERRORSOCCURRED, o provedor não alocará nenhuma memória e assegurará que *prgParamProperties* é um ponteiro nulo na saída.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O **GetParameterProperties** método retorna os mesmos códigos de erro que o OLE DB de núcleo **icommandproperties:: GetProperties** os métodos, exceto que DB_S_ERRORSOCCURRED e DB_E_ERRORSOCCURED não podem ser gerado.  
  
## <a name="remarks"></a>Comentários  
 **Isscommandwithparameters:: Getparameterproperties** se comporta de forma consistente em relação às **GetParameterInfo**. Se [isscommandwithparameters:: SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) ou **SetParameterInfo** não foi chamado ou que foram chamados com cParams igual a zero, **GetParameterInfo**deriva informações de parâmetro e retorna isso. Se **isscommandwithparameters:: SetParameterProperties** ou **SetParameterInfo** tiverem sido chamados para pelo menos um parâmetro, **isscommandwithparameters:: Getparameterproperties**  retornará propriedades apenas para esses parâmetros para o qual **isscommandwithparameters:: SetParameterProperties** foi chamado. Se **isscommandwithparameters:: SetParameterProperties** é chamado após **isscommandwithparameters:: Getparameterproperties** ou **GetParameterInfo**, as chamadas subsequentes para **isscommandwithparameters:: Getparameterproperties** retornar os valores substituídos desses parâmetros para o qual **isscommandwithparameters:: SetParameterProperties** foi chamado.  
  
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
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
