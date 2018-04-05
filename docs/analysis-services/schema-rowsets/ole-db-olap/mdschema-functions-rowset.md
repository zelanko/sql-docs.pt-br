---
title: Conjunto de linhas MDSCHEMA_FUNCTIONS | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MDSCHEMA_FUNCTIONS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_FUNCTIONS rowset
ms.assetid: 5253fa8c-b1ce-4504-aff6-a246b5e675c7
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e8a03e34bf6ea617e650132f2a81fb065a014d80
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdschemafunctions-rowset"></a>Conjunto de linhas MDSCHEMA_FUNCTIONS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Descreve as funções disponíveis para aplicativos cliente conectados ao banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **MDSCHEMA_FUNCTIONS** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**NOME_DA_FUNÇÃO**|**DBTYPE_WSTR**|O nome da função.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Uma descrição da função.|  
|**PARAMETER_LIST**|**DBTYPE_WSTR**|Uma lista de parâmetros delimitados por vírgulas, formatados como no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic. Por exemplo, um parâmetro pode ser um nome como cadeia de caracteres.|  
|**RETURN_TYPE**|**DBTYPE_I4**|O **VARTYPE** do tipo de dados de retorno da função.|  
|**ORIGEM**|**DBTYPE_I4**|A origem da função:<br /><br /> 1 para funções MDX.<br /><br /> 2 para funções definidas pelo usuário.|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|O nome da interface para funções definidas pelo usuário<br /><br /> O nome de grupo para funções MDX (expressão multidimensional).|  
|**NOME_DA_BIBLIOTECA**|**DBTYPE_WSTR**|O nome da biblioteca de tipos para funções definidas pelo usuário. **NULO** para funções MDX.|  
|**DLL_NAME**|**DBTYPE_WSTR**|(Opcional) O nome do assembly que implementa a função definida pelo usuário.<br /><br /> Retorna **VT_NULL** para funções MDX.|  
|**HELP_FILE**|**DBTYPE_WSTR**|(Opcional) O nome do arquivo que contém a documentação de ajuda para a função definida pelo usuário.<br /><br /> Retorna **VT_NULL** para funções MDX.|  
|**HELP_CONTEXT**|**DBTYPE_I4**|(Opcional) Retorna a ID de contexto da Ajuda para esta função.|  
|**OBJETO**|**DBTYPE_WSTR**|(Opcional) O nome genérico da classe de objeto à qual se aplica uma propriedade. Por exemplo, o conjunto de linhas correspondente para o < level_name >. Membros da função retorna "**nível**".<br /><br /> Retorna **VT_NULL** para funções definidas pelo usuário ou funções MDX de propriedade não.|  
|**LEGENDA**|**DBTYPE_WSTR**|A legenda de exibição da função.|  
  
 O conjunto de linhas é classificado em **origem**, **INTERFACE_NAME**, **FUNCTION_NAME**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **MDSCHEMA_FUNCTIONS** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**NOME_DA_BIBLIOTECA**|**DBTYPE_WSTR**|Opcional.|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**NOME_DA_FUNÇÃO**|**DBTYPE_WSTR**|Opcional.|  
|**ORIGEM**|**DBTYPE_I4**|Opcional.|  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
