---
title: "Protocolos de cliente – propriedades de TCP IP (guia protocolo) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TCP/IP [SQL Server], client protocols
- client protocols [SQL Server]
ms.assetid: d04f1bce-069c-4a02-b561-c87c3282be36
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a8d82ee917afc74c5fba0a0bbcc01451b99cb645
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="client-protocols---tcp-ip-properties-protocol-tab"></a>Protocolos de Cliente – Propriedades de TCP IP (guia Protocolo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, use o **protocolo** guia o **propriedades de TCP/IP** caixa de diálogo para exibir ou especificar as opções a seguir. Para se conectar a uma porta diferente, digite o número da porta na caixa **Pipe Padrão** . Para obter mais informações sobre cadeias de conexão, consulte [Criando uma cadeia de conexão válida usando TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md).  
  
## <a name="options"></a>Opções  
 **Pipe Padrão**  
 Especifica a porta que a biblioteca de rede TCP/IP usará para tentar se conectar à instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O valor padrão da porta é 1433.  
  
 Ao conectar a uma instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)], o cliente usa esse valor. Se uma instância padrão tiver sido configurada para escutar em uma porta diferente, altere esse valor para esse número de porta.  
  
 Ao se conectar a uma instância nomeada do [!INCLUDE[ssDE](../../includes/ssde-md.md)], o cliente tentará obter o número da porta no Serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no computador servidor. Se o Serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver sendo executado, o número da porta deverá ser fornecido por meio dessa configuração, ou como parte da cadeia de conexão.  
  
 **Enabled**  
 Os valores possíveis são **Sim** e **Não**.  
  
 **Keep Alive**  
 Este parâmetro (em milissegundos) controla a frequência das tentativas do TCP de verificar se uma conexão ociosa ainda está intacta enviando um pacote **KEEPALIVE** . O padrão é 30.000 milissegundos.  
  
 **Intervalo de Atividade**  
 Este parâmetro (em milissegundos) determina o intervalo que separa novas transmissões de **KEEPALIVE** até que uma resposta seja recebida. O padrão é 1.000 milissegundos.  
  
## <a name="see-also"></a>Consulte Também  
 [Escolhendo um protocolo de rede](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Novo Alias &#40; Guia de alias &#41;](../../tools/configuration-manager/new-alias-alias-tab.md)   
 [Propriedades &#60;Alias&#62; &#40;Guia Alias&#41;](../../tools/configuration-manager/alias-properties-alias-tab.md)  
  
  
