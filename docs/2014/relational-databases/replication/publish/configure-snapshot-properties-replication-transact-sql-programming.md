---
title: Configurar propriedades de instantâneo (Programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server replication], properties
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b03dd7f886cee5816d591034d1be63ece45d8d1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63021332"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>Configurar propriedades de instantâneo (Programação Transact-SQL de replicação)
  Propriedades de instantâneo podem ser definidas e modificadas de forma programada usando-se procedimentos armazenados de replicação, nos quais os procedimentos armazenados usados dependem do tipo de publicação.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>Para configurar propriedades de instantâneo ao criar uma publicação de instantâneo ou transacional  
  
1.  No Publicador, execute [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Especifique um nome de publicação **@publication**para, um valor de **instantâneo** ou **contínuo** para **@repl_freq**, e um ou mais dos seguintes parâmetros relacionados ao instantâneo:  
  
    -   **@alt_snapshot_folder**-Especifique um caminho se o instantâneo dessa publicação for acessado desse local em vez de ou além da pasta padrão de instantâneo.  
  
    -   **@compress_snapshot**-Especifique um valor **true** se os arquivos de instantâneo na pasta de instantâneo alternativa forem compactados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] formato de arquivo CAB.  
  
    -   **@pre_snapshot_script**-Especifique o nome do arquivo e o caminho completo de um arquivo **. SQL** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.  
  
    -   **@post_snapshot_script**-Especifique o nome do arquivo e o caminho completo de um arquivo **. SQL** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.  
  
    -   **@snapshot_in_defaultfolder**-Especifique um valor de **false** se o instantâneo estiver disponível somente em um local não padrão.  
  
     Para obter mais informações sobre como criar publicações, consulte [Create a Publication](create-a-publication.md).  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>Para configurar propriedades de instantâneo ao criar uma publicação de mesclagem  
  
1.  No Publicador, execute [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especifique um nome de publicação **@publication**para, um valor de **instantâneo** ou **contínuo** para **@repl_freq**, e um ou mais dos seguintes parâmetros relacionados ao instantâneo:  
  
    -   **@alt_snapshot_folder**-Especifique um caminho se o instantâneo dessa publicação for acessado desse local em vez de ou além da pasta padrão de instantâneo.  
  
    -   **@compress_snapshot**-Especifique um valor **true** se os arquivos de instantâneo na pasta de instantâneo alternativa forem compactados no formato de arquivo CAB.  
  
    -   **@pre_snapshot_script**-Especifique o nome do arquivo e o caminho completo de um arquivo **. SQL** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.  
  
    -   **@post_snapshot_script**-Especifique o nome do arquivo e o caminho completo de um arquivo **. SQL** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.  
  
    -   **@snapshot_in_defaultfolder**-Especifique um valor de **false** se o instantâneo estiver disponível somente em um local não padrão.  
  
2.  Para obter mais informações sobre como criar publicações, consulte [Create a Publication](create-a-publication.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>Para modificar as propriedades de instantâneo de uma publicação de instantâneo ou transacional existente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Especifique um valor de **1** para **@force_invalidate_snapshot** e um dos seguintes valores para **@property**:  
  
    -   **alt_snapshot_folder** -também especifique um novo caminho para a pasta de instantâneo alternativa **@value**para.  
  
    -   **compress_snapshot** -também especifique um valor de **true** ou **false** para **@value** para indicar se os arquivos de instantâneo na pasta de instantâneo alternativa são compactados no formato de arquivo CAB.  
  
    -   **pre_snapshot_script** -também para **@value** especificar o nome do arquivo e o caminho completo de um arquivo **. SQL** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.  
  
    -   **post_snapshot_script** -também para **@value** especificar o nome do arquivo e o caminho completo de um arquivo **. SQL** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.  
  
    -   **@snapshot_in_defaultfolder** - especifique também um valor de **verdadeiro** ou **falso** para indicar se o instantâneo está disponível apenas em um local não padrão.  
  
2.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql). Especifique **@publication** e um ou mais dos parâmetros de credencial de segurança ou agendamento que estão sendo alterados.  
  
    > [!IMPORTANT]  
    >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
3.  Execute o [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) no prompt de comando ou inicie o trabalho do Agente de Instantâneo para gerar um instantâneo novo. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../create-and-apply-the-initial-snapshot.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>Para modificar as propriedades de instantâneo de uma publicação de mesclagem existente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique um valor de **1** para **@force_invalidate_snapshot** e um dos seguintes valores para **@property**:  
  
    -   **alt_snapshot_folder** -também especifique um novo caminho para a pasta de instantâneo alternativa **@value**para.  
  
    -   **compress_snapshot** -também especifique um valor de **true** ou **false** para **@value** para indicar se os arquivos de instantâneo na pasta de instantâneo alternativa são compactados no formato de arquivo CAB.  
  
    -   **pre_snapshot_script** -também para **@value** especificar o nome do arquivo e o caminho completo de um arquivo **. SQL** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.  
  
    -   **post_snapshot_script** -também para **@value** especificar o nome do arquivo e o caminho completo de um arquivo **. SQL** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.  
  
    -   **@snapshot_in_defaultfolder** - especifique também um valor de **verdadeiro** ou **falso** para indicar se o instantâneo está disponível apenas em um local não padrão.  
  
2.  Execute o [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) no prompt de comando ou inicie o trabalho do Agente de Instantâneo para gerar um instantâneo novo. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../create-and-apply-the-initial-snapshot.md).  
  
## <a name="example"></a>Exemplo  
 Esse exemplo cria uma publicação que usa uma pasta de instantâneo alternativa e um instantâneo compactado.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubaltsnapshot.sql#sp_mergealtsnapshot)]  
  
## <a name="see-also"></a>Consulte Também  
 [Locais de pastas de instantâneos alternativos](../alternate-snapshot-folder-locations.md)   
 [Instantâneos compactados](../compressed-snapshots.md)   
 [Executar scripts antes e depois da aplicação do instantâneo](../snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantâneos pelo FTP](../transfer-snapshots-through-ftp.md)   
 [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md)  
  
  
