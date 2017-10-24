---
title: "Mover o método (ADO) | Microsoft Docs"
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
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 69f3ce38f87be4670bcb08f80db076ce88d37212
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="move-method-ado"></a>Método Move (ADO)
Move a posição do registro atual em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *NumRecords*  
 Entrou **longo** expressão que especifica o número de registros move a posição do registro atual.  
  
 *Iniciar*  
 Opcional. Um **cadeia de caracteres** valor ou **Variant** que é avaliada como um indicador. Você também pode usar um [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) valor.  
  
## <a name="remarks"></a>Comentários  
 O **mover** método tem suporte em todos os **registros** objetos.  
  
 Se o *NumRecords* argumento for maior que zero, a posição do registro atual avança (até o fim do **registros**). Se *NumRecords* é menor que zero, a posição atual do registro recua (no início do **registros**).  
  
 Se o **mover** chamada moverá a posição atual do registro para um ponto antes do primeiro registro, o ADO define o registro atual para a posição antes do primeiro registro no conjunto de registros ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é **True **). Tentativa de mover para trás quando o **BOF** propriedade já está **True** gera um erro.  
  
 Se o **mover** chamada moverá a posição atual do registro para um ponto após o último registro, o ADO define o registro atual para a posição após o último registro no conjunto de registros ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é **True **). Tentativa de mover quando encaminhar o **EOF** propriedade já está **True** gera um erro.  
  
 Chamando o **mover** método de vazio **registros** objeto gera um erro.  
  
 Se você passar o *iniciar* argumento, a movimentação é relativo ao registro com esse indicador, supondo que o **registros** objeto dá suporte a indicadores. Se não for especificado, a movimentação é relativo ao registro atual.  
  
 Se você estiver usando o [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propriedade em cache localmente registros do provedor, passando um *NumRecords* argumento que move a posição atual do registro fora do grupo atual de registros armazenado em cache força o ADO para recuperar um novo grupo de registros, a partir do registro de destino. O **CacheSize** propriedade determina o tamanho do grupo recuperado recentemente, e o registro de destino é o primeiro registro recuperado.  
  
 Se o **registros** objeto é somente encaminhada, um usuário ainda pode passar um *NumRecords* argumento menor que zero, fornecido é o destino dentro do conjunto atual de registros armazenado em cache. Se o **mover** chamada seria movidos da posição atual do registro para um registro antes do primeiro registro armazenado em cache, ocorrerá um erro. Assim, você pode usar um cache de registro que oferece suporte à rolagem completos por um provedor que suporte o roll-forward apenas. Porque registros armazenados em cache são carregados na memória, você deve evitar armazenamento em cache registros que não são necessários. Mesmo se um e somente de encaminhamento **registros** move dá suporte ao objeto com versões anteriores dessa forma, ao chamar o [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) método em qualquer somente de encaminhamento **Recordset** objeto ainda Gere um erro.  
  
> [!NOTE]
>  Suporte para mover com versões anteriores em um e somente de encaminhamento **registros** não é previsível, dependendo de seu provedor. Se o registro atual tiver sido posicionado após o último registro de **registros**, **mover** com versões anteriores talvez não resulte na posição atual correta.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método Move (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Exemplo do método Move (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Exemplo do método Move (VC + +)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious métodos (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious métodos (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)

