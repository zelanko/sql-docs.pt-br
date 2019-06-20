---
title: Método Move (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c7b99a0848101ca0fad4844c51e44f1ccc628cd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66707602"
---
# <a name="move-method-ado"></a>Método Move (ADO)
Move a posição do registro atual em um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *NumRecords*  
 Com um sinal **longo** expressão que especifica o número de registros que move a posição do registro atual.  
  
 *Iniciar*  
 Opcional. Um **cadeia de caracteres** valor ou **Variant** que é avaliada como um indicador. Você também pode usar um [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) valor.  
  
## <a name="remarks"></a>Comentários  
 O **mova** método tem suporte em todos os **Recordset** objetos.  
  
 Se o *NumRecords* argumento for maior que zero, a posição atual do registro move para frente (até o final do **Recordset**). Se *NumRecords* é menor que zero, a posição atual do registro move para trás (até o início de **Recordset**).  
  
 Se o **mova** chamada moveria a posição do registro atual para um ponto antes do primeiro registro, o ADO define o registro atual para a posição antes do primeiro registro no conjunto de registros ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é **True** ). Tentativa de mover quando com versões anteriores a **BOF** propriedade já está **verdadeiro** gera um erro.  
  
 Se o **mova** chamada moveria a posição do registro atual para um ponto após o último registro, o ADO define o registro atual para a posição após o último registro no conjunto de registros ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é **True** ). Tentativa de mover o encaminhamento quando o **EOF** propriedade já está **verdadeiro** gera um erro.  
  
 Chamar o **mova** método vazio **Recordset** objeto gera um erro.  
  
 Se você passar o *inicie* argumento, a movimentação é relativo ao registro com esse indicador, supondo que o **Recordset** objeto dá suporte a indicadores. Se não for especificado, a movimentação é relativo ao registro atual.  
  
 Se você estiver usando o [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propriedade em cache localmente os registros do provedor, de passando um *NumRecords* argumento que move a posição atual do registro fora do grupo atual de registros armazenados em cache força o ADO para recuperar um novo grupo de registros, começando do registro de destino. O **CacheSize** propriedade determina o tamanho do grupo recém-recuperado e o registro de destino é o primeiro registro recuperado.  
  
 Se o **conjunto de registros** objeto é somente encaminhada, um usuário ainda pode passar um *NumRecords* argumento menor que zero, desde que o destino seja dentro do conjunto atual de registros armazenados em cache. Se o **mover** chamada moveria a posição do registro atual para um registro antes do primeiro registro armazenado em cache, ocorrerá um erro. Assim, você pode usar um cache de registro que oferece suporte à rolagem completa ao longo de um provedor que dá suporte a apenas roll-forward. Porque registros armazenados em cache são carregados na memória, você deve evitar o armazenamento em cache os registros que não são necessárias. Mesmo se um somente de avanço **conjunto de registros** dá suporte ao objeto com versões anteriores move dessa forma, chamar o [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) método em qualquer somente de avanço **Recordset** objeto ainda Gere um erro.  
  
> [!NOTE]
>  Suporte para mover para trás em uma somente de avanço **Recordset** é imprevisível, dependendo do seu provedor. Se o registro atual tiver sido posicionado após o último registro a **conjunto de registros**, **mover** com versões anteriores talvez não resulte na posição atual do correta.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método Move (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Exemplo do método Move (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Exemplo do método Move (VC + +)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious métodos (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious métodos (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
