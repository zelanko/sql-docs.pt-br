---
title: "Sincronização da Web para Replicação de Mesclagem | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication synchronization [SQL Server replication]
- Internet [SQL Server replication], synchronization
- synchronization [SQL Server replication], Web Synchronization
- Web publishing [SQL Server replication], synchronization
- Web synchronization, about
- Web synchronization
ms.assetid: 84785aba-b2c1-4821-9e9d-a363c73dcb37
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d5884fb9db00d9b995866ce275f44df8b6395c00
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="web-synchronization-for-merge-replication"></a>Sincronização da Web para replicação de mesclagem.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A sincronização da Web para replicação de mesclagem lhe permite replicar dados usando o protocolo HTTPS, e isso é útil nos seguintes cenários:  
  
-   Sincronizando dados de usuários móveis pela Internet.  
  
-   Sincronizando dados entre bancos de dados [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por um firewall de empresa.  
  
 Por exemplo, um representante de vendas ambulante pode usar a sincronização da Web. A empresa, [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)], tem representantes de vendas que viajam a várias lojas e fornecedores ao longo das suas regiões. Em viagens longas os representantes ficam em hotéis e precisam de uma forma conveniente para carregar os dados de vendas e baixar as atualizações de produtos no final de cada dia.  
  
 O departamento de TI de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] configurou cada notebook com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e habilitou a replicação de mesclagem para usar a sincronização da Web. O Merge Agent em cada notebook possui uma URL de Internet que aponta para os componentes de replicação que são instalados em um computador que está executando [!INCLUDE[msCoName](../../includes/msconame-md.md)] Serviços de Informações da Internet (IIS). Esses componentes sincronizam o Assinante com o Publicador. Agora, cada representante pode se conectar através de qualquer conexão de Internet disponível sem usar uma conexão discada remota, e pode carregar e baixar os dados apropriados. A conexão de Internet usa o Protocolo SSL (Secure Sockets Layer); portanto, uma rede privada virtual (VPN) não é requerida.  
  
 Para obter informações sobre como configurar os componentes que são necessários para a sincronização da Web, consulte [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md), [configurar IIS para sincronização da Web](../../relational-databases/replication/configure-iis-for-web-synchronization.md) e [configurar IIS 7 para sincronização da Web](../../relational-databases/replication/configure-iis-7-for-web-synchronization.md).  
  
> [!NOTE]  
>  A sincronização da Web é projetada para sincronizar dados com computadores portáteis, dispositivos de mão e outros clientes. A sincronização da Web não é destinada para aplicativos de alto volume de servidor a servidor.  
  
## <a name="overview-of-how-web-synchronization-works"></a>Visão geral de como a sincronização da Web funciona  
 Quando a sincronização da Web é usada, as atualizações no Assinante são empacotadas e enviadas como uma mensagem XML ao computador que está executando IIS usando o protocolo HTTPS. O computador que está executando IIS então envia um comando ao Publicador em formato binário, normalmente usando TCP/IP. Atualizações no Publicador são enviadas ao computador que está executando IIS e, então, são empacotadas como uma mensagem XML para entrega ao Assinante.  
  
 A ilustração seguinte mostra alguns dos componentes que são envolvidos em sincronização da Web para replicação de mesclagem.  
  
 ![Fluxo de dados e componentes de sincronização da Web](../../relational-databases/replication/media/web-sync01.gif "Fluxo de dados e componentes de sincronização da Web")  
  
 A sincronização da Web é uma opção apenas para assinatura pull; então, um Merge Agent sempre será executado no Assinante. Esse Merge Agent pode ser o Merge Agent padrão, o MErge Agent do controle de Active X ou um aplicativo que fornece sincronização através do RMO (Replication Management Objects). Para especificar o local do computador que está executando IIS, use o parâmetro **–InternetUrl** para o Merge Agent.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener (Replisapi.dll) está configurado no computador que está executando IIS e é responsável pelo manuseio das mensagens enviadas para o servidor do Publicador e dos Assinantes. Cada nó na topologia controla o fluxo de dados XML usando o Reconciliador de Replicação de Mesclagem (Replrec.dll).  
  
 O[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou uma versão posterior é requerida para todos os computadores que participam de sincronização da Web.  
  
### <a name="synchronization-process"></a>Processo de sincronização  
 As etapas seguintes acontecem durante a sincronização:  
  
1.  O Merge Agent é iniciado no Assinante. O agente faz o seguinte:  
  
    1.  Faz uma conexão SQL ao banco de dados de assinatura.  
  
    2.  Extrai quaisquer alterações do banco de dados.  
  
    3.  Faz uma solicitação HTTPS ao computador que está executando IIS.  
  
    4.  Carrega as alterações de dados como uma mensagem de XML.  
  
2.  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener e Reconciliador de Replicação de Mesclagem que estão hospedados no computador que está executando IIS, fazem o seguinte.  
  
    1.  Respondem à solicitação de HTTPS.  
  
    2.  Fazem uma conexão SQL ao banco de dados de publicação.  
  
    3.  Aplicam as alterações carregadas ao banco de dados de publicação.  
  
    4.  Extraem as alterações de download para o Assinante.  
  
    5.  Enviam de volta uma resposta de HTTPS ao Merge Agent.  
  
3.  O Merge Agent no Assinante oferece suporte à resposta HTTPS e aplica as alterações de download ao banco de dados da assinatura.  
  
## <a name="see-also"></a>Consulte Também  
 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)   
 [Topologies for Web Synchronization](../../relational-databases/replication/topologies-for-web-synchronization.md)  
  
  
