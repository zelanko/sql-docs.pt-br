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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 251c35977421d63027fbc9d6042e193125da854d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695641"
---
# <a name="createparameter-method-ado"></a>Método CreateParameter (ADO)
Cria um novo [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto com as propriedades especificadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **parâmetro** objeto.  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Opcional. Um **cadeia de caracteres** que contém o nome do valor de **parâmetro** objeto.  
  
 *Tipo*  
 Opcional. Um [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valor que especifica o tipo de dados de **parâmetro** objeto.  
  
 *Direção*  
 Opcional. Um [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) valor que especifica o tipo de **parâmetro** objeto.  
  
 *Tamanho*  
 Opcional. Um **longo** valor que especifica o comprimento máximo para o valor do parâmetro em caracteres ou bytes.  
  
 *Value*  
 Opcional. Um **Variant** que especifica o valor para o **parâmetro** objeto.  
  
## <a name="remarks"></a>Comentários  
 Use o **CreateParameter** método para criar uma nova **parâmetro** objeto com um nome especificado, o tipo, a direção, o tamanho e o valor. Quaisquer valores que você passe os argumentos são gravados para os respectivos **parâmetro** propriedades.  
  
 Esse método não anexa automaticamente os **parâmetro** do objeto para o **parâmetros** coleção de um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Isso permite que você defina propriedades adicionais ADO cujos valores validará quando você acrescenta o **parâmetro** objeto à coleção.  
  
 Se você especificar um tipo de dados de comprimento variável no *tipo* argumento, você deve passar um *tamanho* argumento ou um conjunto de [tamanho](../../../ado/reference/ado-api/size-property-ado-parameter.md) propriedade do **parâmetro**  objeto antes de acrescentá-lo para o **parâmetros** coleção; caso contrário, ocorrerá um erro.  
  
 Se você especificar um tipo de dados numéricos (**adNumeric** ou **adDecimal**) na *tipo* argumento, em seguida, você também deve definir o [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) e [Precisão](../../../ado/reference/ado-api/precision-property-ado.md) propriedades.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Acrescente e exemplo dos métodos CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Append e CreateParameter métodos (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Método append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Objeto de parâmetro](../../../ado/reference/ado-api/parameter-object.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
