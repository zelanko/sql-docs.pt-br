---
description: Método GetChunk (ADO)
title: Método GetChunk (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
author: rothja
ms.author: jroth
ms.openlocfilehash: dcf021282d4fce049cd89a154c2d00186b3cbee1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775075"
---
# <a name="getchunk-method-ado"></a>Método GetChunk (ADO)
Retorna todos, ou uma parte, do conteúdo de um objeto de [campo](./field-object.md) de dados binário ou de texto grande.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna uma **variante**.  
  
#### <a name="parameters"></a>Parâmetros  
 *Tamanho*  
 Uma expressão **longa** que é igual ao número de bytes ou caracteres que você deseja recuperar.  
  
## <a name="remarks"></a>Comentários  
 Use o método **GetChunk** em um objeto **Field** para recuperar parte ou todos os seus dados binários ou de caractere longos. Em situações em que a memória do sistema é limitada, você pode usar o método **GetChunk** para manipular valores longos em partes, em vez de em sua totalidade.  
  
 Os dados retornados por uma chamada **GetChunk** são atribuídos à *variável*. Se o *tamanho* for maior que os dados restantes, o método **GetChunk** retornará apenas os dados restantes sem a *variável* de preenchimento com espaços vazios. Se o campo estiver vazio, o método **GetChunk** retornará um valor nulo.  
  
 Cada chamada **GetChunk** subsequente recupera dados a partir de onde a chamada **GetChunk** anterior parou. No entanto, se você estiver recuperando dados de um campo e, em seguida, definir ou ler o valor de outro campo no registro atual, o ADO pressupõe que você concluiu a recuperação de dados do primeiro campo. Se você chamar o método **GetChunk** no primeiro campo, o ADO interpretará a chamada como uma nova operação **GetChunk** e começará a ler a partir do início dos dados. O acesso a campos em outros objetos de [conjunto de registros](./recordset-object-ado.md) que não são clones do primeiro objeto **Recordset** não irá interromper as operações **GetChunk** .  
  
 Se o bit **adFldLong** na propriedade [Attributes](./attributes-property-ado.md) de um objeto **Field** for definido como **true**, você poderá usar o método **GetChunk** para esse campo.  
  
 Se não houver registro atual quando você usar o método **GetChunk** em um objeto **Field** , ocorrerá o erro 3021 (nenhum registro atual).  
  
> [!NOTE]
>  O método **GetChunk** não funciona em objetos de **campo** de um objeto de [registro](./record-object-ado.md) . Ele não executa nenhuma operação e produzirá um erro em tempo de execução.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Campo](./field-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos AppendChunk e GetChunk (VB)](./appendchunk-and-getchunk-methods-example-vb.md)   
 [Exemplo dos métodos AppendChunk e GetChunk (VC + +)](./appendchunk-and-getchunk-methods-example-vc.md)   
 [Método AppendChunk (ADO)](./appendchunk-method-ado.md)   
 [Propriedade Attributes (ADO)](./attributes-property-ado.md)