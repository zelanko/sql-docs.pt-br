---
title: "Propriedades da publicação, instantâneo de FTP e Internet | Microsoft Docs"
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
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.internetsynchronization.f1
ms.assetid: 8e0198c3-5e4e-418c-9920-78ccbbfc1323
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fae685dfbf79d3adff163fe1432b821d5e40cdc3
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="publication-properties-ftp-snapshot-and-internet"></a>Propriedades da Publicação, Instantâneo de FTP e Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Essa página permite:  
  
-   Definir propriedades de entrega do instantâneo por FTP (File Transfer Protocol). Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md). Para usar o FTP para entrega de instantâneo, você deve configurar um servidor de FTP. Consulte a documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para obter mais informações.  
  
    > [!NOTE]  
    >  Alterações em qualquer configuração do FTP exigem que um novo instantâneo seja gerado.  
  
-   Definir propriedades de sincronização da Web para replicação de mesclagem no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, que permite que as assinaturas sejam sincronizadas pelo HTTPS (protocolo de transferência segura de hipertexto). Para usar sincronização da Web, você deve configurar um servidor IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
## <a name="options"></a>Opções  
 **Acessar arquivos de instantâneo via FTP**  
 Selecione **Permitir que os Assinantes baixem os arquivos de instantâneo usando FTP**e especifique **Nome do servidor FTP**, **Número da porta**, **Caminho da pasta raiz de FTP**, **Logon**e **Senha**, para permitir que os Assinantes usem o FTP para entrega de instantâneo.  
  
 Essa opção permite que os Assinantes usem o FTP para recuperar arquivos de instantâneo, mas não exige que isso seja feito. Se você selecionar essa opção, o Assistente para Nova Assinatura será padronizado para que o Assinante recupere arquivos de instantâneo pelo FTP. Para alterar a configuração, use a caixa de diálogo **Propriedades da Assinatura** . Se você permitir que os Assinantes acessem arquivos de instantâneo pelo FTP, especifique a pasta de FTP como o local de arquivos de instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades da Assinatura** . Essa ação fará com que o Agente de Instantâneo atualize os arquivos na pasta do FTP automaticamente quando um novo instantâneo for gerado. Se o local para a pasta do FTP não for definido, você terá de atualizar os arquivos manualmente quando novos instantâneos forem gerados. Para obter mais informações, consulte [Deliver a Snapshot Through FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md) (Entregar um instantâneo por meio de FTP).  
  
 **Sincronização da Web**  
 Somente replicação de mesclagem. Selecione **Permitir que os Assinantes sincronizem por meio da conexão com um servidor Web**e especifique um endereço de servidor Web para permitir que Assinantes de mesclagem usem a sincronização da Web. O servidor Web deve usar protocolo SSL (Secure Sockets Layer) e o endereço Web precisa ser totalmente qualificado, como `https://server.domain.com/synchronize`. Para obter mais informações, consulte [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Exibir e modificar propriedades de assinatura push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
