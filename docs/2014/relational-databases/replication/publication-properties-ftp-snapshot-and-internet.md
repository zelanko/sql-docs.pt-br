---
title: Propriedades da publicação, instantâneo de FTP e Internet | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.internetsynchronization.f1
ms.assetid: 8e0198c3-5e4e-418c-9920-78ccbbfc1323
caps.latest.revision: 24
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 994f77e71e3630537021a293a33e79ff3795aa7d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118088"
---
# <a name="publication-properties-ftp-snapshot-and-internet"></a>Propriedades da Publicação, Instantâneo de FTP e Internet
  Essa página permite:  
  
-   Definir propriedades de entrega do instantâneo por FTP (File Transfer Protocol). Para obter mais informações, consulte [transferir instantâneos pelo FTP](transfer-snapshots-through-ftp.md) documentação do Windows para obter mais informações.  
  
    > [!NOTE]  
    >  Alterações em qualquer configuração do FTP exigem que um novo instantâneo seja gerado.  
  
-   Definir propriedades de sincronização da Web para replicação de mesclagem no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, que permite que as assinaturas sejam sincronizadas pelo HTTPS (protocolo de transferência segura de hipertexto). Para usar sincronização da Web, você deve configurar um servidor IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md).  
  
## <a name="options"></a>Opções  
 **Acessar arquivos de instantâneo via FTP**  
 Selecione **Permitir que os Assinantes baixem os arquivos de instantâneo usando FTP**e especifique **Nome do servidor FTP**, **Número da porta**, **Caminho da pasta raiz de FTP**, **Logon**e **Senha**, para permitir que os Assinantes usem o FTP para entrega de instantâneo.  
  
 Essa opção permite que os Assinantes usem o FTP para recuperar arquivos de instantâneo, mas não exige que isso seja feito. Se você selecionar essa opção, o Assistente para Nova Assinatura será padronizado para que o Assinante recupere arquivos de instantâneo pelo FTP. Para alterar a configuração, use a caixa de diálogo **Propriedades da Assinatura** . Se você permitir que os Assinantes acessem arquivos de instantâneo pelo FTP, especifique a pasta de FTP como o local de arquivos de instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades da Assinatura** . Essa ação fará com que o Agente de Instantâneo atualize os arquivos na pasta do FTP automaticamente quando um novo instantâneo for gerado. Se o local para a pasta do FTP não for definido, você terá de atualizar os arquivos manualmente quando novos instantâneos forem gerados. Para obter mais informações, consulte [Deliver a Snapshot Through FTP](publish/deliver-a-snapshot-through-ftp.md) (Entregar um instantâneo por meio de FTP).  
  
 **Sincronização da Web**  
 Somente replicação de mesclagem. Selecione **Permitir que os Assinantes sincronizem por meio da conexão com um servidor Web**e especifique um endereço de servidor Web para permitir que Assinantes de mesclagem usem a sincronização da Web. O servidor Web deve usar protocolo SSL (Secure Sockets Layer) e o endereço Web precisa ser totalmente qualificado, como https://server.domain.com/synchronize. Para obter mais informações, consulte [Configurar sincronização da Web](configure-web-synchronization.md).  
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](publish/view-and-modify-publication-properties.md)   
 [Exibir e modificar propriedades de assinatura pull](view-and-modify-pull-subscription-properties.md)   
 [Exibir e modificar propriedades de assinatura push](view-and-modify-push-subscription-properties.md)   
 [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md)   
 [Publicar dados e objetos de banco de dados](publish/publish-data-and-database-objects.md)  
  
  