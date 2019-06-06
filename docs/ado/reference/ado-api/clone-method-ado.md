---
title: Método clone (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fbeedf9e56c1f0606a7c8f842baedc9d11ad3929
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698801"
---
# <a name="clone-method-ado"></a>Método Clone (ADO)
Cria uma duplicata [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto de uma já existente **Recordset** objeto. Opcionalmente, especifica que o clone ser somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **Recordset** referência de objeto.  
  
#### <a name="parameters"></a>Parâmetros  
 *rstDuplicate*  
 Uma variável de objeto que identifica a duplicata **Recordset** objeto a ser criado.  
  
 *rstOriginal*  
 Uma variável de objeto que identifica o **Recordset** objeto a ser duplicado.  
  
 *LockType*  
 Opcional. Um [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valor que especifica o tipo de bloqueio do original **conjunto de registros**, ou somente leitura **conjunto de registros**. Os valores válidos são **adLockUnspecified** ou **adLockReadOnly**.  
  
## <a name="remarks"></a>Comentários  
 Use o **Clone** duplicado de método para criar vários **Recordset** objetos, especialmente se você desejar manter mais de um registro atual em um determinado conjunto de registros. Usando o **Clone** método é mais eficiente do que criar e abrir uma nova **Recordset** objeto que usa a mesma definição do original.  
  
 O [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade do original **conjunto de registros**, se houver, não será aplicada para o clone. Defina as **filtro** propriedade da nova **Recordset** para filtrar os resultados. A maneira mais simples para copiar todos os existentes **filtro** valor é atribuí-lo diretamente, da seguinte maneira.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 O registro atual de um clone criado recentemente é definido como o primeiro registro.  
  
 As alterações feitas a um **Recordset** objeto são visíveis em todos os seus clones, independentemente do tipo de cursor. No entanto, depois de executar [Requery](../../../ado/reference/ado-api/requery-method.md) no original **conjunto de registros**, os clones não serão sincronizados ao original.  
  
 Fechando o original **Recordset** não fecha suas cópias, nem o fechamento Feche uma cópia original ou qualquer uma das outras cópias.  
  
 Você só pode clonar uma **Recordset** objeto que dá suporte a indicadores. Valores de indicador são intercambiáveis; ou seja, uma referência de indicador de um **Recordset** objeto refere-se no mesmo registro em qualquer um de seus clones.  
  
 Alguns **conjunto de registros** eventos que são disparados também ocorrerá em todas as **Recordset** clones. No entanto, porque o registro atual pode diferir entre clonado **conjuntos de registros**, os eventos podem não ser válidos para o clone. Por exemplo, se você alterar um valor de um campo, uma [eventos WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md) evento ocorrerá no alterados **Recordset** e em todos os clones. O *campos* parâmetro do **eventos WillChangeField** eventos de clonado **Recordset** (em que a alteração não foi feita) fará referência aos campos do registro atual do clone, o que pode ser um registro diferente que o registro atual do original **Recordset** onde ocorreu a alteração.  
  
 A tabela a seguir fornece uma lista completa de todos os **Recordset** eventos. Ele indica se eles são válidos e disparada para qualquer clones de conjunto de registros gerados usando o **Clone** método.  
  
|Evento|Disparada em clones?|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|Não|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|Não|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|Não|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Sim|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Não|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Sim|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Não|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Sim|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Sim|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Não|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Não|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método clone (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [Exemplo do método clone (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Exemplo do método Clone (VC++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   
