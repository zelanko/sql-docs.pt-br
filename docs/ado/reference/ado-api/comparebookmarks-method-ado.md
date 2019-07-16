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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919594"
---
# <a name="comparebookmarks-method-ado"></a>Método CompareBookmarks (ADO)
Compara dois indicadores e retorna uma indicação dos valores relativos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um [CompareEnum](../../../ado/reference/ado-api/compareenum.md) valor que indica a posição de linha relativa de dois registros representado por seus indicadores.  
  
#### <a name="parameters"></a>Parâmetros  
 *Bookmark1*  
 O indicador da primeira linha.  
  
 *Bookmark2*  
 O indicador da segunda linha.  
  
## <a name="remarks"></a>Comentários  
 Os indicadores devem aplicar o mesmo [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, ou uma **conjunto de registros** objeto e seu [clone](../../../ado/reference/ado-api/clone-method-ado.md). Você não pode comparar com confiança indicadores de diferentes **Recordset** objetos, mesmo que elas foram criadas da mesma fonte ou do comando. Nem você pode comparar indicadores para uma **Recordset** cujo provedor subjacente não oferece suporte a comparações de objeto.  
  
 Um indicador identifica exclusivamente uma linha em uma **Recordset** objeto. Use o [indicador](../../../ado/reference/ado-api/bookmark-property-ado.md) propriedade da linha atual para obter seu indicador.  
  
 Como o tipo de dados de um indicador é específico para cada provedor, o ADO expõe-o como uma **Variant**. Por exemplo, os indicadores do SQL Server são do tipo DBTYPE_R8 (**duplas**). ADO poderia expor esse tipo como uma **Variant** com um subtipo do **duplo**.  
  
 Ao comparar os indicadores, ADO não tenta fazer qualquer tipo de coerção. Os valores são simplesmente passados para o provedor de onde ocorre a comparação. Se os indicadores são passados para o **CompareBookmarks** método são armazenadas em variáveis de tipos diferentes, ele pode gerar o seguinte erro de incompatibilidade de tipo: "Argumentos são do tipo errado, estão fora do intervalo aceitável ou estão em conflito com uns aos outros."  
  
 Um indicador que não é válido ou formado incorretamente causará um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método CompareBookmarks (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [Exemplo do método CompareBookmarks (VC + +)](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Propriedade Bookmark (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
