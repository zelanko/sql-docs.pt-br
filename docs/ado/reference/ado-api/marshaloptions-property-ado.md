---
title: Propriedade MarshalOptions (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 01ea12405f6b00ba834b624403891d4ddf66d066
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="marshaloptions-property-ado"></a>Propriedade MarshalOptions (ADO)
Indica os registros da [registros](../../../ado/reference/ado-api/recordset-object-ado.md) devem ser empacotados de volta para o servidor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um [MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md) valor. O valor padrão é **adMarshalAll**.  
  
## <a name="remarks"></a>Comentários  
 Ao usar um cliente [registros](../../../ado/reference/ado-api/recordset-object-ado.md), os registros que foram modificados no cliente são gravados na camada intermediária ou o servidor Web por meio de uma técnica chamada empacotamento, o processo de empacotamento e envio de método de interface parâmetros em limites de thread ou processo. Definindo o **MarshalOptions** propriedade pode melhorar o desempenho quando a modificação de dados remotos são empacotados para a atualização para o servidor Web ou de camada intermediária.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** esta propriedade é usada somente em um cliente **registros**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedade MarshalOptions (VB)](../../../ado/reference/ado-api/marshaloptions-property-example-vb.md)   
 [Exemplo da propriedade MarshalOptions (VC++)](../../../ado/reference/ado-api/marshaloptions-property-example-vc.md)   

