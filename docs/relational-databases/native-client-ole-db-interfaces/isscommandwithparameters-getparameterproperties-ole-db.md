---
description: 'ISSCommandWithParameters:: ParameterProperties em SQL Server Native Client (OLE DB)'
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5ed13eb576aaf85e734be14446f0f6f94d0dddf7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469297"
---
# <a name="isscommandwithparametersgetparameterproperties-in-sql-server-native-client-ole-db"></a>ISSCommandWithParameters:: ParameterProperties em SQL Server Native Client (OLE DB)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

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
 Um ponteiro para memória na qual uma matriz de estrutura SSPARAMPROPS é retornada. O provedor aloca memória para as estruturas e retorna o endereço para essa memória; o consumidor libera essa memória com **IMalloc:: Free** quando ela não precisa mais das estruturas. Antes de chamar **IMalloc:: Free** para *prgParamProperties*, o consumidor também deve chamar **VariantClear** para a propriedade *vValue* de cada estrutura DBPROP para evitar um vazamento de memória nos casos em que a variante contém um tipo de referência (como um BSTR). Se *pcParams* for zero na saída ou um erro diferente de DB_E_ERRORSOCCURRED ocorrer, o provedor não alocará memória e garantirá que *prgParamProperties* seja um ponteiro nulo na saída.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O método **ParameterProperties** retorna os mesmos códigos de erro que o método principal OLE DB **ICommandProperties:: GetProperties** , exceto que DB_S_ERRORSOCCURRED e DB_E_ERRORSOCCURED não podem ser gerados.  
  
## <a name="remarks"></a>Comentários  
 **ISSCommandWithParameters:: ParameterProperties** se comporta consistentemente em relação a **GetParameterInfo**. Se [ISSCommandWithParameters:: ParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) ou **SetParameterInfo** não tiver sido chamado ou tiver sido chamado com cParams igual a zero, **GetParameterInfo** derivará informações de parâmetro e retornará isso. Se **ISSCommandWithParameters:: ParameterProperties** ou **SetParameterInfo** tiver sido chamado para pelo menos um parâmetro, **ISSCommandWithParameters:: ParameterProperties** retornará propriedades somente para os parâmetros para os quais **ISSCommandWithParameters:: ParameterProperties** foi chamado. Se **ISSCommandWithParameters:: ParameterProperties** for chamado após **ISSCommandWithParameters:: ParameterProperties** ou **GetParameterInfo**, as chamadas subsequentes para **ISSCommandWithParameters:: ParameterProperties** retornarão os valores substituídos para esses parâmetros para os quais **ISSCommandWithParameters:: ParameterProperties** foi chamado.  
  
 A estrutura SSPARAMPROPS é definida da seguinte maneira:  

```cpp
struct SSPARAMPROPS {
    DBORDINAL iOrdinal;
    ULONG cPropertySets;
    DBPROPSET *rgPropertySets;
};
```

|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|*iOrdinal*|O ordinal do parâmetro passado.|  
|*cPropertySets*|O número de estruturas DBPROPSET em *rgPropertySets*.|  
|*rgPropertySets*|Um ponteiro para a memória no qual uma matriz de estruturas DBPROPSET deve ser retornada.|  
|||

## <a name="see-also"></a>Consulte Também  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
