---
title: Método CreateParameter (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 6cd78e3cbe992a3f2df5046a26eca990479cb3fd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760212"
---
# <a name="createparameter-method-ado"></a>Método CreateParameter (ADO)
Cria um novo objeto de [parâmetro](../../../ado/reference/ado-api/parameter-object.md) com as propriedades especificadas.  
  
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
 Opcional. Um valor de [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) que especifica o tipo de dados do objeto de **parâmetro** .  
  
 *Direção*  
 Opcional. Um valor [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) que especifica o tipo de objeto de **parâmetro** .  
  
 *Tamanho*  
 Opcional. Um valor **longo** que especifica o comprimento máximo para o valor do parâmetro em caracteres ou bytes.  
  
 *Valor*  
 Opcional. Uma **variante** que especifica o valor para o objeto de **parâmetro** .  
  
## <a name="remarks"></a>Comentários  
 Use o método **CreateParameter** para criar um novo objeto de **parâmetro** com um nome, tipo, direção, tamanho e valor especificados. Todos os valores que você passa nos argumentos são gravados nas propriedades do **parâmetro** correspondente.  
  
 Esse método não acrescenta automaticamente o objeto de **parâmetro** à coleção de **parâmetros** de um objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) . Isso permite que você defina propriedades adicionais cujos valores serão validados ao acrescentar o objeto de **parâmetro** à coleção.  
  
 Se você especificar um tipo de dados de comprimento variável no argumento *Type* , deverá passar um argumento *size* ou definir a propriedade [size](../../../ado/reference/ado-api/size-property-ado-parameter.md) do objeto **Parameter** antes de acrescentá-lo à coleção **Parameters** ; caso contrário, ocorrerá um erro.  
  
 Se você especificar um tipo de dados numérico (**adNumeric** ou **adDecimal**) no argumento *Type* , também deverá definir as propriedades [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) e [Precision](../../../ado/reference/ado-api/precision-property-ado.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Append e CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Exemplo dos métodos Append e CreateParameter (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Método Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Objeto de parâmetro](../../../ado/reference/ado-api/parameter-object.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
