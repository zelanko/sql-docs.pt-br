---
title: Conjunto de linhas MDSCHEMA_FUNCTIONS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_FUNCTIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_FUNCTIONS rowset
ms.assetid: 5253fa8c-b1ce-4504-aff6-a246b5e675c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d5966a975cab0f70c24801e83ee9eab7fa99398
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090866"
---
# <a name="mdschemafunctions-rowset"></a>Conjunto de linhas MDSCHEMA_FUNCTIONS
  Descreve as funções disponíveis para aplicativos cliente conectados ao banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **MDSCHEMA_FUNCTIONS** linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**||O nome da função.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição da função.|  
|**PARAMETER_LIST**|**DBTYPE_WSTR**||Uma lista de parâmetros delimitados por vírgulas, formatados como no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic. Por exemplo, um parâmetro pode ser um nome como cadeia de caracteres.|  
|**RETURN_TYPE**|**DBTYPE_I4**||O **VARTYPE** do tipo de dados de retorno da função.|  
|**ORIGEM**|**DBTYPE_I4**||A origem da função:<br /><br /> -1 para funções MDX.<br />-2 para funções definidas pelo usuário.|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**||O nome da interface para funções definidas pelo usuário<br /><br /> O nome de grupo para funções MDX (expressão multidimensional).|  
|**NOME_DA_BIBLIOTECA**|**DBTYPE_WSTR**||O nome da biblioteca de tipos para funções definidas pelo usuário. **NULO** para funções MDX.|  
|**DLL_NAME**|**DBTYPE_WSTR**||(Opcional) O nome do assembly que implementa a função definida pelo usuário.<br /><br /> Retorna **VT_NULL** para funções MDX.|  
|**HELP_FILE**|**DBTYPE_WSTR**||(Opcional) O nome do arquivo que contém a documentação de ajuda para a função definida pelo usuário.<br /><br /> Retorna **VT_NULL** para funções MDX.|  
|**HELP_CONTEXT**|**DBTYPE_I4**||(Opcional) Retorna a ID de contexto da Ajuda para esta função.|  
|**OBJECT**|**DBTYPE_WSTR**||(Opcional) O nome genérico da classe de objeto à qual se aplica uma propriedade. Por exemplo, o conjunto de linhas correspondente para < level_name >. Os membros de função retorna "**nível**".<br /><br /> Retorna **VT_NULL** para funções definidas pelo usuário ou funções MDX sem-propriedade.|  
|**LEGENDA**|**DBTYPE_WSTR**||A legenda de exibição da função.|  
  
 O conjunto de linhas é classificado em **ORIGIN**, **INTERFACE_NAME**, **FUNCTION_NAME**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **MDSCHEMA_FUNCTIONS** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**NOME_DA_BIBLIOTECA**|**DBTYPE_WSTR**|Opcional.|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**ORIGEM**|**DBTYPE_I4**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
