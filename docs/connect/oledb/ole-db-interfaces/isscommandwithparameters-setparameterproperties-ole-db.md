---
title: ISSCommandWithParameters::SetParameterProperties (OLE DB) | Microsoft Docs
description: Saiba como o método ISSCommandWithParameters::SetParameterProperties define as propriedades do parâmetro no Driver do OLE DB para SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6340c4f52106b15adb2fec651a3cca213dad5d19
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862166"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Define as propriedades de cada parâmetro por ordinal ou define as propriedades de parâmetro em massa especificando uma matriz de estruturas SSPARAMPROPS.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>Argumentos  
 *cParams*[in]  
 O número de estruturas SSPARAMPROPS na matriz *rgParamProperties*. Se esse número for zero, **ISSCommandWithParameters::SetParameterProperties** excluirá todas as propriedades que poderiam ter sido especificadas para qualquer parâmetro no comando.  
  
 *rgParamProperties*[in]  
 Uma matriz de estruturas SSPARAMPROPS a ser definida.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O método **ISSCommandWithParameters::SetParameterProperties** retorna os mesmos códigos de erro do método principal **ICommandProperties::SetProperties** do OLE DB.  
  
## <a name="remarks"></a>Comentários  
 A definição das propriedades de parâmetro com esse método é permitida para cada parâmetro por ordinal, ou com uma única chamada a **ISSCommandWithParameters::SetParameterProperties**, depois que SSPARAMPROPS tiver sido criado com base na matriz de propriedades.  
  
 O método **SetParameterInfo** precisa ser chamado antes do método **ISSCommandWithParameters::SetParameterProperties**. Se você chamar `SetParameterProperties(0, NULL)` limpará todas as propriedades de parâmetro especificadas, ao passo que se chamar `SetParameterInfo(0,NULL,NULL)`, limpará todas as informações do parâmetro incluindo as propriedades que podem ser associadas a um parâmetro.  
  
 A chamada a **ISSCommandWithParameters::SetParameterProperties** para especificar as propriedades de um parâmetro que não é do tipo DBTYPE_XML ou DBTYPE_UDT retorna DB_E_ERRORSOCCURRED ou DB_S_ERRORSOCCURRED e marca o campo *dwStatus* de todos os DBPROPs contidos em SSPARAMPROPS para o parâmetro com DBPROPSTATUS_NOTSET. A matriz DBPROP de cada DBPROPSET contido em SSPARAMPROPS deveria ser atravessada para detectar o parâmetro ao qual DB_E_ERRORSOCCURRED ou DB_S_ERRORSOCCURRED se refere.  
  
 Se **ISSCommandWithParameters::SetParameterProperties** for chamado para especificar as propriedades de parâmetros cujas informações ainda não foram definidas com **SetParameterInfo**, o provedor retornará E_UNEXPECTED com a seguinte mensagem de erro:  
  
 O método SetParameterProperties não pode ser chamado para os parâmetros especificados sem primeiro chamar o método SetParameterInfo. As informações de parâmetro devem ser definidas antes da definição das propriedades de parâmetro.  
  
 Se a chamada a **ISSCommandWithParameters::SetParameterProperties** contiver alguns parâmetros com as informações definidas e outros sem informações definidas, as propriedades dwStatus no DBPROPSET do conjunto de propriedades SSPARAMPROPS serão retornadas com DBSTATUS_NOTSET.  
  
 A estrutura SSPARAMPROPS é definida da seguinte maneira:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 Aprimoramentos no mecanismo de banco de dados desde o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permitem que ISSCommandWithParameters::SetParameterProperties obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por ISSCommandWithParameters::SetParameterProperties em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Descoberta de metadados](../../oledb/features/metadata-discovery.md).  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|*iOrdinal*|O ordinal do parâmetro passado.|  
|*cPropertySets*|O número de estruturas DBPROPSET em *rgPropertySets*.|  
|*rgPropertySets*|Um ponteiro para a memória no qual uma matriz de estruturas DBPROPSET deve ser retornada.|  
  
## <a name="see-also"></a>Consulte Também  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
