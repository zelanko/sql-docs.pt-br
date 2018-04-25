---
title: 'Isscommandwithparameters:: (OLE DB) | Microsoft Docs'
description: ISSCommandWithParameters::SetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e9ddd27c4b2d1fc88385ee6dbf178a1c311b47b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Define as propriedades de cada parâmetro por ordinal ou define as propriedades de parâmetro em massa especificando uma matriz de estruturas SSPARAMPROPS.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>Argumentos  
 cParams *[in]  
 O número de estruturas SSPARAMPROPS na matriz rgParamProperties *. Se esse número for zero, ISSCommandWithParameters::SetParameterProperties** excluirá todas as propriedades que poderiam ter sido especificadas para qualquer parâmetro no comando.  
  
 rgParamProperties *[in]  
 Uma matriz de estruturas SSPARAMPROPS a ser definida.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O método ISSCommandWithParameters::SetParameterProperties **retorna os mesmos códigos de erro que o método principal OLE DB ICommandProperties::SetProperties**.  
  
## <a name="remarks"></a>Remarks  
 A definição das propriedades de parâmetro com esse método é feita para cada parâmetro por ordinal, ou com uma única chamada para ISSCommandWithParameters::SetParameterProperties** depois que SSPARAMPROPS tiver sido criado a partir da matriz de propriedades.  
  
 O método SetParameterInfo **deve ser chamado antes do método ISSCommandWithParameters::SetParameterProperties**. Se você chamar `SetParameterProperties(0, NULL)` limpará todas as propriedades de parâmetro especificadas, ao passo que se chamar `SetParameterInfo(0,NULL,NULL)`, limpará todas as informações do parâmetro incluindo as propriedades que podem ser associadas a um parâmetro.  
  
 Chamar ISSCommandWithParameters::SetParameterProperties **para especificar propriedades de um parâmetro que não seja do tipo DBTYPE_XML o DBTYPE_UDT retorna DB_E_ERRORSOCCURRED ou DB_S_ERRORSOCCURRED e marca o campo dwStatus** de todos os DBPROPs contidos em SSPARAMPROPS para aquele parâmetro com DBPROPSTATUS_NOTSET. A matriz DBPROP de cada DBPROPSET contido em SSPARAMPROPS deveria ser atravessada para detectar o parâmetro ao qual DB_E_ERRORSOCCURRED ou DB_S_ERRORSOCCURRED se refere.  
  
 Se ISSCommandWithParameters::SetParameterProperties **for chamado para especificar as propriedades de parâmetros cujas informações ainda não estiverem definidas com SetParameterInfo**, o provedor retornará E_UNEXPECTED com a seguinte mensagem de erro:  
  
 O método SetParameterProperties não pode ser chamado para os parâmetros especificados sem primeiro chamar o método SetParameterInfo. As informações de parâmetro devem ser definidas antes da definição das propriedades de parâmetro.  
  
 Se a chamada para ISSCommandWithParameters::SetParameterProperties** contiver alguns parâmetros com informações definidas e outros sem informações definidas, as propriedades dwStatus no DBPROPSET do conjunto de propriedades SSPARAMPROPS retornarão com DBSTATUS_NOTSET.  
  
 A estrutura SSPARAMPROPS é definida da seguinte maneira:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 Melhorias no mecanismo de banco de dados, começando com [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permitir isscommandwithparameters:: Obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por isscommandwithparameters:: em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Metadata Discovery](../../oledb/features/metadata-discovery.md).  
  
|Membro|Description|  
|------------|-----------------|  
|iOrdinal|O ordinal do parâmetro passado.|  
|cPropertySets|O número de estruturas DBPROPSET em rgPropertySets *.|  
|rgPropertySets|Um ponteiro para a memória no qual uma matriz de estruturas DBPROPSET deve ser retornada.|  
  
## <a name="see-also"></a>Consulte Também  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
