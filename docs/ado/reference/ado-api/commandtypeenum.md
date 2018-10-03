---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ff7b6ecf919ab83340e49e4395f8c2d1701261d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742874"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
Especifica como um argumento de comando deve ser interpretado.  
  
 É importante validar o usuário forneceu *CommandString* valores para evitar que os usuários do aplicativo a oportunidade de injetar comandos potencialmente perigosos para ADO executar.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|Não especifica o argumento de tipo de comando.|  
|**adCmdText**|1|Avalia [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) como uma definição textual de um comando ou procedimento armazenado chamada.|  
|**adCmdTable**|2|Avalia **CommandText** como um nome de tabela cujas colunas são retornadas por uma consulta SQL gerada internamente.|  
|**adCmdStoredProc**|4|Avalia **CommandText** como um nome de procedimento armazenado.|  
|**adCmdUnknown**|8|Padrão. Indica que o tipo de comando na **CommandText** propriedade não é conhecida.<br /><br /> Quando o tipo de comando não é conhecido, o ADO fará várias tentativas para interpretar a **CommandText**.<br /><br /> -   **CommandText** é interpretado como uma definição textual de uma chamada de procedimento armazenado ou comando. Isso é o mesmo comportamento que **adCmdText**.<br />-   **CommandText** é o nome de um procedimento armazenado. Isso é o mesmo comportamento que **adCmdStoredProc**.<br />-   **CommandText** é interpretado como o nome de uma tabela. Todas as colunas são retornadas por uma consulta SQL gerada internamente. Isso é o mesmo comportamento que **adCmdTable**.|  
|**adCmdFile**|256|Avalia **CommandText** como o nome do arquivo de forma persistente armazenado [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). Usado com **conjunto de registros.** [Aberto](../../../ado/reference/ado-api/open-method-ado-recordset.md) ou [Requery](../../../ado/reference/ado-api/requery-method.md) apenas.|  
|**adCmdTableDirect**|512|Avalia **CommandText** como um nome de tabela cujas colunas são retornadas. Usado com **Recordset.Open** ou **Requery** apenas. Para usar o [Seek](../../../ado/reference/ado-api/seek-method.md) método, o **conjunto de registros** deve ser aberto com **adCmdTableDirect**.<br /><br /> Esse valor não pode ser combinado com o [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valor **adAsyncExecute**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
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
