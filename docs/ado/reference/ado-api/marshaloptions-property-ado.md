---
title: Propriedade MarshalOptions (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca3cb11f425b94145b89638012844d64265bd6b3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="marshaloptions-property-ado"></a>Propriedade MarshalOptions (ADO)
Indica os registros da [registros](../../../ado/reference/ado-api/recordset-object-ado.md) devem ser empacotados de volta para o servidor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um [MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md) valor. O valor padrão é **adMarshalAll**.  
  
## <a name="remarks"></a>Remarks  
 Ao usar um cliente [registros](../../../ado/reference/ado-api/recordset-object-ado.md), os registros que foram modificados no cliente são gravados na camada intermediária ou o servidor Web por meio de uma técnica chamada empacotamento, o processo de empacotamento e envio de método de interface parâmetros em limites de thread ou processo. Definindo o **MarshalOptions** propriedade pode melhorar o desempenho quando a modificação de dados remotos são empacotados para a atualização para o servidor Web ou de camada intermediária.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** esta propriedade é usada somente em um cliente **registros**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedade MarshalOptions (VB)](../../../ado/reference/ado-api/marshaloptions-property-example-vb.md)   
 [Exemplo da propriedade MarshalOptions (VC++)](../../../ado/reference/ado-api/marshaloptions-property-example-vc.md)   
