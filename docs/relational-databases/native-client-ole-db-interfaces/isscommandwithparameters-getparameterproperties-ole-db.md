---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB)
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26c95c64f0f2922ef11946841b160879f001e358
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290066"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Retorna uma matriz de estruturas de conjuntos de propriedades SSPARAMPROPS, um conjunto de propriedades SSPARAMPROPS para cada parâmetro XML ou UDT.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pcParams*[out][in]  
 Um ponteiro para a memória que contém o número de estruturas SSPARAMPROPS retornadas em *prgParamProperties*.  
  
 *prgParamProperties*[out]  
 Um ponteiro para memória na qual uma matriz de estrutura SSPARAMPROPS é retornada. O provedor aloca a memória para as estruturas e retorna o endereço para esta memória; o consumidor libera essa memória com **iMalloc::Livre** quando não precisa mais das estruturas. Antes de ligar para **o IMalloc::Free** for *prgParamProperties*, o consumidor também deve ligar para a **VariantClear** para a propriedade *vValue* de cada estrutura DBPROP, a fim de evitar um vazamento de memória nos casos em que a variante contenha um tipo de referência (como um BSTR.) Se *pcParams* estiver zerado na saída ou um erro diferente DB_E_ERRORSOCCURRED ocorrer, o provedor não aloca rá memória e garante que *prgParamProperties* seja um ponteiro nulo na saída.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O método **GetParameterProperties** retorna os mesmos códigos de erro que o principal método OLE DB **ICommandProperties::GetProperties,** exceto que DB_S_ERRORSOCCURRED e DB_E_ERRORSOCCURED não podem ser levantadas.  
  
## <a name="remarks"></a>Comentários  
 **ISSCommandWithParameters::GetParameterProperties** se comporta consistentemente com relação ao **GetParameterInfo**. Se [ISSCommandWithParameters::SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) ou **SetParameterInfo** não foram chamados ou foram chamados com cParams iguais a zero, **GetParameterInfo** deriva informações de parâmetros e retorna isso. **Se ISSCommandWithParameters::SetParameterProperties** ou **SetParameterInfo** foram chamados para pelo menos um parâmetro, **ISSCommandWithParameters::GetParameterPropriedades** de retorno saem propriedades somente para os parâmetros para os quais **ISSCommandWithParameters:SetParameterProperties** foi chamado. Se **ISSCommandWithParameters::SetParameterPropriedades** são chamadas após **ISSCommandWithParameters::GetParameterProperties** ou **GetParameterInfo,** chamadas subseqüentes para **ISSCommandWithParameters::GetParameterPropriedades** retornar os valores substituídos para os parâmetros para os quais **ISSCommandWithParameters::SetParameterProperties** foi chamado.  
  
 A estrutura SSPARAMPROPS é definida da seguinte maneira:  

```cpp
struct SSPARAMPROPS {
    DBORDINAL iOrdinal;
    ULONG cPropertySets;
    DBPROPSET *rgPropertySets;
};
```

|Membro|Descrição|  
|------------|-----------------|  
|*iOrdinal*|O ordinal do parâmetro passado.|  
|*cPropertySets*|O número de estruturas DBPROPSET em *rgPropertySets*.|  
|*rgPropertySets*|Um ponteiro para a memória no qual uma matriz de estruturas DBPROPSET deve ser retornada.|  
|||

## <a name="see-also"></a>Consulte Também  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
