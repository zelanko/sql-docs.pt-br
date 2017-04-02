---
title: "Propriedades de rede  | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "propriedade LingerTimeout"
  - "propriedade EnableNagleAlgorithm"
  - "propriedade MinPendingAcceptExCount"
  - "propriedade MaxPendingSendCount"
  - "propriedade EnableBinaryXML"
  - "propriedade MinPendingReceiveCount"
  - "propriedade MaxCompletedReceiveCount"
  - "propriedade DisableNonblockingMode"
  - "propriedade RequestSizeThreshold"
  - "propriedade CompressionLevel"
  - "propriedade ReceiveBufferSize"
  - "propriedade EnableCompression"
  - "propriedade ServerSendTimeout"
  - "propriedade IPV4Support"
  - "propriedade MaxPendingReceiveCount"
  - "propriedades MaxPendingAcceptExCount"
  - "propriedade IPV6Support"
  - "propriedade MaxAllowedRequestSize"
  - "propriedade ServerReceiveTimeout"
  - "propriedade EnableLingerOnClose"
  - "propriedade InitialConnectTimeout"
  - "propriedade SendBufferSize"
  - "propriedade ScatterReceiveMultiplier"
  - "propriedades de rede [Analysis Services]"
ms.assetid: ef4251e2-abe5-4c5b-9868-7549782d0244
caps.latest.revision: 15
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 15
---
# Propriedades de rede 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor listadas nas tabelas a seguir. Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** modo de servidor multidimensional e tabular  
  
## Geral  
 **ListenOnlyOnLocalConnections**  
 Uma propriedade Booleana que identifica a escuta apenas em conexões locais, por exemplo localhost.  
  
## Ouvinte  
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
  
## Solicitações  
 **EnableBinaryXML**  
 Uma propriedade Booleana que especifica se o servidor reconhecerá solicitações xml em formato binário.  
  
 **EnableCompression**  
 Uma propriedade Booleana que especifica se a compressão está habilitada para solicitações.  
  
## Respostas  
 **CompressionLevel**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **EnableBinaryXML**  
 Uma propriedade Booleana que especifica se o servidor está habilitado para respostas xml binárias.  
  
 **EnableCompression**  
 Uma propriedade Booleana que especifica se a compressão está habilitada para respostas a solicitações de cliente.  
  
## TCP  
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
  
## Consulte também  
 [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  