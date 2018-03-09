---
title: "Método CompareBookmarks (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 431ffdb1a2be03404b4d0c3636f547b6c8cf8514
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="comparebookmarks-method-ado"></a>Método CompareBookmarks (ADO)
Compara dois indicadores e retorna uma indicação de seus valores relativos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um [CompareEnum](../../../ado/reference/ado-api/compareenum.md) valor que indica a posição de linha relativa de dois registros representados por seus indicadores.  
  
#### <a name="parameters"></a>Parâmetros  
 *Bookmark1*  
 O indicador da primeira linha.  
  
 *Bookmark2*  
 O marcador da segunda linha.  
  
## <a name="remarks"></a>Remarks  
 Os indicadores devem aplicar o mesmo [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, ou um **registros** objeto e seu [clone](../../../ado/reference/ado-api/clone-method-ado.md). Você não pode comparar confiável indicadores de diferentes **registros** objetos, mesmo se elas foram criadas da mesma fonte ou do comando. Ou você pode comparar indicadores para uma **registros** objeto cujo provedor subjacente não oferece suporte a comparações.  
  
 Um indicador identifica exclusivamente uma linha em uma **registros** objeto. Use o [indicador](../../../ado/reference/ado-api/bookmark-property-ado.md) propriedade da linha atual para obter seu indicador.  
  
 Como o tipo de dados de um indicador é específico para cada provedor, ADO expõe como uma **Variant**. Por exemplo, os indicadores do SQL Server são do tipo DBTYPE_R8 (**duplo**). ADO poderia expor este tipo como um **Variant** com um subtipo de **duplo**.  
  
 Ao comparar os indicadores, ADO não tenta executar qualquer tipo de coerção. Apenas os valores são passados para o provedor de onde ocorre a comparação. Se os indicadores passado para o **CompareBookmarks** método são armazenados em variáveis de tipos diferentes, ele pode gerar o seguinte erro de incompatibilidade de tipo: "argumentos são do tipo errado, estão fora do intervalo aceitável ou estão em conflito com o outro."  
  
 Um indicador que não é válido ou formado incorretamente causará um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método CompareBookmarks (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [Exemplo do método CompareBookmarks (VC + +)](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Propriedade Bookmark (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
