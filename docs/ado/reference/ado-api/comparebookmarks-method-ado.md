---
title: Método CompareBookmarks (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0d737c2f031fa3ba630eabb7e52dff0e056c3390
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919594"
---
# <a name="comparebookmarks-method-ado"></a>Método CompareBookmarks (ADO)
Compara dois indicadores e retorna uma indicação de seus valores relativos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor [CompareEnum](../../../ado/reference/ado-api/compareenum.md) que indica a posição de linha relativa de dois registros representados por seus indicadores.  
  
#### <a name="parameters"></a>Parâmetros  
 *Bookmark1*  
 O indicador da primeira linha.  
  
 *Bookmark2*  
 O indicador da segunda linha.  
  
## <a name="remarks"></a>Comentários  
 Os indicadores devem ser aplicados ao mesmo objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ou a um objeto **Recordset** e seu [clone](../../../ado/reference/ado-api/clone-method-ado.md). Não é possível comparar com confiança os indicadores de objetos diferentes do **conjunto de registros** , mesmo que eles tenham sido criados a partir da mesma fonte ou comando. Nem é possível comparar indicadores para um objeto **Recordset** cujo provedor subjacente não ofereça suporte a comparações.  
  
 Um indicador identifica exclusivamente uma linha em um objeto **Recordset** . Use a propriedade [Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md) da linha atual para obter seu indicador.  
  
 Como o tipo de dados de um indicador é específico para cada provedor, o ADO o expõe como uma **variante**. Por exemplo, SQL Server indicadores são do tipo DBTYPE_R8 (**duplo**). O ADO exporia esse tipo como uma **variante** com um subtipo de **Double**.  
  
 Ao comparar indicadores, o ADO não tenta nenhum tipo de coerção. Os valores são simplesmente passados para o provedor em que ocorre a comparação. Se os indicadores passados para o método **CompareBookmarks** forem armazenados em variáveis de tipos diferentes, ele poderá gerar o seguinte erro de incompatibilidade de tipo: "os argumentos são do tipo incorreto, estão fora do intervalo aceitável ou estão em conflito entre si".  
  
 Um indicador inválido ou formado incorretamente causará um erro.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método CompareBookmarks (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [Exemplo do método CompareBookmarks (VC + +)](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Propriedade Bookmark (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
