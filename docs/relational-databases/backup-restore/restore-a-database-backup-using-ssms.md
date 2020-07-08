---
title: Restaurar um backup de banco de dados usando o SSMS | Microsoft Docs
description: Este artigo explica como restaurar um backup completo do banco de dados do SQL Server usando o SQL Server Management Studio.
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.locatebackupfileazure.f1
- sql13.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2e23cceab272e11eedb1fa99250dce5520ada073
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718013"
---
# <a name="restore-a-database-backup-using-ssms"></a>Restore a Database Backup Using SSMS
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Este tópico explica como restaurar um backup completo do banco de dados usando o SQL Server Management Studio.    
       
### <a name="important"></a>Importante:    
Antes de poder restaurar um banco de dados no modelo de recuperação completa ou bulk-logged, talvez seja necessário fazer backup do log de transações ativas (conhecido como a [parte final do log](tail-log-backups-sql-server.md)). Para obter mais informações, veja [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)).  

Ao restaurar um banco de dados de outra instância, considere as informações descritas em [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).   
    
Para restaurar um banco de dados criptografado, você precisa ter acesso ao certificado ou à chave assimétrica usada para criptografar o banco de dados. Sem o certificado ou a chave assimétrica, não é possível restaurar o banco de dados. Você deverá manter o certificado usado para criptografar a chave de criptografia do banco de dados durante o tempo que precisar salvar o backup. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).    
    
Se você restaurar um banco de dados de versão anterior para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], esse banco de dados será atualizado automaticamente para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Isso impede que o banco de dados seja usado com uma versão anterior da [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. No entanto, isso se relaciona com a atualização dos metadados e não afeta o [nível de compatibilidade do banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md). Se o nível de compatibilidade de um banco de dados de usuário for 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização. Se o nível de compatibilidade for 90 ou inferior antes da atualização, no banco de dados atualizado, o nível de compatibilidade será definido como 100, que é o nível de compatibilidade mais baixo com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
Normalmente, o banco de dados se torna disponível imediatamente. No entanto, se o banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices, dependendo da definição da propriedade de servidor **Opção de Atualização de Texto Completo** . Se a opção de atualização for definida como **Importar** ou **Recriar**, os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados que serão indexados, a importação poderá demorar várias horas, e a recompilação será até dez vezes mais demorada.     
    
Quando a opção de atualização for definida como **Importar**, se não houver um catálogo de texto completo disponível, os índices de texto completo associados serão recompilados. Para obter informações sobre como exibir ou alterar a configuração da propriedade **Full-Text Upgrade Option** , veja [Gerenciar e monitorar a pesquisa de texto completo para uma instância de servidor](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).    

Para obter informações sobre a restauração do serviço de armazenamento de Blobs do Microsoft Azure, veja [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).

## <a name="examples"></a>Exemplos
    
### <a name="a-restore-a-full-database-backup"></a>a. Restaurar um backup de banco de dados completo   
    
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
    
2.  Clique com o botão direito do mouse em **Bancos de Dados** e selecione **Restaurar Banco de Dados...**    
    
3.  Na página **Geral** , use a seção **Origem** para especificar a origem e o local dos conjuntos de backup a serem restaurados. Selecione uma das seguintes opções:    
    
    -   **Backup de banco de dados**    
    
         Selecione o banco de dados a ser restaurado na lista suspensa. A lista contém apenas os bancos de dados dos quais foi feito um backup de acordo com o histórico de backup do **msdb** .    
    
        > [!NOTE]
        > Se o backup foi obtido de um servidor diferente, o servidor de destino não terá informações de histórico de backup para o banco de dados especificado. Nesse caso, selecione **Dispositivo** para especificar manualmente o arquivo ou o dispositivo a ser restaurado. 
    
    -   **Dispositivo**    
    
         Clique no botão Procurar ( **...** ) para abrir a caixa de diálogo **Selecione dispositivos de backup** . 
         
        -   Caixa de diálogo**Selecionar dispositivos de backup**  
        
            **Tipo de mídia de backup**  
         Selecione um tipo de mídia na lista suspensa **Tipo de mídia de backup** .  Observação: A opção **Fita** só aparece se houver uma unidade de fita montada no computador, e a opção **Dispositivo de backup** só aparece se houver, no mínimo, um dispositivo de backup.

            **Adicionar**  
            Dependendo do tipo de mídia selecionado no campo **Tipo de mídia de backup** , clicar em **Adicionar** abre uma das caixas de diálogo a seguir. (Se a lista na caixa de listagem **Mídia de backup** estiver cheia, o botão **Adicionar** não estará disponível.)

            |Típo de mídia|Caixa de diálogo|Descrição|    
            |----------------|----------------|-----------------|    
            |**Arquivo**|**Localizar o arquivo de backup**|Nessa caixa de diálogo, você pode selecionar um arquivo local da árvore ou pode especificar um arquivo remoto que use o seu nome totalmente qualificado da UNC (Convenção Universal de Nomenclatura). Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).|    
            |**Dispositivo**|**Selecionar dispositivo de backup**|Nessa caixa de diálogo você pode selecionar em uma lista de dispositivos lógicos de backup, definida na instância de servidor.|    
            |**Fita**|**Selecionar fita de backup**|Nessa caixa de diálogo você pode selecionar em uma lista de unidades de fita conectadas fisicamente ao computador que executa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|    
            |**URL**|**Selecionar um local de arquivo de backup**|Nesta caixa de diálogo, você pode selecionar um contêiner de armazenamento do Azure/credenciais do SQL Server, adicionar um novo contêiner de armazenamento do Azure com uma assinatura de acesso compartilhado ou gerar uma assinatura de acesso compartilhado e uma credencial do SQL Server para um contêiner de armazenamento existente.  Veja também [Conectar-se a uma Assinatura do Microsoft Azure](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)|  
         
             **Remover**    
             Remove um ou mais arquivos, fitas ou dispositivos de backup lógicos selecionados.    
                 
             **Sumário**    
            Exibe o conteúdos da mídia de um arquivo, fita ou dispositivo de backup lógico selecionado.  Esse botão poderá não funcionar se o tipo de mídia for **URL**.  

             **Mídia de backup**   
             Lista a mídia selecionada.
    
             Após adicionar os dispositivos desejados à caixa de listagem **Mídia de backup** , clique em **OK** para voltar à página **Geral** .    
    
         Na caixa de listagem **Fonte: Dispositivo: Banco de Dados**, selecione o nome do banco de dados que deve ser restaurado.    
    
         > [!NOTE]
         > Essa lista estará disponível apenas quando **Dispositivo** for selecionado. Apenas os bancos de dados que têm backups no dispositivo selecionado estarão disponíveis.    
     
4.  Na seção **Destino** , a caixa **Banco de Dados** é preenchida automaticamente com o nome do banco de dados a ser restaurado. Para alterar o nome do banco de dados, digite o novo nome na caixa **Banco de Dados** .    
    
5.  Na caixa **Restaurar para** , deixe o padrão como **Para o último backup obtido** ou clique em **Linha do tempo** para acessar a caixa de diálogo **Linha do Tempo de Backup** para selecionar manualmente um momento determinado a fim de interromper a ação de recuperação. Para obter mais informações sobre como designar um momento específico, consulte [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md).    
    
6.  Na grade **Conjuntos de backup a serem restaurados** , selecione os backups a serem restaurados. Essa grade exibe os backups disponíveis para o local especificado. Por padrão, um plano de recuperação é sugerido. Para substituir o plano de recuperação sugerido, você pode alterar as seleções na grade. Backups que dependem da restauração de um backup anterior têm a seleção automaticamente cancelada quando a seleção do backup anterior é cancelada. Para obter informações sobre as colunas da grade **Conjuntos de backup a serem restaurados** , veja [Restaurar banco de dados &#40;página Geral&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)).    
    
7.  Opcionalmente, clique em **Arquivos** no painel **Selecionar uma página** para acessar a caixa de diálogo **Arquivos de Banco de Dados** . Daqui, você pode restaurar o banco de dados em um novo local, com a especificação de um novo destino de restauração para cada arquivo na grade **Restaurar os arquivos de banco de dados como** . Para obter mais informações sobre essa grade, veja [Restaurar banco de dados &#40;Página Arquivos&#41;](../../relational-databases/backup-restore/restore-database-files-page.md).    
    
8. Para exibir ou selecionar as opções avançadas, na página **Opções** , no painel **Opções de restauração** , você pode selecionar qualquer uma das seguintes opções, de acordo com sua situação:    

   1. Opções**WITH** (não necessárias):    
    
     - **Substituir o banco de dados existente (WITH REPLACE)**    
    
     - **Preservar as configurações de replicação (WITH KEEP_REPLICATION)**    
    
     - **Acesso restrito ao banco de dados restaurado (WITH RESTRICTED_USER)**    
    
   2. Selecione uma opção para a caixa **Estado de recuperação** . Essa caixa determina o estado do banco de dados após a operação de restauração.    
    
     - **RESTORE WITH RECOVERY** é o comportamento padrão que deixa o banco de dados pronto para uso revertendo as transações não confirmadas. Os logs de transações adicionais não podem ser restaurados. Selecione essa opção se você estiver restaurando todos os backups necessários agora.    
    
     - **RESTORE WITH NORECOVERY** deixa o banco de dados não operacional e não reverte as transações não confirmadas. Os logs de transações adicionais podem ser restaurados. Só é possível usar o banco de dados depois que ele é recuperado.    
    
     - **RESTORE WITH STANDBY** deixa o banco de dados no modo somente leitura. Ele desfaz as transações não confirmadas, mas salva as ações de desfazer em um arquivo em espera para que os efeitos da recuperação possam ser revertidos.    
    
   3. **Faça backup da parte final do log antes da restauração.** Nem todos os cenários de restauração exigem um backup da parte final do log.  Para obter mais informações, veja **Cenários que exigem um backup da parte final do log** de [Backups da parte final do log (SQL Server).](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)
  
   4. As operações de restauração poderão falhar se houver conexões ativas com o banco de dados. Marque a opção **Fechar conexões existentes** para assegurar que todas as conexões ativas entre o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e o banco de dados sejam fechadas. Essa caixa de seleção define o banco de dados no modo de usuário único antes de executar as operações de restauração e define o banco de dados no modo de vários usuários ao concluir.    
  
   5. Selecione **Perguntar antes de restaurar cada backup** para que você seja solicitado entre cada operação de restauração. Isso normalmente só é necessário quando o banco de dados é grande e você deseja monitorar o status da operação de restauração.    
    
Para obter mais informações sobre essas opções de restauração, veja [Restaurar banco de dados &#40;página Opções&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)).    
    
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="b-restore-an-earlier-disk-backup-over-an-existing-database"></a>B. Restaurar um backup anterior de disco sobre um banco de dados existente
O exemplo a seguir restaura um backup anterior de disco do `Sales` e substitui o banco de dados existente `Sales` .

1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
2.  Clique com o botão direito do mouse em **Bancos de Dados** e selecione **Restaurar Banco de Dados...**  
3.  Na página **Geral** , selecione **Dispositivo** na seção **Fonte** .
4.  Clique no botão Procurar ( **...** ) para abrir a caixa de diálogo **Selecione dispositivos de backup** . Clique em **Adicionar** e navegue até o backup. Clique em **OK** depois de selecionar os arquivos de backup em disco.
5.  Clique em **OK** para retornar à página **Geral** .
6.  Clique em **Opções** no painel **Selecionar uma página** .
7.  Na seção **Opções de restauração** , marque a opção **Substituir o banco de dados existente (WITH REPLACE)** .

    > [!NOTE]
    > Não marcar essa opção poderá resultar na seguinte mensagem de erro: "System.Data.SqlClient.SqlError: O conjunto de backup contém um backup de um banco de dados diferente do banco de dados "`Sales`" existente. (Microsoft.SqlServer.SmoExtended)”

8.  Na seção **Backup da parte final do log** , desmarque a opção **Fazer backup da parte final do log antes da restauração**.

    > [!NOTE]
    > Nem todos os cenários de restauração exigem um backup da parte final do log. Você não precisará de um backup da parte final do log se o ponto de recuperação estiver em um backup de log anterior. Além disso, um backup da parte final do log será desnecessário se você estiver movendo ou substituindo um banco de dados e não precisar restaurá-lo para um momento determinado após o seu backup mais recente. Para obter mais informações, veja [Backups da parte final do log (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).

    Essa opção não está disponível em bancos de dados no modelo de recuperação SIMPLES.

9.  Na seção **Conexões de servidor** , marque a opção **Fechar conexões existentes com o banco de dados de destino**.

    > [!NOTE]
    > Não marcar essa opção poderá resultar na seguinte mensagem de erro: "System.Data.SqlClient.SqlError: Não foi possível obter acesso exclusivo porque o banco de dados está sendo usado. (Microsoft.SqlServer.SmoExtended)”
    
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="c--restore-an-earlier-disk-backup-with-a-new-database-name-where-the-original-database-still-exists"></a>C.  Restaurar um backup anterior de disco com um novo nome de banco de dados no local em que o banco de dados original ainda existe
O exemplo a seguir restaura um backup anterior de disco do `Sales` e cria um novo banco de dados chamado `SalesTest`.  O banco de dados original, `Sales`, ainda existe no servidor.

1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
2.  Clique com o botão direito do mouse em **Bancos de Dados** e selecione **Restaurar Banco de Dados...**  
3.  Na página **Geral** , selecione **Dispositivo** na seção **Fonte** .
4.  Clique no botão Procurar ( **...** ) para abrir a caixa de diálogo **Selecione dispositivos de backup** . Clique em **Adicionar** e navegue até o backup. Clique em **OK** depois de selecionar os arquivos de backup em disco.
5.  Clique em **OK** para retornar à página **Geral** .
6.  Na seção **Destino** , a caixa **Banco de Dados** é preenchida automaticamente com o nome do banco de dados a ser restaurado. Para alterar o nome do banco de dados, digite o novo nome na caixa **Banco de Dados** .
7.  Clique em **Opções** no painel **Selecionar uma página** .
8.  Na seção **Backup da parte final do log** , desmarque a opção “**Fazer backup da parte final do log antes da restauração**”.

    > [!IMPORTANT]
    > Não desmarcar essa opção resultará na alteração do estado de restauração do banco de dados existente, `Sales`.

9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

    > [!NOTE]
    > Se você receber a seguinte mensagem de erro:      
    > "System.Data.SqlClient.SqlError: O backup da parte final do log do banco de dados "`Sales`" não foi feito. Use `BACKUP LOG WITH NORECOVERY` para fazer backup do log se ele contiver trabalho que você não deseja perder. Use a cláusula `WITH REPLACE` ou `WITH STOPAT` da instrução `RESTORE` para simplesmente substituir o conteúdo do log. (Microsoft.SqlServer.SmoExtended)”.      
    > Em seguida, é provável que você não inseriu o novo nome do banco de dados da Etapa 6 acima. Normalmente a restauração evita a substituição acidental de um banco de dados por um banco de dados diferente. Se o banco de dados especificado em uma instrução `RESTORE` já existir no servidor atual e a GUID de família do banco de dados especificado for diferente da GUID de família do banco de dados registrado no conjunto de backup, o banco de dados não será restaurado. Essa é uma proteção importante.

### <a name="d--restore-earlier-disk-backups-to-a-point-in-time"></a>D.  Restaurar backups anteriores de disco em um ponto específico
O exemplo a seguir restaura um banco de dados para seu estado de `1:23:17 PM` em `May 30, 2016` e mostra uma operação de restauração que envolve vários backups de log. Atualmente, o banco de dados não existe no servidor.

1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
2.  Clique com o botão direito do mouse em **Bancos de Dados** e selecione **Restaurar Banco de Dados...**  
3.  Na página **Geral** , selecione **Dispositivo** na seção **Fonte** .
4.  Clique no botão Procurar ( **...** ) para abrir a caixa de diálogo **Selecione dispositivos de backup** . Clique em **Adicionar** e navegue até o backup completo e todos os backups de log de transações relevantes.  Clique em **OK** depois de selecionar os arquivos de backup em disco.
5.  Clique em **OK** para retornar à página **Geral** .
6.  Na seção **Destino** , clique em **Linha do tempo** para acessar a caixa de diálogo **Linha do Tempo de Backup** para selecionar manualmente um ponto específico para interromper a ação de recuperação.
7.  Selecione **Data e hora específicas**.  
8.  Altere o **Intervalo da linha do tempo** para **Hora** na caixa suspensa (opcional).  
9.  Mova o controle deslizante para o tempo desejado.
10. Clique em **OK** para retornar à página Geral.
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="e--restore-a-backup-from-the-microsoft-azure-storage-service"></a>E.  Restaurar um backup do serviço de armazenamento do Microsoft Azure

#### <a name="common-steps"></a>Etapas comuns
Os dois exemplos a seguir executam uma restauração de `Sales` de um backup localizado no serviço de armazenamento do Microsoft Azure.  O nome da Conta de armazenamento é `mystorageaccount`.  O contêiner é chamado `myfirstcontainer`.  Para resumir, as seis primeiras etapas são listadas aqui uma vez e todos os exemplos serão iniciados na **Etapa 7**.
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.
2.  Clique com o botão direito do mouse em **Bancos de Dados** e selecione **Restaurar Banco de Dados...** .
3.  Na página **Geral** , selecione **Dispositivo** na seção **Fonte** .
4.  Clique no botão Procurar (...) para abrir a caixa de diálogo **Selecione dispositivos de backup** .    
5.  Selecione **URL** na lista suspensa **Tipo de mídia de backup:** .
6.  Clique em **Adicionar** e a caixa de diálogo **Selecione um Local do Arquivo de Backup** será aberta.

#### <a name="e1---restore-a-striped-backup-over-an-existing-database-and-a-shared-access-signature-exists"></a>E1.   Restaure um backup distribuído em um banco de dados e em uma assinatura de acesso compartilhado existentes.
Uma política de acesso armazenado foi criada com direitos de leitura, gravação, exclusão e lista.  Uma assinatura de acesso compartilhado associada à política de acesso armazenado foi criada para o contêiner `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`.  Basicamente, as etapas são as mesmas que seriam usadas se já existisse uma credencial do SQL Server.  Atualmente, o banco de dados `Sales` existe no servidor.  Os arquivos de backup são `Sales_stripe1of2_20160601.bak` e `Sales_stripe2of2_20160601.bak`.  

1.  Selecione `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` na lista suspensa **Contêiner de armazenamento do Azure:** se já existir uma credencial do SQL Server; caso contrário, insira manualmente o nome do contêiner, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`. 
1. Insira a assinatura de acesso compartilhado na caixa RTF **Assinatura de acesso compartilhado:** .
1. Clique em **OK** e a caixa de diálogo **Localizar Arquivo de Backup no Microsoft Azure** será aberta.
1. Expanda **Contêineres** e navegue até `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`.
1. Mantenha pressionada a tecla CTRL e selecione os arquivos `Sales_stripe1of2_20160601.bak` e `Sales_stripe2of2_20160601.bak`.
1. Clique em **OK**.
1. Clique em **OK** para retornar à página **Geral** .
1. Clique em **Opções** no painel **Selecionar uma página** .
1. Na seção Opções de **restauração** , marque a opção **Substituir o banco de dados existente (WITH REPLACE)** .
1. Na seção **Backup da parte final do log** , desmarque a opção **Fazer backup da parte final do log antes da restauração**.
1. Na seção **Conexões de servidor** , marque a opção **Fechar conexões existentes com o banco de dados de destino**.
1. Clique em **OK**.

#### <a name="e2---a-shared-access-signature-does-not-exist"></a>E2.   Não há uma assinatura de acesso compartilhado
Neste exemplo, atualmente, o banco de dados `Sales` não existe no servidor.
1. Clique em **Adicionar** e a caixa de diálogo **Conectar-se a uma Assinatura da Microsoft** será aberta.  
1. Conclua a caixa de diálogo **Conectar-se a uma Assinatura da Microsoft** e clique em **OK** para retornar à caixa de diálogo **Selecionar um local de arquivo de backup** .  Veja [Conectar-se a uma assinatura do Microsoft Azure](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md) para obter mais informações.
1. Clique em **OK** na caixa de diálogo **Selecionar um local de arquivo de backup** e a caixa de diálogo **Localizar arquivo de backup no Microsoft Azure** será aberta.
1. Expanda **Contêineres** e navegue até `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`.
1. Selecione o arquivo de backup e clique em **OK**.
1. Clique em **OK** para retornar à página **Geral** .
1. Clique em **OK**.

#### <a name="f-restore-local-backup-to-microsoft-azure-storage-url"></a>F. Restaurar o backup local no armazenamento do Microsoft Azure (URL)
O banco de dados `Sales` será restaurado para o contêiner de armazenamento do Microsoft Azure `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` de um backup localizado em `E:\MSSQL\BAK`.  A credencial do SQL Server para o contêiner do Azure já foi criada.  Uma credencial do SQL Server para o contêiner de destino já deve existir, pois não pode ser criada por meio da tarefa **Restaurar** .  Atualmente, o banco de dados `Sales` não existe no servidor.
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.
2.  Clique com o botão direito do mouse em **Bancos de Dados** e selecione **Restaurar Banco de Dados...** .
3.  Na página **Geral** , selecione **Dispositivo** na seção **Fonte** .
4.  Clique no botão Procurar (...) para abrir a caixa de diálogo **Selecione dispositivos de backup** .  
5.  Selecione **Arquivo** na lista suspensa **Tipo de mídia de backup:** .
6.  Clique em **Adicionar** e a caixa de diálogo **Localizar arquivo de backup** será aberta.
7.  Navegue até `E:\MSSQL\BAK`, selecione o arquivo de backup e clique em **OK**.
8.  Clique em **OK** para retornar à página **Geral** .
9.  Clique em **Arquivos** no painel **Selecionar uma página** .
10. Marque a caixa de seleção **Relocar todos os arquivos para a pasta**.
11. Insira o contêiner, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, nas caixas de texto de **Pasta do arquivo de dados:** e **Pasta do arquivo de log:** .
12. Clique em **OK**.

## <a name="see-also"></a>Consulte Também    
 [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)     
 [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)     
 [Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)     
 [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)     
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)     
 [Restaurar banco de dados &#40;página Opções&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)     
 [Restaurar banco de dados &#40;página Geral&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)    
    
  
