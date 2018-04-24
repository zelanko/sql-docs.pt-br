---
title: BOF, propriedades EOF (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1941b22639091d673bb687c3ae8b2d9ea1fdf063
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="bof-eof-properties-ado"></a>BOF, propriedades EOF (ADO)
-   **BOF** indica que a posição do registro atual é antes do primeiro registro em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
-   **EOF** indica que a posição do registro atual é após o último registro de um **registros** objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 O **BOF** e **EOF** propriedades retorno **booliano** valores.  
  
## <a name="remarks"></a>Remarks  
 Use o **BOF** e **EOF** propriedades para determinar se um **registros** objeto contiver registros ou se você tiver feito além dos limites de um **conjunto de registros**  quando você move de registro para registro do objeto.  
  
 O **BOF** propriedade retorna **True** (-1) se a posição do registro atual é anterior ao primeiro registro e **False** (0) se a posição atual do registro está em ou depois do primeiro Registro.  
  
 O **EOF** propriedade retorna **True** se a posição do registro atual é posterior ao último registro e **False** se a posição atual do registro está em ou antes do último registro.  
  
 Se o **BOF** ou **EOF** é de propriedade **True**, há um registro atual.  
  
 Se você abrir um **registros** objeto que não contenha registros, o **BOF** e **EOF** propriedades são definidas como **True** (consulte a [ RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propriedade para obter mais informações sobre esse estado de um **registros**). Quando você abre um **registros** objeto que contém pelo menos um registro, o primeiro registro é o registro atual e o **BOF** e **EOF** propriedades são **False** .  
  
 Se você excluir o último registro restante no **registros** objeto, o **BOF** e **EOF** propriedades podem permanecer **False** até que você tentativa de reposicionar o registro atual.  
  
 Esta tabela mostra qual **mover** métodos são permitidos com diferentes combinações do **BOF** e **EOF** propriedades.  
  
||MoveFirst,<br /><br /> MoveLast|MovePrevious,<br /><br /> Mover < 0|Mover 0|MoveNext,<br /><br /> Mover > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**True**, **EOF**=**False**|Allowed (permitido)|Erro|Erro|Allowed (permitido)|  
|**BOF**=**False**, **EOF**=**True**|Allowed (permitido)|Allowed (permitido)|Erro|Erro|  
|Ambos **True**|Erro|Erro|Erro|Erro|  
|Ambos **False**|Allowed (permitido)|Allowed (permitido)|Allowed (permitido)|Allowed (permitido)|  
  
 Permitir que um **mover** método não garante que o método com êxito localizará um registro; significa apenas que chamar especificado **mover** método não irá gerar um erro.  
  
 A tabela a seguir mostra o que acontece com o **BOF** e **EOF** as configurações de propriedade quando você chama vários **mover** métodos mas não conseguem localizar com êxito um registro.  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**, **MoveLast**|Definido como **True**|Definido como **True**|  
|**Mover** 0|Nenhuma alteração|Nenhuma alteração|  
|**MovePrevious**, **mover** < 0|Definido como **True**|Nenhuma alteração|  
|**MoveNext**, **mover** > 0|Nenhuma alteração|Definido como **True**|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades do indicador (VB), BOF e EOF](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [Exemplo de propriedades do indicador (VC + +), BOF e EOF](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
