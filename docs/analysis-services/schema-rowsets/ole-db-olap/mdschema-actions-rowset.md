---
title: Conjunto de linhas MDSCHEMA_ACTIONS | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_ACTIONS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_ACTIONS rowset
ms.assetid: f73081f8-ac51-4286-b46e-2b34e792c3e0
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 50b7b29005b5dc5ee4652a79784f33194c5a5a9a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="mdschemaactions-rowset"></a>Conjunto de linhas MDSCHEMA_ACTIONS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Descreve as ações que podem estar disponíveis para o aplicativo cliente.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **MDSCHEMA_ACTIONS** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||O nome do banco de dados.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||Sem suporte. Sempre contém **VT_NULL**.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||O nome do cubo ao qual pertence esta ação.|  
|**ACTION_NAME**|**DBTYPE_WSTR**||O nome dessa ação.|  
|**ACTION_TYPE**|**DBTYPE_I4**||Um bitmap que é usado para especificar o método de disparo da ação. O arquivo Msmd.h define as seguintes constantes do valor de bit para esse bitmap:<br /><br /> **MDACTION_TYPE_URL** (**0x01**)<br /><br /> **MDACTION_TYPE_HTML** (**0x02**)<br /><br /> **MDACTION_TYPE_STATEMENT** (**0x04**)<br /><br /> **MDACTION_TYPE_DATASET** (**0x08**)<br /><br /> **MDACTION_TYPE_ROWSET** (**0x10**)<br /><br /> **MDACTION_TYPE_COMMANDLINE** (**0x20**)<br /><br /> **MDACTION_TYPE_PROPRIETARY** (**0x40**)<br /><br /> **MDACTION_TYPE_REPORT** (**0x80**)<br /><br /> **MDACTION_TYPE_DRILLTHROUGH** (**0x100**)|  
|**COORDENADA**|**DBTYPE_WSTR**||Uma expressão da linguagem MDX (Multidimensional Expressions) que especifica um objeto ou uma coordenada no espaço multidimensional no qual a ação é executada. É responsabilidade do aplicativo cliente fornecer o valor desta coluna de restrição.<br /><br /> O **CORDINATE** deve ser resolvido para o objeto especificado em **COORDINATE_TYPE**.|  
|**COORDINATE_TYPE**|**DBTYPE_I4**||Um bitmap que especifica como o **COORDENAR** coluna de restrição é interpretada. O arquivo Msmd.h define as seguintes constantes do valor de bit para esse bitmap:<br /><br /> **MDACTION_COORDINATE_CUBE** (**1**)<br /><br /> **MDACTION_COORDINATE_DIMENSION** (**2**): refere-se às hierarquias de dimensões.<br /><br /> **MDACTION_COORDINATE_LEVEL** (**3**)<br /><br /> **MDACTION_COORDINATE_MEMBER** (**4**)<br /><br /> **MDACTION_COORDINATE_SET** (**5**)<br /><br /> **MDACTION_COORDINATE_CELL** (**6**)|  
|**ACTION_CAPTION**|**DBTYPE_WSTR**||O nome da ação se nenhuma legenda tiver sido especificada e nenhuma conversão tiver sido especificada no DDL.<br /><br /> Se uma legenda ou conversão tiver sido especificada, e **CaptionIsMDX** for false, uma das seguintes cadeias de caracteres:<br /><br /> -A tradução para o idioma apropriado.<br /><br /> -A legenda especificada se nenhuma conversão foi encontrado para o idioma especificado.<br /><br /> -O nome da ação se nenhuma conversão foi encontrado e a legenda não foi especificado no DDL.<br /><br /> Se uma legenda ou conversão tiver sido especificada, e **CaptionIsMDX** for true, a cadeia de caracteres resultante da descoberta da conversão apropriada para o idioma especificado ou a conversão especificada na legenda DDL e calcular a fórmula para criar a cadeia de caracteres.<br /><br /> Se a ação tiver sido especificada em MDX Script, não haverá conversões e a legenda sempre será tratada como uma expressão MDX.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição amigável da ação.|  
|**CONTEÚDO**|**DBTYPE_WSTR**||A expressão ou conteúdo da ação a ser executada.|  
|**APLICATIVO**|**DBTYPE_WSTR**||O nome do aplicativo a ser usado para executar a ação.|  
|**INVOCAÇÃO**|**DBTYPE_I4**||Informações sobre como a ação deve ser invocada:<br /><br /> **MDACTION_INVOCATION_INTERACTIVE** (**1**) indica uma ação normal usada durante as operações normais. Este é o valor padrão desta coluna.<br /><br /> **MDACTION_INVOCATION_ON_OPEN** (**2**) indica que a ação deve ser executada quando o cubo é aberto pela primeira vez.<br /><br /> **MDACTION_INVOCATION_BATCH** (**4**) indica que a ação é executada como parte de uma operação em lote ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tarefa.<br /><br /> <br /><br /> Observe que esses valores de enumeração são definidos no arquivo, msmd. h.|  
  
 O conjunto de linhas é classificado em **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **ACTION_NAME**.  
  
> [!NOTE]  
>  Ações de **MDACTION_TYPE_PROPRIETARY** tipo deve fornecer um valor para o **aplicativo** coluna.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **MDSCHEMA_ACTIONS** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Obrigatório|  
|**ACTION_NAME**|**DBTYPE_WSTR**|Opcional|  
|**ACTION_TYPE**|**DBTYPE_I4**|Opcional|  
|**COORDENADA**|**DBTYPE_WSTR**|Obrigatório|  
|**COORDINATE_TYPE**|**DBTYPE_I4**|Obrigatório|  
|**INVOCAÇÃO**|**DBTYPE_I4**|(Opcional) O **INVOCAÇÃO** coluna de restrição padrão é o valor de **MDACTION_INVOCATION_INTERACTIVE**. Para recuperar todas as ações, use o **MDACTION_INVOCATION_ALL** valor o **INVOCAÇÃO** coluna de restrição.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) A restrição padrão é um valor de 1. Um bitmap com um dos seguintes valores válidos:<br /><br /> 1 CUBO<br /><br /> 2 DIMENSÃO|  
  
> [!IMPORTANT]  
>  O **INVOCAÇÃO** coluna de restrição tem um valor padrão de **MDACTION_INVOCATION_INTERACTIVE**. Qualquer conjunto de linhas de esquema que não especifique explicitamente um valor para essa coluna só conterá linhas com esse valor. Se você quiser que o conjunto de linhas para conter todo o conjunto de ações, use o **MDACTION_INVOCATION_ALL** constante a **INVOCAÇÃO** coluna de restrição.  
  
 Aplicativos cliente podem definir mais de um **ACTION_TYPE** usando o operador OR.  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir lista o válido **COORDENAR** e **COORDINATE_TYPE** combinações.  
  
|tipo de objeto COORDINATE|COORDINATE_TYPE|  
|----------------------------|----------------------|  
|**Cube**|**MDACTION_COORDINATE_CUBE**|  
|**Dimension**|**MDACTION_COORDINATE_DIMENSION**<br /><br /> **MDACTION_COORDINATE_LEVEL**<br /><br /> **MDACTION_COORDINATE_MEMBER**<br /><br /> **MDACTION_COORDINATE_SET**<br /><br /> **MDACTION_COORDINATE_CELL**|  
|**Hierarchy**|**MDACTION_COORDINATE_DIMENSION**|  
|**Level**|**MDACTION_COORDINATE_LEVEL**|  
|**Membro**|**MDACTION_COORDINATE_MEMBER**|  
|**Definir**|**MDACTION_COORDINATE_SET**|  
|**célula**|**MDACTION_COORDINATE_CELL**|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
