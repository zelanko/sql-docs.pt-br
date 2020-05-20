---
title: Propriedade CommandTimeout (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
author: rothja
ms.author: jroth
ms.openlocfilehash: b771c5b8dc54bb312893885aea9c9c151feef3e3
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760382"
---
# <a name="commandtimeout-property-ado"></a>Propriedade CommandTimeout (ADO)
Indica por quanto tempo aguardar ao executar um comando antes de encerrar a tentativa e gerar um erro.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que indica, em segundos, por quanto tempo aguardar a execução de um comando. O padrão é 30.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **CommandTimeout** em um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) para permitir o cancelamento de uma chamada de método [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) , devido a atrasos do tráfego de rede ou uso intenso do servidor. Se o intervalo definido na propriedade **CommandTimeout** expirar antes que o comando conclua a execução, ocorre um erro e o ADO cancela o comando. Se você definir a propriedade como zero, o ADO aguardará indefinidamente até que a execução seja concluída. Verifique se o provedor e a fonte de dados para os quais você está escrevendo código dão suporte à funcionalidade **CommandTimeout** .  
  
 A configuração **CommandTimeout** em um objeto de **conexão** não tem efeito sobre a configuração **CommandTimeout** em um objeto de **comando** na mesma **conexão**; ou seja, a propriedade **CommandTimeout** do objeto de **comando** não herda o valor do valor **CommandTimeout** do objeto de **conexão** .  
  
 Em um objeto de **conexão** , a propriedade **CommandTimeout** permanece de leitura/gravação depois que a **conexão** é aberta.  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Propriedade ConnectionTimeout (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
