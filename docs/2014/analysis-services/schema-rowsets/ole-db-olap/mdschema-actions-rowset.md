---
title: Conjunto de linhas MDSCHEMA_ACTIONS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_ACTIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_ACTIONS rowset
ms.assetid: f73081f8-ac51-4286-b46e-2b34e792c3e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 317ddc9a284df779a44866c0c037310b29f76d02
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140710"
---
# <a name="mdschemaactions-rowset"></a>Conjunto de linhas MDSCHEMA_ACTIONS
  Descreve as ações que podem estar disponíveis ao aplicativo cliente.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `MDSCHEMA_ACTIONS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||O nome do banco de dados.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||Sem suporte. Sempre contém `VT_NULL`.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||O nome do cubo ao qual pertence esta ação.|  
|`ACTION_NAME`|`DBTYPE_WSTR`||O nome dessa ação.|  
|`ACTION_TYPE`|`DBTYPE_I4`||Um bitmap que é usado para especificar o método de disparo da ação. O arquivo Msmd.h define as seguintes constantes do valor de bit para esse bitmap:<br /><br /> -   `MDACTION_TYPE_URL` (`0x01`)<br />-   `MDACTION_TYPE_HTML` (`0x02`)<br />-   `MDACTION_TYPE_STATEMENT` (`0x04`)<br />-   `MDACTION_TYPE_DATASET` (`0x08`)<br />-   `MDACTION_TYPE_ROWSET` (`0x10`)<br />-   `MDACTION_TYPE_COMMANDLINE` (`0x20`)<br />-   `MDACTION_TYPE_PROPRIETARY` (`0x40`)<br />-   `MDACTION_TYPE_REPORT` (`0x80`)<br />-   `MDACTION_TYPE_DRILLTHROUGH` (`0x100`)|  
|`COORDINATE`|`DBTYPE_WSTR`||Uma expressão da linguagem MDX (Multidimensional Expressions) que especifica um objeto ou uma coordenada no espaço multidimensional no qual a ação é executada. É responsabilidade do aplicativo cliente fornecer o valor desta coluna de restrição.<br /><br /> O `CORDINATE` deve ser resolvido para o objeto especificado em `COORDINATE_TYPE`.|  
|`COORDINATE_TYPE`|`DBTYPE_I4`||Um bitmap que especifica como a coluna de restrição `COORDINATE` é interpretada. O arquivo Msmd.h define as seguintes constantes do valor de bit para esse bitmap:<br /><br /> -   `MDACTION_COORDINATE_CUBE` (`1`)<br />-   `MDACTION_COORDINATE_DIMENSION` (`2`)<br />     refere-se às hierarquias de dimensões.<br />-   `MDACTION_COORDINATE_LEVEL` (`3`)<br />-   `MDACTION_COORDINATE_MEMBER` (`4`)<br />-   `MDACTION_COORDINATE_SET` (`5`)<br />-   `MDACTION_COORDINATE_CELL` (`6`)|  
|`ACTION_CAPTION`|`DBTYPE_WSTR`||O nome da ação se nenhuma legenda tiver sido especificada e nenhuma conversão tiver sido especificada no DDL.<br /><br /> Quando há especificação de uma legenda ou de conversões, e `CaptionIsMDX` é false, ocorre uma das seguintes cadeias de caracteres:<br /><br /> -A tradução para o idioma apropriado.<br />-A legenda especificada se nenhuma conversão for localizada para o idioma especificado.<br />-O nome da ação se nenhuma conversão tiver sido encontrado e a legenda não foi especificada no DDL.<br /><br /> Se uma legenda ou conversão tiver sido especificada, e `CaptionIsMDX` for true, a cadeia de caracteres resultante da descoberta da conversão apropriada para o idioma especificado ou a conversão especificada na legenda DDL, e o cálculo da fórmula para criar a cadeia de caracteres.<br /><br /> Se a ação tiver sido especificada em MDX Script, não haverá conversões e a legenda sempre será tratada como uma expressão MDX.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição amigável da ação.|  
|`CONTENT`|`DBTYPE_WSTR`||A expressão ou conteúdo da ação a ser executada.|  
|`APPLICATION`|`DBTYPE_WSTR`||O nome do aplicativo a ser usado para executar a ação.|  
|`INVOCATION`|`DBTYPE_I4`||Informações sobre como a ação deve ser invocada:<br /><br /> -   `MDACTION_INVOCATION_INTERACTIVE` (`1`) indica uma ação normal usada durante as operações normais. Este é o valor padrão desta coluna.<br />-   `MDACTION_INVOCATION_ON_OPEN` (`2`) indica que a ação deve ser realizada quando o cubo é aberto pela primeira vez.<br />-   `MDACTION_INVOCATION_BATCH` (`4`) indica que a ação é executada como parte de uma operação em lote ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tarefa.<br /><br /> Estes valores de enumeração são definidos no arquivo, Msmd.h.|  
  
 O conjunto de linhas é classificado em `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `ACTION_NAME`.  
  
> [!NOTE]  
>  Ações do tipo `MDACTION_TYPE_PROPRIETARY` devem fornecer um valor para a coluna `APPLICATION`.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `MDSCHEMA_ACTIONS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Obrigatório|  
|`ACTION_NAME`|`DBTYPE_WSTR`|Opcional|  
|`ACTION_TYPE`|`DBTYPE_I4`|Opcional|  
|`COORDINATE`|`DBTYPE_WSTR`|Obrigatório|  
|`COORDINATE_TYPE`|`DBTYPE_I4`|Obrigatório|  
|`INVOCATION`|`DBTYPE_I4`|(Opcional) O valor padrão da coluna de restrição `INVOCATION` é `MDACTION_INVOCATION_INTERACTIVE`. Para recuperar todas as ações, use o valor `MDACTION_INVOCATION_ALL` na coluna de restrição `INVOCATION`.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -CUBO DE 1<br />-DIMENSÃO DE 2<br /><br /> A restrição padrão tem valor 1.|  
  
> [!IMPORTANT]  
>  O valor padrão da coluna de restrição `INVOCATION` é `MDACTION_INVOCATION_INTERACTIVE`. Qualquer conjunto de linhas de esquema que não especifique explicitamente um valor para essa coluna só conterá linhas com esse valor. Se você desejar que o conjunto de linhas contenha o conjunto inteiro de ações, use a constante `MDACTION_INVOCATION_ALL` na coluna de restrição `INVOCATION`.  
  
 Aplicativos cliente podem definir mais de um `ACTION_TYPE` usando o operador OR.  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir lista as combinações `COORDINATE` e `COORDINATE_TYPE` válidas.  
  
|tipo de objeto COORDINATE|COORDINATE_TYPE|  
|----------------------------|----------------------|  
|`Cube`|`MDACTION_COORDINATE_CUBE`|  
|`Dimension`|`MDACTION_COORDINATE_DIMENSION`<br /><br /> `MDACTION_COORDINATE_LEVEL`<br /><br /> `MDACTION_COORDINATE_MEMBER`<br /><br /> `MDACTION_COORDINATE_SET`<br /><br /> `MDACTION_COORDINATE_CELL`|  
|`Hierarchy`|`MDACTION_COORDINATE_DIMENSION`|  
|`Level`|`MDACTION_COORDINATE_LEVEL`|  
|`Member`|`MDACTION_COORDINATE_MEMBER`|  
|`Set`|`MDACTION_COORDINATE_SET`|  
|`cell`|`MDACTION_COORDINATE_CELL`|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
