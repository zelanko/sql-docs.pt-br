---
title: "Pasta do Instant&#226;neo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.replicationutilities.specifysnapshotfolder.f1"
ms.assetid: 3eb1b73f-ddb3-4d09-be6e-811c414698e9
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Pasta do Instant&#226;neo
  A página **Pasta do Instantâneo** aparece no Assistente para Configurar a Distribuição e no Assistente para Nova Publicação. O local especificado para a pasta de instantâneo será usada como padrão para todos os publicadores habilitados nesse assistente (a pasta de instantâneo padrão não se aplica a Publicadores posteriormente habilitados usando o **Propriedades do distribuidor** caixa de diálogo). Você pode substituir esse padrão por qualquer Publicador na página **Publicadores** do Assistente para Configurar a Distribuição da caixa de diálogo **Propriedades do Distribuidor** .  
  
 A pasta de instantâneo é simplesmente um diretório que você designou como um compartilhamento, agentes que leem essa pasta e gravam nela devem ter permissões suficientes para acessá-la. Para obter mais informações sobre como proteger a pasta adequadamente, consulte [proteger a pasta de instantâneo](../../relational-databases/replication/security/secure-the-snapshot-folder.md). Antes de implementar replicação, teste se os agentes de replicação poderão se conectar à pasta de instantâneo. Faça logon na conta que será usada por cada agente e depois tente acessar a pasta de instantâneo.  
  
## Opções  
 **Pasta do instantâneo**  
 Insira o caminho para a pasta onde você quer arquivos de instantâneo sejam armazenados.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você use um compartilhamento de rede como um local de pasta de instantâneo. Caminhos locais (os que iniciam com uma letra de unidade, como c:\\) não estão acessíveis para os agentes em outros computadores.  
  
## Consulte também  
 [Locais da pasta de instantâneos alternativos](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  