---
title: Propriedades de rede | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 70e1ea429d7c60f3d9ba7806d6e6a6a25998b4f5
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="network-properties"></a>Propriedades de rede
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor listadas nas tabelas a seguir. Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** modo de servidor multidimensional e tabular  
  
## <a name="general"></a>Geral  
 **ListenOnlyOnLocalConnections**  
 Uma propriedade Booleana que identifica a escuta apenas em conexões locais, por exemplo localhost.  
  
## <a name="listener"></a>Ouvinte  
 **IPV4Support**  
 Uma propriedade de inteiro de 32 bits assinada que define o suporte ao protocolo IPv4. Essa propriedade tem um dos valores listados na tabela a seguir:  
  
|Value|Descrição|  
|-----------|-----------------|  
|*0*|IPv4 desabilitado; os clientes não podem se conectar.|  
|*1*|(Padrão) IPv4 necessário; servidor não será iniciado se não puder escutar IPv4.|  
|*2*|IPv4 é opcional; o servidor tenta escutar IPv4, mas será iniciado mesmo se não conseguir.|  
  
 **IPV6Support**  
 Uma propriedade de inteiro de 32 bits assinada que define o suporte ao protocolo IPv6. Essa propriedade tem um dos valores listados na tabela a seguir:  
  
|Value|Descrição|  
|-----------|-----------------|  
|*0*|IPv6 desabilitado; os clientes não podem se conectar.|  
|*1*|(Padrão) IPv6 necessário; servidor não será iniciado se não for possível escutar IPv6|  
|*2*|IPv6 é opcional; o servidor tenta escutar IPv6, mas será iniciado mesmo se não conseguir.|  
  
 **MaxAllowedRequestSize**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **RequestSizeThreshold**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ServerReceiveTimeout**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ServerSendTimeout**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="requests"></a>Solicitações  
 **EnableBinaryXML**  
 Uma propriedade Booleana que especifica se o servidor reconhecerá solicitações xml em formato binário.  
  
 **EnableCompression**  
 Uma propriedade Booleana que especifica se a compressão está habilitada para solicitações.  
  
## <a name="responses"></a>Respostas  
 **CompressionLevel**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **EnableBinaryXML**  
 Uma propriedade Booleana que especifica se o servidor está habilitado para respostas xml binárias.  
  
 **EnableCompression**  
 Uma propriedade Booleana que especifica se a compressão está habilitada para respostas a solicitações de cliente.  
  
## <a name="tcp"></a>TCP  
 **InitialConnectTimeout**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxCompletedReceiveCount**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingAcceptExCount**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingReceiveCount**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingSendCount**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MinPendingAcceptExCount**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MinPendingReceiveCount**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ScatterReceiveMultiplier**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ DisableNonblockingMode**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ EnableLingerOnClose**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\EnableNagleAlgorithm**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ LingerTimeout**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ ReceiveBufferSize**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ SendBufferSize**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do servidor no Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
