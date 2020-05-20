---
title: Propriedade ConnectionTimeout (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionTimeout
helpviewer_keywords:
- ConnectionTimeout property [ADO]
ms.assetid: 8904a403-1383-4b4b-b53d-5c01d6f5deac
author: rothja
ms.author: jroth
ms.openlocfilehash: 252707003d3471d611ffafb637250009da20504f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762617"
---
# <a name="connectiontimeout-property-ado"></a>Propriedade ConnectionTimeout (ADO)
Indica por quanto tempo aguardar ao estabelecer uma conexão antes de encerrar a tentativa e gerar um erro.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que indica, em segundos, o tempo de espera até que a conexão seja aberta. O padrão é 15.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **connectionTimeout** em um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) se os atrasos do tráfego de rede ou o uso intenso do servidor fizerem com que seja necessário abandonar uma tentativa de conexão. Se o tempo da configuração da propriedade **connectionTimeout** expirar antes da abertura da conexão, ocorrerá um erro e o ADO cancelará a tentativa. Se você definir a propriedade como zero, o ADO aguardará indefinidamente até que a conexão seja aberta. Verifique se o provedor para o qual você está escrevendo código dá suporte à funcionalidade **connectionTimeout** .  
  
 A propriedade **connectionTimeout** é de leitura/gravação quando a conexão é fechada e somente leitura quando é aberta.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ConnectionString, ConnectionTimeout e State (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Exemplo das propriedades ConnectionString, ConnectionTimeout e State (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [Propriedade CommandTimeout (ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)
