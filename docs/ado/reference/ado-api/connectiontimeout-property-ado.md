---
title: Propriedade ConnectionTimeout (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Connection15::ConnectionTimeout
helpviewer_keywords: ConnectionTimeout property [ADO]
ms.assetid: 8904a403-1383-4b4b-b53d-5c01d6f5deac
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 17572bfd4ef1de5fa20246f88c8a0187409bbfd4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="connectiontimeout-property-ado"></a>Propriedade ConnectionTimeout (ADO)
Indica por quanto tempo a aguardar ao estabelecer uma conexão antes de encerrar a tentativa e gerar um erro.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **longo** valor que indica, em segundos, o tempo de espera para a conexão abrir. O padrão é 15.  
  
## <a name="remarks"></a>Comentários  
 Use o **ConnectionTimeout** propriedade em uma [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) se os atrasos de rede de tráfego ou pesada de uso do servidor faça necessárias abandono de uma tentativa de conexão do objeto. Se o tempo desde o **ConnectionTimeout** configuração da propriedade decorrido antes da abertura da conexão, ocorrerá um erro e ADO cancela a tentativa. Se você definir a propriedade como zero, o ADO aguardará indefinidamente até que a conexão é aberta. Verifique se o provedor ao qual você está escrevendo código oferece suporte a **ConnectionTimeout** funcionalidade.  
  
 O **ConnectionTimeout** propriedade é leitura/gravação quando a conexão é fechada e somente leitura quando ela é aberta.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de estado (VB), ConnectionTimeout e ConnectionString](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Exemplo de propriedades de estado (VC + +), ConnectionTimeout e ConnectionString](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [Propriedade CommandTimeout (ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)
