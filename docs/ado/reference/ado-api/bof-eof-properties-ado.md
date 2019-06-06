---
title: BOF, EOF propriedades (ADO) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 9a449c0e635c7fe0e63bc1f4d8b1b0b91712135d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696283"
---
# <a name="bof-eof-properties-ado"></a>Propriedades BOF, EOF (ADO)
-   **BOF** indica que a posição do registro atual está antes do primeiro registro em um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
-   **EOF** indica que a posição do registro atual é após o último registro de um **Recordset** objeto.  
  
## <a name="return-value"></a>Valor retornado  
 O **BOF** e **EOF** retorno de propriedades **booliano** valores.  
  
## <a name="remarks"></a>Comentários  
 Use o **BOF** e **EOF** propriedades para determinar se um **conjunto de registros** objeto contém registros ou se você passou além dos limites de um **conjunto de registros**  quando você move de um registro para o registro do objeto.  
  
 O **BOF** propriedade retorna **verdadeiro** (-1) se a posição do registro atual está antes do primeiro registro e **False** (0) se a posição do registro atual é em ou após o primeiro Registro.  
  
 O **EOF** propriedade retorna **verdadeiro** se a posição do registro atual é após o último registro e **False** se a posição do registro atual é em ou antes do último registro.  
  
 Se o **BOF** ou **EOF** é de propriedade **verdadeiro**, não há nenhum registro atual.  
  
 Se você abrir um **conjunto de registros** objeto não contendo nenhum registro, o **BOF** e **EOF** propriedades são definidas como **True** (consulte a [ RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propriedade para obter mais informações sobre esse estado de um **Recordset**). Quando você abre um **conjunto de registros** objeto que contém pelo menos um registro, o primeiro registro é o registro atual e o **BOF** e **EOF** propriedades são **False** .  
  
 Se você excluir o último registro restante na **conjunto de registros** objeto, o **BOF** e **EOF** propriedades poderão permanecer **False** até que você tentativa de reposicionar o registro atual.  
  
 Esta tabela mostra quais **mova** métodos são permitidos com diferentes combinações da **BOF** e **EOF** propriedades.  
  
||MoveFirst,<br /><br /> MoveLast|MovePrevious,<br /><br /> Mover < 0|Mover 0|MoveNext,<br /><br /> Mover > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**verdadeiro**, **EOF**=**False**|Allowed (permitido)|Erro|Erro|Allowed (permitido)|  
|**BOF**=**False**, **EOF**=**True**|Allowed (permitido)|Allowed (permitido)|Erro|Erro|  
|Ambos **True**|Erro|Erro|Erro|Erro|  
|Ambos **False**|Allowed (permitido)|Allowed (permitido)|Allowed (permitido)|Allowed (permitido)|  
  
 Permitindo que um **mova** método não garante que o método com êxito será localizar um registro; significa apenas que chamar especificado **mover** método não irá gerar um erro.  
  
 A tabela a seguir mostra o que acontece com o **BOF** e **EOF** configurações de propriedade quando você chama vários **mover** métodos, mas não conseguem localizar com êxito um registro.  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**, **MoveLast**|Definido como **True**|Definido como **True**|  
|**Move** 0|Nenhuma alteração|Nenhuma alteração|  
|**MovePrevious**, **mover** < 0|Definido como **True**|Nenhuma alteração|  
|**MoveNext**, **Move** > 0|Nenhuma alteração|Definido como **True**|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [BOF, EOF e exemplo de propriedades do indicador (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF e exemplo de propriedades do indicador (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
