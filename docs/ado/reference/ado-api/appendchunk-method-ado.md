---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9d575460daf0f801f6d6dd2e80b0c67f4886dc7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920560"
---
# <a name="appendchunk-method-ado"></a>Método AppendChunk (ADO)
Acrescenta dados a um grande de texto ou dados binários [campo](../../../ado/reference/ado-api/field-object.md), ou como um [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *object*  
 Um **campo** ou **parâmetro** objeto.  
  
 *Dados*  
 Um **Variant** que contém os dados para acrescentar ao objeto.  
  
## <a name="remarks"></a>Comentários  
 Use o **AppendChunk** método em um **campo** ou **parâmetro** objeto preenchê-lo com dados binários longos ou de caractere. Em situações em que a memória do sistema é limitada, você pode usar o **AppendChunk** método para manipular valores longos em partes em vez de em sua totalidade.  
  
## <a name="field"></a>Campo  
 Se o **adFldLong** bit na [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade de um **campo** objeto é definido como **true**, você pode usar o  **AppendChunk** método para esse campo.  
  
 A primeira **AppendChunk** chamar em um **campo** objeto grava dados no campo, substituindo quaisquer dados existentes. Subsequentes **AppendChunk** chamadas adicionam aos dados existentes. Se você está anexando dados a um campo e, em seguida, você pode definir ou ler o valor de outro campo no registro atual, o ADO pressupõe que você esteja concluído acrescentando dados para o primeiro campo. Se você chamar o **AppendChunk** método no primeiro campo novamente, ADO interpreta a chamada como um novo **AppendChunk** operação e substitui os dados existentes. Acessar campos em outros [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objetos que não são clones do primeiro **conjunto de registros** objeto não interromperá **AppendChunk** operações.  
  
 Se não houver nenhum registro atual quando você chama **AppendChunk** em um **campo** do objeto, ocorrerá um erro.  
  
> [!NOTE]
>  O **AppendChunk** método não funciona em **campo** objetos de um [registro Object (ADO)](../../../ado/reference/ado-api/record-object-ado.md) objeto. Ele não executará qualquer operação e produzirá um erro de tempo de execução.  
  
## <a name="parameter"></a>Parâmetro  
 Se o **adParamLong** bit na **atributos** propriedade de um **parâmetro** objeto é definido como **true**, você pode usar o  **AppendChunk** método para esse parâmetro.  
  
 A primeira **AppendChunk** chamar em um **parâmetro** objeto grava os dados para o parâmetro, substituindo quaisquer dados existentes. Subsequentes **AppendChunk** chama em um **parâmetro** objeto adicionar aos dados existentes do parâmetro. Uma **AppendChunk** chamada que transmite um valor nulo descarta todos os dados de parâmetro.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de AppendChunk e GetChunk exemplo dos métodos (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk e GetChunk métodos (VC + +)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [Método GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
