---
title: "Propriedades da Publica&#231;&#227;o, Instant&#226;neo de FTP e Internet | Microsoft Docs"
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
  - "sql13.rep.newpubwizard.pubproperties.internetsynchronization.f1"
ms.assetid: 8e0198c3-5e4e-418c-9920-78ccbbfc1323
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Propriedades da Publica&#231;&#227;o, Instant&#226;neo de FTP e Internet
  Essa página permite:  
  
-   Definir propriedades de entrega do instantâneo por FTP (File Transfer Protocol). Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md). Para usar o FTP para entrega de instantâneo, você deve configurar um servidor de FTP. Consulte a documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para obter mais informações.  
  
    > [!NOTE]  
    >  Alterações em qualquer configuração do FTP exigem que um novo instantâneo seja gerado.  
  
-   Definir propriedades de sincronização da Web para replicação de mesclagem no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, que permite que as assinaturas sejam sincronizadas pelo HTTPS (protocolo de transferência segura de hipertexto). Para usar sincronização da Web, você deve configurar um servidor IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Para obter mais informações, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
## Opções  
 **Acessar arquivos de instantâneo via FTP**  
 Selecione **Permitir que os assinantes para baixar arquivos de instantâneo usando FTP (File Transfer Protocol)**, e especifique **nome do servidor FTP**, **número da porta**, **o caminho da pasta raiz do FTP**, **Login**, e **senha**, os assinantes podem usar o FTP para entrega de instantâneo.  
  
 Essa opção permite que os Assinantes usem o FTP para recuperar arquivos de instantâneo, mas não exige que isso seja feito. Se você selecionar essa opção, o Assistente para Nova Assinatura será padronizado para que o Assinante recupere arquivos de instantâneo pelo FTP. Para alterar a configuração, use a caixa de diálogo **Propriedades da Assinatura** . Se você permitir que os Assinantes acessem arquivos de instantâneo pelo FTP, especifique a pasta de FTP como o local de arquivos de instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades da Assinatura** . Essa ação fará com que o Agente de Instantâneo atualize os arquivos na pasta do FTP automaticamente quando um novo instantâneo for gerado. Se o local para a pasta do FTP não for definido, você terá de atualizar os arquivos manualmente quando novos instantâneos forem gerados. Para obter mais informações, consulte [entregar um instantâneo por meio de FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
 **Sincronização da Web**  
 Somente replicação de mesclagem. Selecione **Permitir que os Assinantes sincronizem por meio da conexão com um servidor Web**e especifique um endereço de servidor Web para permitir que Assinantes de mesclagem usem a sincronização da Web. O servidor Web deve usar SSL (Secure Sockets Layer) e o endereço da Web precisa ser totalmente qualificado, como um https://server.domain.com/synchronize. Para obter mais informações, consulte [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
## Consulte também  
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizar e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  