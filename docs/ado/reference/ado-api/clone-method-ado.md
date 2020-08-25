---
description: Método Clone (ADO)
title: Método Clone (ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c91960975b04e5c09cf2745e1bb77e7b343dbd2e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776245"
---
# <a name="clone-method-ado"></a>Método Clone (ADO)
Cria um objeto [Recordset](./recordset-object-ado.md) duplicado a partir de um objeto **Recordset** existente. Opcionalmente, especifica que o clone é somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna uma referência de objeto **Recordset** .  
  
#### <a name="parameters"></a>Parâmetros  
 *rstDuplicate*  
 Uma variável de objeto que identifica o objeto de **conjunto de registros** duplicado a ser criado.  
  
 *rstOriginal*  
 Uma variável de objeto que identifica o objeto de **conjunto de registros** a ser duplicado.  
  
 *LockType*  
 Opcional. Um valor de [LockTypeEnum](./locktypeenum.md) que especifica o tipo de bloqueio do **conjunto de registros**original ou um conjunto de **registros**somente leitura. Os valores válidos são **adLockUnspecified** ou **adLockReadOnly**.  
  
## <a name="remarks"></a>Comentários  
 Use o método **clone** para criar vários objetos de **conjunto de registros** duplicados, especialmente se você quiser manter mais de um registro atual em um determinado conjunto de registros. O uso do método **clone** é mais eficiente do que criar e abrir um novo objeto **Recordset** que usa a mesma definição que o original.  
  
 A propriedade [Filter](./filter-property.md) do conjunto de **registros**original, se houver, não será aplicada ao clone. Defina a propriedade **filtro** do novo **conjunto de registros** para filtrar os resultados. A maneira mais simples de copiar qualquer valor de **filtro** existente é atribuí-lo diretamente, como a seguir.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 O registro atual de um clone recentemente criado é definido como o primeiro registro.  
  
 As alterações feitas em um objeto **Recordset** são visíveis em todos os seus clones, independentemente do tipo de cursor. No entanto, depois de executar a [consulta](./requery-method.md) novamente no **conjunto de registros**original, os clones não serão mais sincronizados com o original.  
  
 O fechamento do **conjunto de registros** original não fecha suas cópias, nem fecha uma cópia, fecha o original ou qualquer uma das outras cópias.  
  
 Você só pode clonar um objeto **Recordset** que dê suporte a indicadores. Os valores de indicador são intercambiáveis; ou seja, uma referência de indicador de um objeto **Recordset** refere-se ao mesmo registro em qualquer um de seus clones.  
  
 Alguns eventos do **conjunto de registros** que são disparados também ocorrerão em todos os clones do **conjunto de registros** . No entanto, como o registro atual pode diferir entre **conjuntos de registros**clonados, os eventos podem não ser válidos para o clone. Por exemplo, se você alterar um valor de um campo, um evento [WillChangeField](./willchangefield-and-fieldchangecomplete-events-ado.md) ocorrerá no conjunto de **registros** alterado e em todos os clones. O parâmetro *Fields* do evento **WillChangeField** de um conjunto de **registros** clonado (em que a alteração não foi feita) fará referência aos campos do registro atual do clone, que pode ser um registro diferente do registro atual do **conjunto de registros** original em que a alteração ocorreu.  
  
 A tabela a seguir fornece uma lista completa de todos os eventos do **conjunto de registros** . Ele indica se eles são válidos e disparados para quaisquer clones de conjuntos de registros gerados usando o método **clone** .  
  
|Evento|Disparado em clones?|  
|-----------|--------------------------|  
|[EndOfRecordset](./endofrecordset-event-ado.md)|Não|  
|[FetchComplete](./fetchcomplete-event-ado.md)|Não|  
|[FetchProgress](./fetchprogress-event-ado.md)|Não|  
|[FieldChangeComplete](./willchangefield-and-fieldchangecomplete-events-ado.md)|Sim|  
|[MoveComplete](./willmove-and-movecomplete-events-ado.md)|Não|  
|[RecordChangeComplete](./willchangerecord-and-recordchangecomplete-events-ado.md)|Sim|  
|[RecordsetChangeComplete](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Não|  
|[WillChangeField](./willchangefield-and-fieldchangecomplete-events-ado.md)|Sim|  
|[WillChangeRecord](./willchangerecord-and-recordchangecomplete-events-ado.md)|Sim|  
|[WillChangeRecordset](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Não|  
|[WillMove](./willmove-and-movecomplete-events-ado.md)|Não|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método clone (VB)](./clone-method-example-vb.md)   
 [Exemplo do método clone (VBScript)](./clone-method-example-vbscript.md)   
 [Exemplo do método Clone (VC++)](./clone-method-example-vc.md)