---
title: Conjunto de linhas MDSCHEMA_FUNCTIONS | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 81c5ff06837dd9004be1ffc72be017a4991e902f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemafunctions-rowset"></a>Conjunto de linhas MDSCHEMA_FUNCTIONS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Descreve as funções disponíveis para aplicativos cliente conectados ao banco de dados.  
  
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
|**OBJECT**|**DBTYPE_WSTR**|(Opcional) O nome genérico da classe de objeto à qual se aplica uma propriedade. Por exemplo, o conjunto de linhas correspondente para o < level_name >. Membros da função retorna "**nível**".<br /><br /> Retorna **VT_NULL** para funções definidas pelo usuário ou funções MDX de propriedade não.|  
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
  
## <a name="see-also"></a>Consulte também  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
