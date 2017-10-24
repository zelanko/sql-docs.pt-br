---
title: CommandTypeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- CommandTypeEnum
helpviewer_keywords:
- CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bc2cd3acc56c11bdab98d58c1adc76d98eb1579d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="commandtypeenum"></a>CommandTypeEnum
Especifica como um argumento de comando deve ser interpretado.  
  
 É importante validar o usuário forneceu *CommandString* valores para evitar que os usuários do aplicativo a oportunidade de injetar comandos potencialmente perigosos para ADO executar.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|Não especifique o argumento de tipo de comando.|  
|**adCmdText**|1|Avalia [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) como uma definição textual de um comando ou procedimento armazenado chama.|  
|**adCmdTable**|2|Avalia **CommandText** como um nome de tabela cujas colunas são retornadas por uma consulta SQL gerada internamente.|  
|**adCmdStoredProc**|4|Avalia **CommandText** como um nome de procedimento armazenado.|  
|**adCmdUnknown**|8|Padrão. Indica que o tipo de comando no **CommandText** propriedade não é conhecida.<br /><br /> Quando o tipo de comando não é conhecido, o ADO fará várias tentativas para interpretar o **CommandText**.<br /><br /> -   **CommandText** é interpretado como uma definição textual de uma chamada de procedimento armazenado ou comando. Este é o mesmo comportamento que **adCmdText**.<br />-   **CommandText** é o nome de um procedimento armazenado. Este é o mesmo comportamento que **adCmdStoredProc**.<br />-   **CommandText** é interpretado como o nome de uma tabela. Todas as colunas são retornadas por uma consulta SQL gerada internamente. Este é o mesmo comportamento que **adCmdTable**.|  
|**adCmdFile**|256|Avalia **CommandText** como o nome do arquivo de uma maneira persistente armazenado [registros](../../../ado/reference/ado-api/recordset-object-ado.md). Usado com **Recordset.** [Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) ou [Requery](../../../ado/reference/ado-api/requery-method.md) somente.|  
|**adCmdTableDirect**|512|Avalia **CommandText** como um nome de tabela cujas colunas são retornadas. Usado com **Recordset.Open** ou **Requery** somente. Para usar o [busca](../../../ado/reference/ado-api/seek-method.md) método, o **registros** deve ser aberto com **adCmdTableDirect**.<br /><br /> Esse valor não pode ser combinado com o [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valor **adAsyncExecute**.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CommandType.UNSPECIFIED|  
|AdoEnums.CommandType.TEXT|  
|AdoEnums.CommandType.TABLE|  
|AdoEnums.CommandType.STOREDPROC|  
|AdoEnums.CommandType.UNKNOWN|  
|AdoEnums.CommandType.FILE|  
|AdoEnums.CommandType.TABLEDIRECT|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Propriedade CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)|[Método Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Método Execute (conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|[Método Open (Conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Método Requery](../../../ado/reference/ado-api/requery-method.md)||

