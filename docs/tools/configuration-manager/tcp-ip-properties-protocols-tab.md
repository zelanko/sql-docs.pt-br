---
title: Propriedades de TCP/IP (guia Protocolos) | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- TCP/IP [SQL Server], configuration options
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 34f6d026e29da596afaa6c812a726a64fb7e828f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38002678"
---
# <a name="tcpip-properties-protocols-tab"></a>Propriedades do TCP/IP (guia Protocolos)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Use a caixa de diálogo **Propriedades do TCP/IP** para configurar as opções do protocolo TCP/IP. Clique em **TCP/IP** no painel esquerdo, para mostrar configurações individuais de endereço IP no painel de detalhes.  
  
 O Microsoft SQL Server deve ser reiniciado para que as alterações tenham efeito.  
  
## <a name="options"></a>Opções  
 **Enabled**  
 Os valores possíveis são **Sim** e **Não**.  
  
 **Keep Alive**  
 Especifique o intervalo (em milissegundos) no qual os pacotes keep-alive são transmitidos para verificar se o computador remoto de uma conexão ainda está disponível.  
  
 **Listen All**  
 Especifique se o SQL Server escutará em todos os endereços IP associados às placas de rede no computador. Se for definido como **No**, configure cada endereço IP separadamente usando a caixa de diálogo de propriedades de cada endereço IP. Se for definido como **Yes**, as configurações da caixa de propriedades **IPAll** se aplicarão a todos os endereços IP. O valor padrão é **Yes**.  
  
 **No Delay**  
 O SQL Server não implementa alterações a esta propriedade.  
  
## <a name="see-also"></a>Consulte Também  
 [Escolhendo um protocolo de rede](https://msdn.microsoft.com/library/ms187892(v=sql.130).aspx)   
 [Criando uma cadeia de conexão válida usando TCP/IP](creating-a-valid-connection-string-using-tcp-ip.md)  
  
  
