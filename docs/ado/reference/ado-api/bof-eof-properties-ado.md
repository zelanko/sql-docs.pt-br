---
title: Propriedades BOF, EOF (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4932d3349c2d4e2948ddd28d9df3a30424064dcb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920382"
---
# <a name="bof-eof-properties-ado"></a>Propriedades BOF, EOF (ADO)
-   **BOF** Indica que a posição atual do registro é anterior ao primeiro registro em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
-   **EOF** Indica que a posição atual do registro é posterior ao último registro em um objeto **Recordset** .  
  
## <a name="return-value"></a>Valor retornado  
 As propriedades **BOF** e **EOF** retornam valores **boolianos** .  
  
## <a name="remarks"></a>Comentários  
 Use as propriedades **BOF** e **EOF** para determinar se um objeto **Recordset** contém registros ou se você ultrapassou os limites de um objeto **Recordset** quando você move de registro para registro.  
  
 A propriedade **BOF** retornará **true** (-1) se a posição atual do registro for anterior ao primeiro registro e **false** (0) se a posição atual do registro for no ou após o primeiro registro.  
  
 A propriedade **EOF** retornará **true** se a posição atual do registro for posterior ao último registro e **false** se a posição do registro atual for no ou antes do último registro.  
  
 Se a propriedade **BOF** ou **EOF** for **true**, não haverá registro atual.  
  
 Se você abrir um objeto **Recordset** que não contém nenhum registro, as propriedades **BOF** e **EOF** serão definidas como **true** (consulte a propriedade [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) para obter mais informações sobre esse estado de um **conjunto de registros**). Quando você abre um objeto **Recordset** que contém pelo menos um registro, o primeiro registro é o registro atual e as propriedades **BOF** e **EOF** são **false**.  
  
 Se você excluir o último registro restante no objeto **Recordset** , as propriedades **BOF** e **EOF** poderão permanecer **falsas** até que você tente reposicionar o registro atual.  
  
 Esta tabela mostra quais métodos de **movimentação** são permitidos com combinações diferentes das propriedades **BOF** e **EOF** .  
  
||MoveFirst<br /><br /> Velas|MovePrevious<br /><br /> Mover < 0|Mover 0|MoveNext<br /><br /> Mover > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**true**, **EOF**=**false**|Permitido|Erro|Erro|Permitido|  
|**BOF**=**false**, **EOF**=**true**|Permitido|Permitido|Erro|Erro|  
|Ambos **verdadeiros**|Erro|Erro|Erro|Erro|  
|Ambos **falsos**|Permitido|Permitido|Permitido|Permitido|  
  
 Permitir um método de **movimentação** não garante que o método localizará um registro com êxito; Isso significa apenas que chamar o método de **movimentação** especificado não gerará um erro.  
  
 A tabela a seguir mostra o que acontece com as configurações de propriedade **BOF** e **EOF** quando você chama vários métodos **move** , mas não consegue localizar um registro com êxito.  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**, **MoveLast**|Definir como **true**|Definir como **true**|  
|**Mover** 0|Nenhuma alteração|Nenhuma alteração|  
|**MovePrevious**, **mover** < 0|Definir como **true**|Nenhuma alteração|  
|**MoveNext**, **mover** > 0|Nenhuma alteração|Definir como **true**|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades BOF, EOF e Bookmark (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [Exemplo das propriedades BOF, EOF e Bookmark (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
