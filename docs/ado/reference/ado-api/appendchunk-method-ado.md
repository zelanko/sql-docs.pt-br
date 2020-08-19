---
description: Método AppendChunk (ADO)
title: Método AppendChunk (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
author: rothja
ms.author: jroth
ms.openlocfilehash: 290155a3e6ea7e8ec0110d2bc2672cc74f6895b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451228"
---
# <a name="appendchunk-method-ado"></a>Método AppendChunk (ADO)
Anexa dados a um [campo](../../../ado/reference/ado-api/field-object.md)de dados binário ou de texto grande ou a um objeto de [parâmetro](../../../ado/reference/ado-api/parameter-object.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *object*  
 Um **campo** ou objeto de **parâmetro** .  
  
 *Dados*  
 Uma **variante** que contém os dados a serem acrescentados ao objeto.  
  
## <a name="remarks"></a>Comentários  
 Use o método **AppendChunk** em um **campo** ou objeto de **parâmetro** para preenchê-lo com dados binários longos ou de caracteres. Em situações em que a memória do sistema é limitada, você pode usar o método **AppendChunk** para manipular valores longos em partes, em vez de em sua totalidade.  
  
## <a name="field"></a>Campo  
 Se o bit **adFldLong** na propriedade [Attributes](../../../ado/reference/ado-api/attributes-property-ado.md) de um objeto **Field** for definido como **true**, você poderá usar o método **AppendChunk** para esse campo.  
  
 A primeira chamada **AppendChunk** em um objeto **Field** grava dados no campo, substituindo os dados existentes. As chamadas **AppendChunk** subsequentes são adicionadas aos dados existentes. Se você estiver acrescentando dados a um campo e, em seguida, definir ou ler o valor de outro campo no registro atual, o ADO assumirá que você terminou de acrescentar dados ao primeiro campo. Se você chamar o método **AppendChunk** no primeiro campo novamente, o ADO interpretará a chamada como uma nova operação **AppendChunk** e substituirá os dados existentes. O acesso a campos em outros objetos [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) que não são clones do primeiro objeto **Recordset** não irá interromper as operações de **AppendChunk** .  
  
 Se não houver registro atual quando você chamar **AppendChunk** em um objeto **Field** , ocorrerá um erro.  
  
> [!NOTE]
>  O método **AppendChunk** não funciona em objetos de **campo** de um objeto de [registro (ADO)](../../../ado/reference/ado-api/record-object-ado.md) . Ele não executa nenhuma operação e produzirá um erro em tempo de execução.  
  
## <a name="parameter"></a>Parâmetro  
 Se o bit **adParamLong** na propriedade **Attributes** de um objeto **Parameter** for definido como **true**, você poderá usar o método **AppendChunk** para esse parâmetro.  
  
 A primeira chamada **AppendChunk** em um objeto de **parâmetro** grava dados no parâmetro, substituindo todos os dados existentes. As chamadas **AppendChunk** subsequentes em um objeto de **parâmetro** são adicionadas aos dados de parâmetro existentes. Uma chamada **AppendChunk** que passa um valor nulo descarta todos os dados de parâmetro.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Campo](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos AppendChunk e GetChunk (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [Exemplo dos métodos AppendChunk e GetChunk (VC + +)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [Método GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
