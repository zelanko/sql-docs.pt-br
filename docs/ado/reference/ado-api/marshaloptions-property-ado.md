---
description: Propriedade MarshalOptions (ADO)
title: Propriedade marshaloptions (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
author: rothja
ms.author: jroth
ms.openlocfilehash: a3eb985c5940659f6d70c331dd860f0588398fb8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774495"
---
# <a name="marshaloptions-property-ado"></a>Propriedade MarshalOptions (ADO)
Indica quais registros do [conjunto de registros](./recordset-object-ado.md) devem ser empacotados de volta para o servidor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de [MarshalOptionsEnum](./marshaloptionsenum.md) . O valor padrão é **adMarshalAll**.  
  
## <a name="remarks"></a>Comentários  
 Ao usar um [conjunto de registros](./recordset-object-ado.md)do lado do cliente, os registros que foram modificados no cliente são gravados novamente na camada intermediária ou no servidor Web por meio de uma técnica chamada marshaling, do processo de empacotamento e envio de parâmetros de método de interface entre limites de thread ou processo. A definição da propriedade **marshaloptions** pode melhorar o desempenho quando dados remotos modificados são empacotados para atualização de volta para a camada intermediária ou servidor Web.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Essa propriedade é usada somente em um **conjunto de registros**do lado do cliente.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade marshaloptions (VB)](./marshaloptions-property-example-vb.md)   
 [Exemplo da propriedade MarshalOptions (VC++)](./marshaloptions-property-example-vc.md)