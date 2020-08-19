---
description: Propriedade Direction
title: Propriedade Direction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Direction
helpviewer_keywords:
- Direction property
ms.assetid: d5732578-3434-4dcd-a9f7-db1abd1b3b94
author: rothja
ms.author: jroth
ms.openlocfilehash: 37987e58829b1b6957b4fe1de440aaeb4aae1763
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444048"
---
# <a name="direction-property"></a>Propriedade Direction
Indica se o [parâmetro](../../../ado/reference/ado-api/parameter-object.md) representa um parâmetro de entrada, um parâmetro de saída, uma entrada e um parâmetro de saída, ou se o parâmetro é o valor de retorno de um procedimento armazenado.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Direction** para especificar como um parâmetro é passado para ou de um procedimento. A propriedade **Direction** é de leitura/gravação; Isso permite que você trabalhe com provedores que não retornam essas informações ou para definir essas informações quando você não quer que o ADO faça uma chamada extra ao provedor para recuperar informações de parâmetro.  
  
 Nem todos os provedores podem determinar a direção dos parâmetros em seus procedimentos armazenados. Nesses casos, você deve definir a propriedade **Direction** antes de executar a consulta.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
