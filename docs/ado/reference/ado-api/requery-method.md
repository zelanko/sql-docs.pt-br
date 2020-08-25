---
description: Método Requery
title: Método Requery | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
author: rothja
ms.author: jroth
ms.openlocfilehash: a8b9a5d3ab52fdbd3e219104ce3553cd69753a40
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777685"
---
# <a name="requery-method"></a>Método Requery
Atualiza os dados em um objeto de [conjunto de registros](./recordset-object-ado.md) executando novamente a consulta na qual o objeto se baseia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Opções*  
 Opcional. Um bitmask que contém valores [ExecuteOptionEnum](./executeoptionenum.md) e [CommandTypeEnum](./commandtypeenum.md) que afetam esta operação.  
  
> [!NOTE]
>  Se *Options* for definido como **adAsyncExecute**, essa operação será executada de forma assíncrona e um evento [RecordsetChangeComplete](./willchangerecordset-and-recordsetchangecomplete-events-ado.md) será emitido quando for concluído. Os valores de **ExecuteOpenEnum** de **adExecuteNoRecords** ou **adExecuteStream** não devem ser usados com **Requery**.  
  
## <a name="remarks"></a>Comentários  
 Use o método **Requery** para atualizar todo o conteúdo de um objeto **Recordset** da fonte de dados emitindo novamente o comando original e recuperando os dados uma segunda vez. Chamar esse método é equivalente a chamar os métodos [Close](./close-method-ado.md) e [Open](./open-method-ado-recordset.md) sucessivamente. Se você estiver editando o registro atual ou adicionando um novo registro, ocorrerá um erro.  
  
 Enquanto o objeto **Recordset** estiver aberto, as propriedades que definem a natureza do cursor ([CursorType](./cursortype-property-ado.md), [LockType](./locktype-property-ado.md), [MaxRecords](./maxrecords-property-ado.md)e assim por diante) são somente leitura. Assim, o método **Requery** só pode atualizar o cursor atual. Para alterar qualquer uma das propriedades do cursor e exibir os resultados, você deve usar o método [Close](./close-method-ado.md) para que as propriedades se tornem de leitura/gravação novamente. Você pode alterar as configurações de propriedade e chamar o método [Open](./open-method-ado-recordset.md) para reabrir o cursor.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Execute, Requery e Clear (VB)](./execute-requery-and-clear-methods-example-vb.md)   
 [Exemplo dos métodos Execute, Requery e Clear (VBScript)](./execute-requery-and-clear-methods-example-vbscript.md)   
 [Exemplo dos métodos Execute, Requery e Clear (VC + +)](./execute-requery-and-clear-methods-example-vc.md)   
 [Propriedade CommandText (ADO)](./commandtext-property-ado.md)