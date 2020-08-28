---
description: Método Move (ADO)
title: Método Move (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b394d64a9d1b1f403137e9875db83fdd82c2ac1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990587"
---
# <a name="move-method-ado"></a>Método Move (ADO)
Move a posição do registro atual em um objeto [Recordset](./recordset-object-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *NumRecords*  
 Uma expressão **longa** assinada que especifica o número de registros movidos pela posição do registro atual.  
  
 *Iniciar*  
 Opcional. Um valor de **cadeia de caracteres** ou uma **variante** que é avaliada como um indicador. Você também pode usar um valor [BookmarkEnum](./bookmarkenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Há suporte para o método **move** em todos os objetos **Recordset** .  
  
 Se o argumento *NumRecords* for maior que zero, a posição do registro atual avançará (em direção ao final do **conjunto de registros**). Se *NumRecords* for menor que zero, a posição do registro atual mudará para trás (em direção ao início do **conjunto de registros**).  
  
 Se a chamada de **movimentação** mover a posição do registro atual para um ponto antes do primeiro registro, o ADO definirá o registro atual como a posição anterior ao primeiro registro no conjunto de registros ([BOF](./bof-eof-properties-ado.md) é **true**). Uma tentativa de retroceder quando a propriedade **BOF** já é **verdadeira** gera um erro.  
  
 Se a chamada de **movimentação** mover a posição do registro atual para um ponto após o último registro, o ADO definirá o registro atual como a posição após o último registro no conjunto de registros ([EOF](./bof-eof-properties-ado.md) é **true**). Uma tentativa de avançar quando a propriedade **EOF** já é **verdadeira** gera um erro.  
  
 Chamar o método **move** de um objeto **Recordset** vazio gera um erro.  
  
 Se você passar o argumento *Start* , a movimentação será relativa ao registro com esse indicador, supondo que o objeto **Recordset** dê suporte a indicadores. Se não for especificado, a movimentação será relativa ao registro atual.  
  
 Se você estiver usando a propriedade [CacheSize](./cachesize-property-ado.md) para armazenar localmente os registros do provedor, passar um argumento *NumRecords* que move a posição do registro atual para fora do grupo atual de registros em cache força o ADO a recuperar um novo grupo de registros, a partir do registro de destino. A propriedade **CacheSize** determina o tamanho do grupo recuperado recentemente e o registro de destino é o primeiro registro recuperado.  
  
 Se o objeto **Recordset** for somente encaminhamento, um usuário ainda poderá passar um argumento *NumRecords* menor que zero, desde que o destino esteja dentro do conjunto atual de registros armazenados em cache. Se a chamada de **movimentação** mover a posição do registro atual para um registro antes do primeiro registro em cache, ocorrerá um erro. Portanto, você pode usar um cache de registro que dá suporte à rolagem completa em um provedor que dá suporte apenas à rolagem de encaminhamento. Como os registros armazenados em cache são carregados na memória, você deve evitar armazenar em cache mais registros do que o necessário. Mesmo que um objeto **Recordset** somente de encaminhamento dê suporte a movimentações para trás dessa forma, chamar o método [MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) em qualquer objeto **Recordset** somente de encaminhamento ainda gerará um erro.  
  
> [!NOTE]
>  O suporte para mover para trás em um **conjunto de registros** somente de encaminhamento não é previsível, dependendo do seu provedor. Se o registro atual tiver sido posicionado após o último registro no **conjunto de registros**, **mover** para trás pode não resultar na posição atual correta.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Move (VB)](./move-method-example-vb.md)   
 [Exemplo do método Move (VBScript)](./move-method-example-vbscript.md)   
 [Exemplo do método Move (VC + +)](./move-method-example-vc.md)   
 [Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (ADO)](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (RDS)](../rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](./moverecord-method-ado.md)