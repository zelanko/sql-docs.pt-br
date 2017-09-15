---
title: "Método (ADO) clone | Microsoft Docs"
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
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9b7586bef017cd4e5f3a89586b8600abfd183f5a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="clone-method-ado"></a>Método clone (ADO)
Cria uma duplicata [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto a partir de um existente **registros** objeto. Opcionalmente, especifica que o clone ser somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **registros** referência de objeto.  
  
#### <a name="parameters"></a>Parâmetros  
 *rstDuplicate*  
 Uma variável de objeto que identifica a duplicata **registros** objeto a ser criado.  
  
 *rstOriginal*  
 Uma variável de objeto que identifica o **registros** objeto a ser duplicado.  
  
 *LockType*  
 Opcional. Um [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valor que especifica o tipo de bloqueio do original **registros**, ou somente leitura **registros**. Os valores válidos são **adLockUnspecified** ou **adLockReadOnly**.  
  
## <a name="remarks"></a>Comentários  
 Use o **Clone** duplicado de método para criar vários **registros** objetos, especialmente se você deseja manter mais de um registro atual em um determinado conjunto de registros. Usando o **Clone** método é mais eficiente do que criar e abrir um novo **registros** objeto que usa a mesma definição original.  
  
 O [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade do original **registros**, se houver, não será aplicado ao clone. Definir o **filtro** propriedade do novo **registros** para filtrar os resultados. A maneira mais simples para copiar todos os existentes **filtro** valor é atribuí-lo diretamente, da seguinte maneira.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 O registro atual de um clone criado recentemente é definido como o primeiro registro.  
  
 As alterações feitas a um **registros** objeto são visíveis em todos os seus clones independentemente do tipo de cursor. No entanto, após você executar [Requery](../../../ado/reference/ado-api/requery-method.md) no original **registros**, os clones não serão sincronizados com o original.  
  
 Fechando o original **registros** não fechar suas cópias, nem o fechamento fechar uma cópia original ou qualquer uma das outras cópias.  
  
 Você só pode clonar um **registros** objeto que dá suporte a indicadores. Valores de indicador são intercambiáveis; ou seja, uma referência de indicador de um **registros** objeto refere-se para o mesmo registro em qualquer um de seus clones.  
  
 Alguns **registros** eventos disparados também ocorrerá em todos os **registros** clones. No entanto, porque o registro atual pode diferir entre clonado **conjuntos de registros**, os eventos podem não ser válidos para o clone. Por exemplo, se você alterar um valor de um campo, uma [WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md) evento ocorrerá no alterado **registros** e em todos os clones. O *campos* parâmetro do **WillChangeField** evento clonado **registros** (onde a alteração não foi feita) fará referência aos campos de registro atual do clone, que pode ser um registro diferente que o registro atual do original **registros** onde a alteração ocorreu.  
  
 A tabela a seguir fornece uma lista completa de todos os **registros** eventos. Indica se forem válidos e disparada para qualquer clones de conjunto de registros gerados por meio de **Clone** método.  
  
|Evento|Disparado em clones?|  
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

