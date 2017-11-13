---
title: "Método CreateParameter (ADO) | Microsoft Docs"
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
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a7fc09313bffacefd2d9eff86c9176222c094ebe
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="createparameter-method-ado"></a>Método CreateParameter (ADO)
Cria um novo [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto com as propriedades especificadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>Valor de retorno  
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
 Use o **CreateParameter** método para criar um novo **parâmetro** objeto com um nome especificado, o tipo, a direção, o tamanho e o valor. Quaisquer valores que você passa os argumentos são gravados para o correspondente **parâmetro** propriedades.  
  
 Esse método não anexa automaticamente o **parâmetro** o objeto para o **parâmetros** coleção de um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Isso permite que você defina propriedades adicionais, cujo valores ADO será validado quando você acrescentar o **parâmetro** objeto à coleção.  
  
 Se você especificar um tipo de dados de comprimento variável no *tipo* argumento, você deve passar um *tamanho* argumento ou um conjunto de [tamanho](../../../ado/reference/ado-api/size-property-ado-parameter.md) propriedade do **parâmetro**  objeto antes de acrescentá-lo para o **parâmetros** coleção; caso contrário, ocorrerá um erro.  
  
 Se você especificar um tipo de dados numéricos (**adNumeric** ou **adDecimal**) no *tipo* argumento, em seguida, você também deve definir o [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) e [Precisão](../../../ado/reference/ado-api/precision-property-ado.md) propriedades.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Anexar e exemplo dos métodos CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Anexar e exemplo dos métodos CreateParameter (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [(ADO) do método append](../../../ado/reference/ado-api/append-method-ado.md)   
 [Objeto de parâmetro](../../../ado/reference/ado-api/parameter-object.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)

