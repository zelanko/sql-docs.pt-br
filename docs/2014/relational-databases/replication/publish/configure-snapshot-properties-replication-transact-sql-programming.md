---
title: Configurar propriedades de instantâneo (Programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server replication], properties
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 161ff6dadbd3917e75609e60f9e1a602b6437028
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292246"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>Configurar propriedades de instantâneo (Programação Transact-SQL de replicação)
  Propriedades de instantâneo podem ser definidas e modificadas de forma programada usando-se procedimentos armazenados de replicação, nos quais os procedimentos armazenados usados dependem do tipo de publicação.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>Para configurar propriedades de instantâneo ao criar uma publicação de instantâneo ou transacional  
  
1.  No Publicador, execute [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Especifique um nome de publicação para **@publication**, um valor de **snapshot** ou **continuous** para **@repl_freq**, e um ou mais dos seguintes parâmetros relacionados a instantâneo.  
  
    -   **@alt_snapshot_folder** - especifique um caminho se o instantâneo para essa publicação for acessado daquele local em vez de ou além da pasta padrão de instantâneo.  
  
    -   **@compress_snapshot** - especifique um valor de **verdadeiro** se os arquivos de instantâneo na pasta de instantâneo alternativa forem compactados no formato de arquivo CAB [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .  
  
    -   **@pre_snapshot_script** - especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.  
  
    -   **@post_snapshot_script** - especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.  
  
    -   **@snapshot_in_defaultfolder** - especifique um valor de **falso** se o instantâneo só estiver disponível em um local não padrão.  
  
     Para obter mais informações sobre como criar publicações, consulte [Create a Publication](create-a-publication.md).  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>Para configurar propriedades de instantâneo ao criar uma publicação de mesclagem  
  
1.  No Publicador, execute [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especifique um nome de publicação para **@publication**, um valor de **snapshot** ou **continuous** para **@repl_freq**, e um ou mais dos seguintes parâmetros relacionados a instantâneo.  
  
    -   **@alt_snapshot_folder** - especifique um caminho se o instantâneo para essa publicação for acessado daquele local em vez de ou além da pasta padrão de instantâneo.  
  
    -   **@compress_snapshot** - especifique um valor de **verdadeiro** se os arquivos de instantâneo na pasta de instantâneo alternativa forem compactados em formato de arquivo CAB.  
  
    -   **@pre_snapshot_script** - especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.  
  
    -   **@post_snapshot_script** - especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.  
  
    -   **@snapshot_in_defaultfolder** - especifique um valor de **falso** se o instantâneo só estiver disponível em um local não padrão.  
  
2.  Para obter mais informações sobre como criar publicações, consulte [Create a Publication](create-a-publication.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>Para modificar as propriedades de instantâneo de uma publicação de instantâneo ou transacional existente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Especifique um valor **1** para **@force_invalidate_snapshot** e um dos valores a seguir para **@property**:  
  
    -   **alt_snapshot_folder** - também especifique um caminho novo para a pasta de instantâneo alternativa para **@value**.  
  
    -   **compress_snapshot** - especifique também um valor de **verdadeiro** ou **falso** para **@value** para indicar se arquivos de instantâneo na pasta de instantâneo alternativa são compactados no formato de arquivo CAB.  
  
    -   **pre_snapshot_script** - também para **@value** especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.  
  
    -   **post_snapshot_script** - também para **@value** especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.  
  
    -   **@snapshot_in_defaultfolder** - especifique também um valor de **verdadeiro** ou **falso** para indicar se o instantâneo está disponível apenas em um local não padrão.  
  
2.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql). Especifique **@publication** e um ou mais dos parâmetros de credencial de segurança ou programação que estão sendo alterados.  
  
    > [!IMPORTANT]  
    >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
3.  Execute o [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) no prompt de comando ou inicie o trabalho do Agente de Instantâneo para gerar um instantâneo novo. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>Para modificar as propriedades de instantâneo de uma publicação de mesclagem existente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique um valor **1** para **@force_invalidate_snapshot** e um dos valores a seguir para **@property**:  
  
    -   **alt_snapshot_folder** - também especifique um caminho novo para a pasta de instantâneo alternativa para **@value**.  
  
    -   **compress_snapshot** - especifique também um valor de **verdadeiro** ou **falso** para **@value** para indicar se arquivos de instantâneo na pasta de instantâneo alternativa são compactados no formato de arquivo CAB.  
  
    -   **pre_snapshot_script** - também para **@value** especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.  
  
    -   **post_snapshot_script** - também para **@value** especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.  
  
    -   **@snapshot_in_defaultfolder** - especifique também um valor de **verdadeiro** ou **falso** para indicar se o instantâneo está disponível apenas em um local não padrão.  
  
2.  Execute o [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) no prompt de comando ou inicie o trabalho do Agente de Instantâneo para gerar um instantâneo novo. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md).  
  
## <a name="example"></a>Exemplo  
 Esse exemplo cria uma publicação que usa uma pasta de instantâneo alternativa e um instantâneo compactado.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubaltsnapshot.sql#sp_mergealtsnapshot)]  
  
## <a name="see-also"></a>Consulte também  
 [Locais da pasta de instantâneos alternativos](../alternate-snapshot-folder-locations.md)   
 [Instantâneos compactados](../compressed-snapshots.md)   
 [Executar scripts antes e depois da aplicação do instantâneo](../execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantâneos pelo FTP](../transfer-snapshots-through-ftp.md)   
 [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md)  
  
  
