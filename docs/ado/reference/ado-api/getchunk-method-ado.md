---
title: Método GetChunk (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d39075e6d3c16540ded137a8ac78ccc6f8d94f8
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278785"
---
# <a name="getchunk-method-ado"></a>Método GetChunk (ADO)
Retorna todos os ou uma parte do conteúdo de um texto grande ou dados binários [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **Variant**.  
  
#### <a name="parameters"></a>Parâmetros  
 *Tamanho*  
 Um **longo** expressão que é igual ao número de bytes ou caracteres que você deseja recuperar.  
  
## <a name="remarks"></a>Remarks  
 Use o **GetChunk** método em um **campo** objeto recuperar parte ou todos os seus dados binários longos ou de caractere. Em situações em que a memória do sistema é limitada, você pode usar o **GetChunk** método para manipular valores longos em partes, em vez de em sua totalidade.  
  
 Os dados que um **GetChunk** chamada retorna é atribuído a *variável*. Se *tamanho* é maior do que os dados restantes, o **GetChunk** método retorna apenas os dados restantes sem preenchimento *variável* com espaços vazios. Se o campo estiver vazio, o **GetChunk** método retorna um valor nulo.  
  
 Cada subsequentes **GetChunk** chamada recupera dados a partir de onde o anterior **GetChunk** chamada parou. No entanto, se você estiver recuperando dados de um campo e, em seguida, definir ou ler o valor de outro campo no registro atual, o ADO pressupõe que você concluiu a recuperação de dados do primeiro campo. Se você chamar o **GetChunk** método no primeiro campo novamente, ADO interpreta a chamada como um novo **GetChunk** operação e começa a leitura do início dos dados. Acessar campos em outros [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objetos que não são clones do primeiro **registros** objeto não interromperá **GetChunk** operações.  
  
 Se o **adFldLong** bit no [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade de um **campo** objeto é definido como **True**, você pode usar o **GetChunk**  método para esse campo.  
  
 Se não houver nenhum registro atual quando você usa o **GetChunk** método em um **campo** do objeto, ocorrerá erro 3021 (não há registro atual).  
  
> [!NOTE]
>  O **GetChunk** método não funcionará em **campo** objetos de um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto. Ele não executará qualquer operação e produzirá um erro de tempo de execução.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [AppendChunk e GetChunk métodos exemplo (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk e GetChunk métodos exemplo (VC + +)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Método AppendChunk (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
