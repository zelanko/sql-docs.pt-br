---
title: 'Isscommandwithparameters:: SetParameterProperties (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dafc28244a94a3738b91c454f75bc8bb26d0b391
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416965"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
  Define as propriedades de cada parâmetro por ordinal ou define as propriedades de parâmetro em massa especificando uma matriz de estruturas SSPARAMPROPS.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT SetParameterProperties(  
DB_UPARAMS cParams,   
SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>Argumentos  
 *cParams*[in]  
 O número de estruturas SSPARAMPROPS na *rgParamProperties* matriz. Se esse número for zero, `ISSCommandWithParameters::SetParameterProperties` excluirá todas as propriedades que poderiam ter sido especificadas para todos os parâmetros no comando.  
  
 *rgParamProperties*[in]  
 Uma matriz de estruturas SSPARAMPROPS a ser definida.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O `ISSCommandWithParameters::SetParameterProperties` método retorna os mesmos códigos de erro que o OLE DB de núcleo **icommandproperties:: SetProperties** método.  
  
## <a name="remarks"></a>Remarks  
 Definindo propriedades de parâmetro com esse método é permitido em cada parâmetro por ordinal ou com um único `ISSCommandWithParameters::SetParameterProperties` chamada depois que o SSPARAMPROPS tiver sido criado da matriz de propriedade.  
  
 O **SetParameterInfo** método deve ser chamado antes de chamar o `ISSCommandWithParameters::SetParameterProperties` método. Se você chamar `SetParameterProperties(0, NULL)` limpará todas as propriedades de parâmetro especificadas, ao passo que se chamar `SetParameterInfo(0,NULL,NULL)`, limpará todas as informações do parâmetro incluindo as propriedades que podem ser associadas a um parâmetro.  
  
 Chamando `ISSCommandWithParameters::SetParameterProperties` para especificar propriedades para um parâmetro que não é do tipo DBTYPE_XML o DBTYPE_UDT retorna DB_E_ERRORSOCCURRED ou DB_S_ERRORSOCCURRED e marca o *dwStatus* campo de todos os DBPROPs contidos em SSPARAMPROPS para esse parâmetro com DBPROPSTATUS_NOTSET. A matriz DBPROP de cada DBPROPSET contido em SSPARAMPROPS deveria ser atravessada para detectar o parâmetro ao qual DB_E_ERRORSOCCURRED ou DB_S_ERRORSOCCURRED se refere.  
  
 Se `ISSCommandWithParameters::SetParameterProperties` é chamado para especificar as propriedades de parâmetros cujas informações de parâmetro tem ainda não foi definida com **SetParameterInfo**, o provedor retornará E_UNEXPECTED com a seguinte mensagem de erro:  
  
 O método SetParameterProperties não pode ser chamado para os parâmetros especificados sem primeiro chamar o método SetParameterInfo. As informações de parâmetro devem ser definidas antes da definição das propriedades de parâmetro.  
  
 Se a chamada para `ISSCommandWithParameters::SetParameterProperties` contém alguns parâmetros, onde as informações do parâmetro tem sido definida, e alguns parâmetros em que as informações do parâmetro não tem sido definida, as propriedades dwStatus no DBPROPSET do conjunto de propriedades SSPARAMPROPS retornarão com DBSTATUS_NOTSET.  
  
 A estrutura SSPARAMPROPS é definida da seguinte maneira:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 Melhorias no mecanismo de banco de dados a partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir isscommandwithparameters:: SetParameterProperties Obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por isscommandwithparameters:: SetParameterProperties nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [descoberta de metadados](../native-client/features/metadata-discovery.md).  
  
|Membro|Description|  
|------------|-----------------|  
|*iOrdinal*|O ordinal do parâmetro passado.|  
|*cPropertySets*|O número de estruturas DBPROPSET em *rgPropertySets*.|  
|*rgPropertySets*|Um ponteiro para a memória no qual uma matriz de estruturas DBPROPSET deve ser retornada.|  
  
## <a name="see-also"></a>Consulte também  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
