---
title: Entregar um instantâneo pelo FTP | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
caps.latest.revision: 47
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 991c8ab81340b5ab9b03b79174e7a60e33b505cf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32964761"
---
# <a name="deliver-a-snapshot-through-ftp"></a>Entregar um instantâneo pelo FTP
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como entregar um instantâneo pelo FTP no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para entregar um instantâneo pelo FTP, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se forem usadas assinaturas pull, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\ftpserver\home\snapshots. Para obter mais informações, consulte [Proteger a pasta de instantâneos](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Para transferir arquivos de instantâneo que usam Protocolo de Transferência de Arquivo (FTP), deve-se, em primeiro lugar, configurar um servidor de FTP. Para obter mais informações, consulte a documentação [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Serviços de Informações da Internet (IIS).  
  
###  <a name="Security"></a> Segurança  
 Para ajudar a melhorar a segurança, recomendamos implementar uma rede privada virtual (VPN) ao usar a entrega de instantâneo FTP pela Internet. Para obter mais informações, consulte [Publicar dados pela Internet usando VPN](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md).  
  
 Como uma prática recomendada de segurança, não permita logons anônimos ao servidor FTP. O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se forem usadas assinaturas pull, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\ftpserver\home\snapshots. Para obter mais informações, consulte [Proteger a pasta de instantâneos](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
 Quando possível, solicite que os usuários insiram suas credenciais em tempo de execução. Se você armazenar credenciais em um arquivo de script, será necessário proteger o arquivo.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Depois que o servidor FTP for configurado, especifique informações de diretório e de segurança para esse servidor na caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-ftp-information"></a>Para especificar informações de FTP  
  
1.  Na caixa de diálogo **Propriedades da Publicação – \<Publicação>**, selecione **Permitir que os Assinantes baixem os arquivos de instantâneo usando FTP** de uma das seguintes páginas:  
  
    -   A página **Instantâneo de FTP** para publicações de instantâneo e transacionais e publicações de mesclagem para Publicadores executando versões anteriores ao [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
    -   A página **Instantâneo de FTP e Internet** , para publicações de mesclagem de Publicadores executando [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou versões posteriores.  
  
2.  Especifique valores para **Nome do servidor FTP**, **Número da porta**, **Caminho da pasta raiz de FTP**, **Logon**e **Senha**.  
  
     Por exemplo, se a raiz do servidor FTP for \\\ftpserver\home e você quiser que os instantâneos sejam armazenados em \\\ftpserver\home\snapshots, especifique \snapshots\ftp para a propriedade **Caminho da pasta raiz de FTP** (a replicação acrescentará 'ftp' ao caminho da pasta de instantâneo ao criar os arquivos de instantâneo).  
  
3.  Especifique que o Agente de Instantâneo deve gravar os arquivos de instantâneo no diretório especificado na etapa 2. Por exemplo, para que o Snapshot Agent grave os arquivos de instantâneo em \\\ftpserver\home\snapshots, é necessário especificar o caminho \\\ftpserver\home\snapshots em um ou dois locais:  
  
    -   O local de instantâneo padrão para o Distribuidor associado a essa publicação.  
  
         Para obter mais informações sobre como especificar o local de instantâneo padrão, consulte [Como especificar o local do instantâneo padrão &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md).  
  
    -   Um local alternativo de pasta de instantâneo para essa publicação. Um local alternativo será requerido se o instantâneo for compactado.  
  
         Insira o caminho na caixa de texto **Colocar os arquivos nesta pasta** na página Instantâneo da caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre locais alternativos da pasta de instantâneo, consulte [Alternate Snapshot Folder Locations](../../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 A opção para tornar os arquivos de instantâneo disponíveis em um servidor FTP podem ser definidas, e essas configurações FTP podem ser modificadas programaticamente usando procedimentos de armazenamento. O procedimento usado depende do tipo de publicação. A entrega de instantâneo FTP é usada apenas com assinaturas pull.  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-snapshot-or-transactional-publication"></a>Par habilitar a entrega de instantâneo FTP para um instantâneo ou publicação transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Especifique **@publication**, um valor de **true** para **@enabled_for_internet**e valores adequados para os seguintes parâmetros:  
  
    -   **@ftp_address** - o endereço do servidor FTP usado para entregar o instantâneo.  
  
    -   (Opcional) **@ftp_port** - a porta usada pelo servidor FTP.  
  
    -   (Opcional) **@ftp_subdirectory** - o subdiretório do diretório FTP padrão atribuído a um logon de FTP. Por exemplo, se a raiz do servidor FTP for \\\ftpserver\home e você desejar que os instantâneos sejam armazenados em \\\ftpserver\home\snapshots, especifique **\snapshots\ftp** para **@ftp_subdirectory** (a replicação acrescentará 'ftp' ao caminho da pasta de instantâneo ao criar os arquivos de instantâneo).  
  
    -   (Opcional) **@ftp_login** - uma conta de logon usada para conectar-se ao servidor FTP.  
  
    -   (Opcional) **@ftp_password** - a senha para o logon no FTP.  
  
     Isso cria uma publicação que usa FTP. Para obter mais informações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-merge-publication"></a>Para habilitar a entrega de instantâneo FTP para uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique **@publication**, um valor de **true** para **@enabled_for_internet** e valores adequados para os seguintes parâmetros:  
  
    -   **@ftp_address** - o endereço do servidor FTP usado para entregar o instantâneo.  
  
    -   (Opcional) **@ftp_port** - a porta usada pelo servidor FTP.  
  
    -   (Opcional) **@ftp_subdirectory** - o subdiretório do diretório FTP padrão atribuído a um logon de FTP. Por exemplo, se a raiz do servidor FTP for \\\ftpserver\home e você desejar que os instantâneos sejam armazenados em \\\ftpserver\home\snapshots, especifique **\snapshots\ftp** para **@ftp_subdirectory** (a replicação acrescentará 'ftp' ao caminho da pasta de instantâneo ao criar os arquivos de instantâneo).  
  
    -   (Opcional) **@ftp_login** - uma conta de logon usada para conectar-se ao servidor FTP.  
  
    -   (Opcional) **@ftp_password** - a senha para o logon no FTP.  
  
     Isso cria uma publicação que usa FTP. Para obter mais informações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication-that-uses-ftp-snapshot-delivery"></a>Para criar uma assinatura pull para um instantâneo ou publicação transacional que use a entrega de instantâneo FTP  
  
1.  No Assinante, no banco de dados de assinatura, execute [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Especifique **@publisher** e **@publication**.  
  
    -   No Assinante, no banco de dados de assinatura, execute [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, As credenciais do Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)] nas quais o Distribution Agent no Assinante executa do **@job_login** e **@job_password**e um valor de **true** para **@use_ftp**.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) para registrar a assinatura pull. Para obter mais informações, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication-that-uses-ftp-snapshot-delivery"></a>Para criar uma assinatura pull para uma publicação de mesclagem use a entrega de instantâneo FTP  
  
1.  No Assinante, no banco de dados de assinatura, execute o [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Especifique **@publisher** e **@publication**.  
  
2.  No Assinante, no banco de dados de assinatura, execute [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, As credenciais do Windows nas quais o Distribution Agent no Assinante executa do **@job_login** e **@job_password**e um valor de **true** para **@use_ftp**.  
  
3.  No Publicador do banco de dados de publicação, execute [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) para registrar a assinatura pull. Para obter mais informações, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
#### <a name="to-change-one-or-more-ftp-snapshot-delivery-settings-for-a-snapshot-or-transactional-publication"></a>Para alterar uma ou outra configuração de entrega de instantâneo FTP para um instantâneo ou publicação transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Especifique um dos valores seguintes para **@property** e um valor novo dessa configuração para **@value**:  
  
    -   **ftp_address** - o endereço do servidor FTP usado para entregar o instantâneo.  
  
    -   **ftp_port** - a porta usada pelo servidor FTP.  
  
    -   **ftp_subdirectory** - o subdiretório do diretório de FTP padrão usado para o instantâneo de FTP.  
  
    -   **ftp_login** - um logon usado para conectar-se ao servidor FTP.  
  
    -   **ftp_password** - a senha para o logon no FTP.  
  
2.  (Opcional) Repita a etapa 1 para cada configuração FTP que é alterada.  
  
3.  (Opcional) Para desabilitar a entrega do instantâneo de FTP , execute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) no Publicador do banco de dados de publicação. Especifique um valor de **enabled_for_internet** para **@property** e um valor de **false** para **@value**.  
  
#### <a name="to-change-ftp-snapshot-delivery-settings-for-a-merge-publication"></a>Para alterar a entrega do instantâneo de FTP para uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique um dos valores seguintes para **@property** e um valor novo dessa configuração para **@value**:  
  
    -   **ftp_address** - o endereço do servidor FTP usado para entregar o instantâneo.  
  
    -   **ftp_port** - a porta usada pelo servidor FTP.  
  
    -   **ftp_subdirectory** - o subdiretório do diretório de FTP padrão usado para o instantâneo de FTP.  
  
    -   **ftp_login** - um logon usado para conectar-se ao servidor FTP.  
  
    -   **ftp_password** - a senha para o logon no FTP.  
  
2.  (Opcional) Repita a etapa 1 para cada configuração FTP que é alterada.  
  
3.  (Opcional) Para desabilitar a entrega do instantâneo de FTP , execute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) no Publicador do banco de dados de publicação. Especifique um valor de **enabled_for_internet** para **@property** e um valor de **false** para **@value**.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 O exemplo seguinte cria uma publicação de mesclagem que permite aos Assinantes acessarem os dados de instantâneo que usam FTP. O Assinante deve usar uma conexão VPN segura ao acessar o compartilhamento de FTP. **sqlcmd** as variáveis de script são usadas para fornecer valores de logon e senha. Para obter mais informações, consulte [Usar sqlcmd com variáveis de script](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_1.sql)]  
  
 O exemplo a seguir cria uma assinatura para uma publicação de mesclagem onde o Assinante obtém o instantâneo usando FTP. O Assinante deve usar uma conexão VPN segura ao acessar o compartilhamento de FTP. **sqlcmd** as variáveis de script são usadas para fornecer valores de logon e senha. Para obter mais informações, consulte [Usar sqlcmd com variáveis de script](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_2.sql)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_3.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantâneos pelo FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Inicializar uma assinatura com um instantâneo](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
