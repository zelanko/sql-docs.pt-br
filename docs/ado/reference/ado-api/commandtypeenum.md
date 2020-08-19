---
description: CommandTypeEnum
title: CommandTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommandTypeEnum
helpviewer_keywords:
- CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
author: rothja
ms.author: jroth
ms.openlocfilehash: 861abb0066f4b9f32ff8f9071c1520a1dec73016
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450818"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
Especifica como um argumento de comando deve ser interpretado.  
  
 É importante validar os valores de *commandstring* fornecidos pelo usuário para evitar que os usuários de aplicativos tenham a oportunidade de injetar comandos potencialmente perigosos para execução do ADO.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|Não especifica o argumento de tipo de comando.|  
|**adCmdText**|1|Avalia [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) como uma definição textual de um comando ou uma chamada de procedimento armazenado.|  
|**adCmdTable**|2|Avalia **CommandText** como um nome de tabela cujas colunas são todas retornadas por uma consulta SQL gerada internamente.|  
|**adCmdStoredProc**|4|Avalia **CommandText** como um nome de procedimento armazenado.|  
|**adCmdUnknown**|8|Padrão. Indica que o tipo de comando na propriedade **CommandText** não é conhecido.<br /><br /> Quando o tipo de comando não é conhecido, o ADO fará várias tentativas de interpretar o **CommandText**.<br /><br /> -   **CommandText** é interpretado como uma definição textual de um comando ou uma chamada de procedimento armazenado. Esse é o mesmo comportamento que **adCmdText**.<br />-   **CommandText** é o nome de um procedimento armazenado. Esse é o mesmo comportamento que **adCmdStoredProc**.<br />-   **CommandText** é interpretado como o nome de uma tabela. Todas as colunas são retornadas por uma consulta SQL gerada internamente. Esse é o mesmo comportamento que **adCmdTable**.|  
|**adCmdFile**|256|Avalia **CommandText** como o nome de arquivo de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)armazenado de forma persistente. Usado com o **conjunto de registros.** [Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) ou somente [consulta](../../../ado/reference/ado-api/requery-method.md) .|  
|**adCmdTableDirect**|512|Avalia **CommandText** como um nome de tabela cujas colunas são todas retornadas. Usado com **Recordset. Open** ou **Requery** somente. Para usar o método [Seek](../../../ado/reference/ado-api/seek-method.md) , o **conjunto de registros** deve ser aberto com **adCmdTableDirect**.<br /><br /> Esse valor não pode ser combinado com o valor de [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) **adAsyncExecute**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.CommandType.UNSPECIFIED|  
|AdoEnums.CommandType.TEXT|  
|AdoEnums.CommandType.TABLE|  
|AdoEnums.CommandType.STOREDPROC|  
|AdoEnums.CommandType.UNKNOWN|  
|AdoEnums.CommandType.FILE|  
|AdoEnums.CommandType.TABLEDIRECT|  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Propriedade CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)  
        [Método Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)  
    :::column-end:::
    :::column:::
        [Método Execute (conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)  
        [Método Open (Conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)  
    :::column-end:::
    :::column:::
        [Método Requery](../../../ado/reference/ado-api/requery-method.md)  
    :::column-end:::
:::row-end:::
