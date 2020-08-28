---
description: Método CreateParameter (ADO)
title: Método CreateParameter (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
author: rothja
ms.author: jroth
ms.openlocfilehash: 8fd075dff5ae67c7965082a9b7d0f75f5c4d47eb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974477"
---
# <a name="createparameter-method-ado"></a>Método CreateParameter (ADO)
Cria um novo objeto de [parâmetro](./parameter-object.md) com as propriedades especificadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um objeto de **parâmetro** .  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Opcional. Um valor de **cadeia de caracteres** que contém o nome do objeto de **parâmetro** .  
  
 *Tipo*  
 Opcional. Um valor de [DataTypeEnum](./datatypeenum.md) que especifica o tipo de dados do objeto de **parâmetro** .  
  
 *Direção*  
 Opcional. Um valor [ParameterDirectionEnum](./parameterdirectionenum.md) que especifica o tipo de objeto de **parâmetro** .  
  
 *Tamanho*  
 Opcional. Um valor **longo** que especifica o comprimento máximo para o valor do parâmetro em caracteres ou bytes.  
  
 *Valor*  
 Opcional. Uma **variante** que especifica o valor para o objeto de **parâmetro** .  
  
## <a name="remarks"></a>Comentários  
 Use o método **CreateParameter** para criar um novo objeto de **parâmetro** com um nome, tipo, direção, tamanho e valor especificados. Todos os valores que você passa nos argumentos são gravados nas propriedades do **parâmetro** correspondente.  
  
 Esse método não acrescenta automaticamente o objeto de **parâmetro** à coleção de **parâmetros** de um objeto de [comando](./command-object-ado.md) . Isso permite que você defina propriedades adicionais cujos valores serão validados ao acrescentar o objeto de **parâmetro** à coleção.  
  
 Se você especificar um tipo de dados de comprimento variável no argumento *Type* , deverá passar um argumento *size* ou definir a propriedade [size](./size-property-ado-parameter.md) do objeto **Parameter** antes de acrescentá-lo à coleção **Parameters** ; caso contrário, ocorrerá um erro.  
  
 Se você especificar um tipo de dados numérico (**adNumeric** ou **adDecimal**) no argumento *Type* , também deverá definir as propriedades [NumericScale](./numericscale-property-ado.md) e [Precision](./precision-property-ado.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Append e CreateParameter (VB)](./append-and-createparameter-methods-example-vb.md)   
 [Exemplo dos métodos Append e CreateParameter (VC + +)](./append-and-createparameter-methods-example-vc.md)   
 [Método Append (ADO)](./append-method-ado.md)   
 [Objeto de parâmetro](./parameter-object.md)   
 [Coleção Parameters (ADO)](./parameters-collection-ado.md)