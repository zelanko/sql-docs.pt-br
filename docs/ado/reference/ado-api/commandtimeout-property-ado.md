---
title: Propriedade CommandTimeout (ADO) | Microsoft Docs
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
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a7848d7fb51a01c35f8a8699b89ea132da36396b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="commandtimeout-property-ado"></a>Propriedade CommandTimeout (ADO)
Indica por quanto tempo de espera durante a execução de um comando antes de encerrar a tentativa e gerar um erro.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **longo** valor que indica, em segundos, o tempo de espera para um comando seja executado. O padrão é 30.  
  
## <a name="remarks"></a>Remarks  
 Use o **CommandTimeout** propriedade em uma [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto ou [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto para permitir que o cancelamento de uma [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método Chame, devido a atrasos de rede de tráfego ou pesada de uso do servidor. Se o intervalo definido no **CommandTimeout** propriedade decorrido antes que o comando conclui a execução, ocorrerá um erro e ADO cancela o comando. Se você definir a propriedade como zero, o ADO aguardará indefinidamente até que a execução seja concluída. Verifique se o provedor e fonte de dados ao qual você está escrevendo o suporte a código de **CommandTimeout** funcionalidade.  
  
 O **CommandTimeout** definição em um **Conexão** objeto não tem nenhum efeito **CommandTimeout** definição em um **comando** do objeto no mesmo **Conexão**; ou seja, o **comando** do objeto **CommandTimeout** propriedade não herda o valor da **Conexão** do objeto **CommandTimeout** valor.  
  
 Em um **Conexão** objeto, o **CommandTimeout** propriedade permanece somente leitura após o **Conexão** é aberto.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Propriedade ConnectionTimeout (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
