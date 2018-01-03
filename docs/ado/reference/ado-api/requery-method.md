---
title: "Método Requery | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords: Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 90ca81710f2c20929305e894fe2dbda49bb5b3b8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="requery-method"></a>Método Requery
Atualiza os dados em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto executar novamente a consulta na qual o objeto se baseia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Opções*  
 Opcional. Uma máscara de bits que contém [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) e [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valores que afetam esta operação.  
  
> [!NOTE]
>  Se *opções* é definido como **adAsyncExecute**, esta operação será executado de forma assíncrona e um [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) evento será emitido quando ele é concluído. O **ExecuteOpenEnum** valores de **adExecuteNoRecords** ou **adExecuteStream** não deve ser usada com **Requery**.  
  
## <a name="remarks"></a>Remarks  
 Use o **Requery** método para atualizar todo o conteúdo de um **registros** objeto da fonte de dados, emitir novamente o comando original e recuperando os dados uma segunda vez. Chamar esse método é equivalente a chamar o [fechar](../../../ado/reference/ado-api/close-method-ado.md) e [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) métodos em sucessão. Se você estiver editando o registro atual ou adicionar um novo registro, ocorrerá um erro.  
  
 Enquanto o **registros** estiver aberto, as propriedades que definem a natureza do cursor ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md), [LockType](../../../ado/reference/ado-api/locktype-property-ado.md), [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md) e assim por diante) são somente leitura. Portanto, o **Requery** método só pode atualizar o cursor atual. Para alterar qualquer uma das propriedades de cursor e exibir os resultados, você deve usar o [fechar](../../../ado/reference/ado-api/close-method-ado.md) método para que as propriedades se tornar somente leitura novamente. Você pode alterar as configurações de propriedade e a chamada a [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método para reabrir o cursor.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Execute, repetir e limpar o exemplo de métodos (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, repetir e limpar o exemplo de métodos (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, repetir e limpar o exemplo de métodos (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
