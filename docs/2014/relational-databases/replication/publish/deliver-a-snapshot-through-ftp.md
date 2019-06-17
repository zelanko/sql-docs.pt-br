---
title: Entregar um instantâneo pelo FTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d1a8989492c9efb670b00bda00dbfa757c549fca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62960060"
---
# <a name="deliver-a-snapshot-through-ftp"></a>Entregar um instantâneo pelo FTP
  Este tópico descreve como entregar um instantâneo pelo FTP no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
##  <a name="Restrictions"></a> Limitações e restrições  
  
-   O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se forem usadas assinaturas pull, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\ftpserver\home\snapshots. Para obter mais informações, consulte [Proteger a pasta de instantâneos](../security/secure-the-snapshot-folder.md).  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Para transferir arquivos de instantâneo que usam Protocolo de Transferência de Arquivo (FTP), deve-se, em primeiro lugar, configurar um servidor de FTP. Para obter mais informações, consulte a documentação [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Serviços de Informações da Internet (IIS).  
  
###  <a name="Security"></a> Segurança  
 Para ajudar a melhorar a segurança, recomendamos implementar uma rede privada virtual (VPN) ao usar a entrega de instantâneo FTP pela Internet. Para obter mais informações, consulte [Publicar dados pela Internet usando VPN](../publish-data-over-the-internet-using-vpn.md).  
  
 Como uma prática recomendada de segurança, não permita logons anônimos ao servidor FTP. O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se forem usadas assinaturas pull, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\ftpserver\home\snapshots. Para obter mais informações, consulte [Proteger a pasta de instantâneos](../security/secure-the-snapshot-folder.md).  
  
 Quando possível, solicite que os usuários insiram suas credenciais em tempo de execução. Se você armazenar credenciais em um arquivo de script, será necessário proteger o arquivo.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Depois que o servidor FTP for configurado, especifique informações de diretório e de segurança para esse servidor na caixa de diálogo **Propriedades da Publicação – \<Publicação>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-ftp-information"></a>Para especificar informações de FTP  
  
1.  Na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione **Permitir que os Assinantes baixem os arquivos de instantâneo usando FTP** de uma das seguintes páginas:   
    -   A página **Instantâneo de FTP** para publicações de instantâneo e transacionais e publicações de mesclagem para Publicadores executando versões anteriores ao [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].    
    -   A página **Instantâneo de FTP e Internet** , para publicações de mesclagem de Publicadores executando [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou versões posteriores.    
2.  Especifique valores para **Nome do servidor FTP**, **Número da porta**, **Caminho da pasta raiz de FTP**, **Logon**e **Senha**.    
     Por exemplo, se a raiz do servidor FTP for \\\ftpserver\home e você quiser que os instantâneos sejam armazenados em \\\ftpserver\home\snapshots, especifique \snapshots\ftp para a propriedade **Caminho da pasta raiz de FTP** (a replicação acrescentará 'ftp' ao caminho da pasta de instantâneo ao criar os arquivos de instantâneo).    
3.  Especifique que o Agente de Instantâneo deve gravar os arquivos de instantâneo no diretório especificado na etapa 2. Por exemplo, para que o Snapshot Agent grave os arquivos de instantâneo em \\\ftpserver\home\snapshots, é necessário especificar o caminho \\\ftpserver\home\snapshots em um ou dois locais:    
    -   O local de instantâneo padrão para o Distribuidor associado a essa publicação.    
         Para obter mais informações sobre como especificar o local do instantâneo padrão, consulte [especificar o local de instantâneo padrão](../snapshot-options.md#snapshot-folder-locations).    
    -   Um local alternativo de pasta de instantâneo para essa publicação. Um local alternativo será requerido se o instantâneo for compactado.    
         Insira o caminho na caixa de texto **Colocar os arquivos nesta pasta** na página Instantâneo da caixa de diálogo **Propriedades da Publicação – \<Publicação>** .   
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 A opção para tornar os arquivos de instantâneo disponíveis em um servidor FTP podem ser definidas, e essas configurações FTP podem ser modificadas programaticamente usando procedimentos de armazenamento. O procedimento usado depende do tipo de publicação. A entrega de instantâneo FTP é usada apenas com assinaturas pull.  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-snapshot-or-transactional-publication"></a>Par habilitar a entrega de instantâneo FTP para um instantâneo ou publicação transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Especificar **@publication** , um valor de `true` para **@enabled_for_internet** e valores adequados para os seguintes parâmetros:    
    -   **@ftp_address** - o endereço do servidor FTP usado para entregar o instantâneo.    
    -   (Opcional) **@ftp_port** - a porta usada pelo servidor FTP.    
    -   (Opcional) **@ftp_subdirectory** - o subdiretório do diretório FTP padrão atribuído a um logon de FTP. Por exemplo, se a raiz do servidor FTP for \\\ftpserver\home e você desejar que os instantâneos sejam armazenados em \\\ftpserver\home\snapshots, especifique **\snapshots\ftp** para **@ftp_subdirectory** (a replicação acrescentará 'ftp' ao caminho da pasta de instantâneo ao criar os arquivos de instantâneo).    
    -   (Opcional) **@ftp_login** - uma conta de logon usada para conectar-se ao servidor FTP.    
    -   (Opcional) **@ftp_password** - a senha para o logon no FTP.  
  
     Isso cria uma publicação que usa FTP. Para obter mais informações, consulte [Criar uma assinatura](create-a-publication.md).  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-merge-publication"></a>Para habilitar a entrega de instantâneo FTP para uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especificar **@publication** , um valor de `true` para **@enabled_for_internet** e valores adequados para os seguintes parâmetros:  
  
    -   **@ftp_address** - o endereço do servidor FTP usado para entregar o instantâneo.    
    -   (Opcional) **@ftp_port** - a porta usada pelo servidor FTP.    
    -   (Opcional) **@ftp_subdirectory** - o subdiretório do diretório FTP padrão atribuído a um logon de FTP. Por exemplo, se a raiz do servidor FTP for \\\ftpserver\home e você desejar que os instantâneos sejam armazenados em \\\ftpserver\home\snapshots, especifique **\snapshots\ftp** para **@ftp_subdirectory** (a replicação acrescentará 'ftp' ao caminho da pasta de instantâneo ao criar os arquivos de instantâneo).    
    -   (Opcional) **@ftp_login** - uma conta de logon usada para conectar-se ao servidor FTP.    
    -   (Opcional) **@ftp_password** - a senha para o logon no FTP.  
  
     Isso cria uma publicação que usa FTP. Para obter mais informações, consulte [Criar uma assinatura](create-a-publication.md).  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication-that-uses-ftp-snapshot-delivery"></a>Para criar uma assinatura pull para um instantâneo ou publicação transacional que use a entrega de instantâneo FTP  
  
1.  No Assinante, no banco de dados de assinatura, execute [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Especifique **@publisher** e **@publication** .  
  
    -   No Assinante, no banco de dados de assinatura, execute [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Especificar **@publisher** , **@publisher_db** , **@publication** , o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] credenciais do Windows sob as quais o Distribution Agent a Assinante é executado para **@job_login** e **@job_password** e um valor de `true` para **@use_ftp** .  
  
2.  No Publicador do banco de dados de publicação, execute [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) para registrar a assinatura pull. Para obter mais informações, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication-that-uses-ftp-snapshot-delivery"></a>Para criar uma assinatura pull para uma publicação de mesclagem use a entrega de instantâneo FTP  
  
1.  No Assinante, no banco de dados de assinatura, execute o [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Especifique **@publisher** e **@publication** .   
2.  No Assinante, no banco de dados de assinatura, execute [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql). Especificar **@publisher** , **@publisher_db** , **@publication** , as credenciais do Windows sob as quais o Distribution Agent no assinante executa **@job_login** e **@job_password** e um valor de `true` para **@use_ftp** .    
3.  No Publicador do banco de dados de publicação, execute [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql) para registrar a assinatura pull. Para obter mais informações, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).  
  
#### <a name="to-change-one-or-more-ftp-snapshot-delivery-settings-for-a-snapshot-or-transactional-publication"></a>Para alterar uma ou outra configuração de entrega de instantâneo FTP para um instantâneo ou publicação transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Especifique um dos valores seguintes para **@property** e um valor novo dessa configuração para **@value** :    
    -   `ftp_address` - o endereço do servidor FTP usado para entregar o instantâneo.    
    -   `ftp_port` - a porta usada pelo servidor FTP.    
    -   `ftp_subdirectory`- o subdiretório do diretório de FTP padrão usado para o instantâneo de FTP.    
    -   `ftp_login` - um logon usado para conectar-se ao servidor FTP.    
    -   `ftp_password` - a senha para o logon no FTP.  
  
2.  (Opcional) Repita a etapa 1 para cada configuração FTP que é alterada.    
3.  (Opcional) Para desabilitar a entrega do instantâneo de FTP , execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de `enabled_for_internet` para **@property** e um valor de `false` para **@value** .  
  
#### <a name="to-change-ftp-snapshot-delivery-settings-for-a-merge-publication"></a>Para alterar a entrega do instantâneo de FTP para uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique um dos valores seguintes para **@property** e um valor novo dessa configuração para **@value** :  
  
    -   `ftp_address` - o endereço do servidor FTP usado para entregar o instantâneo.    
    -   `ftp_port` - a porta usada pelo servidor FTP.    
    -   `ftp_subdirectory`- o subdiretório do diretório de FTP padrão usado para o instantâneo de FTP.   
    -   `ftp_login` - um logon usado para conectar-se ao servidor FTP.    
    -   `ftp_password` - a senha para o logon no FTP.    
2.  (Opcional) Repita a etapa 1 para cada configuração FTP que é alterada.    
3.  (Opcional) Para desabilitar a entrega do instantâneo de FTP , execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de `enabled_for_internet` para **@property** e um valor de `false` para **@value** .  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 O exemplo seguinte cria uma publicação de mesclagem que permite aos Assinantes acessarem os dados de instantâneo que usam FTP. O Assinante deve usar uma conexão VPN segura ao acessar o compartilhamento de FTP. **sqlcmd** as variáveis de script são usadas para fornecer valores de logon e senha. Para obter mais informações, consulte [Usar sqlcmd com variáveis de script](../../scripting/sqlcmd-use-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubftp.sql#sp_createmergepub_ftp)]  
  
 O exemplo a seguir cria uma assinatura para uma publicação de mesclagem onde o Assinante obtém o instantâneo usando FTP. O Assinante deve usar uma conexão VPN segura ao acessar o compartilhamento de FTP. **sqlcmd** as variáveis de script são usadas para fornecer valores de logon e senha. Para obter mais informações, consulte [Usar sqlcmd com variáveis de script](../../scripting/sqlcmd-use-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsub_ftp)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsubagent_ftp)]  
  
## <a name="see-also"></a>Consulte também  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantâneos pelo FTP](../transfer-snapshots-through-ftp.md)   
 [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md)   
 [Inicializar uma assinatura com um instantâneo](../initialize-a-subscription-with-a-snapshot.md)  
  
  
