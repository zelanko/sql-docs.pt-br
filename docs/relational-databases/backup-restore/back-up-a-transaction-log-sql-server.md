---
title: Fazer backup de um log de transações (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction log backups [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- backing up transaction logs [SQL Server], SQL Server Management Studio
ms.assetid: 3426b5eb-6327-4c7f-88aa-37030be69fbf
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7373cd39e6ac616fe28a8fd386415dd4ce99016c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934510"
---
# <a name="back-up-a-transaction-log-sql-server"></a>Fazer backup de um log de transações (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como fazer backup de um log de transações no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou PowerShell.  
  
   
##  <a name="Restrictions"></a> Limitações e restrições  
  
-   A instrução BACKUP não é permitida em uma transação explícita ou [implícita](../../t-sql/statements/set-implicit-transactions-transact-sql.md) .  Uma transação explícita é aquela para a qual você define o início e término da transação explicitamente.
  
##  <a name="Recommendations"></a> Recomendações  
  
-   Se um banco de dados usar o [modelo de recuperação](recovery-models-sql-server.md) total ou log de transação em massa, você deverá fazer backup do log de transações com regularidade suficiente para proteger os dados e impedir que o [log de transações fique cheio](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md). Isso trunca o log e oferece suporte à restauração do banco de dados para um período específico. 
  
-   Por padrão, toda operação de backup bem-sucedida acrescenta uma entrada ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao log de eventos do sistema. Se você fizer backup do log com frequência, essas mensagens de êxito serão acumuladas muito rapidamente, resultando em logs de erros imensos que dificultam a localização de outras mensagens. Nessas situações, você pode suprimir essas entradas de log usando o sinalizador de rastreamento 3226, caso nenhum dos seus scripts dependa dessas entradas. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
  
##  <a name="Permissions"></a> Permissões  
**Verifique as permissões corretas antes de começar!** 

As permissões BACKUP DATABASE e BACKUP LOG necessárias são concedidas por padrão aos membros da função de servidor fixa **sysadmin** e às funções de banco de dados fixas **db_owner** e **db_backupoperator** .  
  
 Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup podem interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa deve ter permissões de gravação. No entanto, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, não verifica permissões de acesso a arquivos. Problemas de permissões no arquivo físico do dispositivo de backup poderão não ser tão claros até que você tente acessar o [recurso físico](backup-devices-sql-server.md) quando tentar fazer backup ou uma restauração. Novamente, verifique as permissões antes de começar!

[!INCLUDE[Freshness](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="back-up-using-ssms"></a>Fazer backup usando SSMS  
  
1.  Depois de conectar-se à instância adequada do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objeto, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Backup**. Será exibida a caixa de diálogo **Backup de Banco de Dados** .  
  
4.  Na caixa de listagem **Banco de Dados** , verifique o nome do banco de dados. Você pode, como opção, selecionar um banco de dados diferente da lista.  
  
5.  Verifique se o modelo de recuperação é **FULL** ou **BULK_LOGGED**.  
  
6.  Na caixa de listagem **Tipo de Backup** , selecione **Log de Transações**.  
  
7.  Opcionalmente, você pode selecionar **Copiar Somente Backup** para criar um backup somente cópia. Um *backup somente cópia* é um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não depende da sequência de backups convencionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
    > [!NOTE]
    > Quando a opção **Diferencial** está selecionada, você não pode criar um backup somente cópia.  
  
8.  Aceite o nome do conjunto de backup padrão sugerido na caixa de texto **Nome** ou digite um nome diferente para o conjunto de backup.  
  
9. Opcionalmente, na caixa de texto **Descrição** , digite uma descrição do conjunto de backup.  
  
10. Especifique quando o conjunto de backup irá expirar:  
  
    -   Para que o conjunto de backup expire depois de um número específico de dias, clique em **Depois** (a opção padrão) e digite quantos dias depois da criação do conjunto ele deve expirar. Esse valor pode ser de 0 a 99999 dias; 0 dia significa que o conjunto de backup nunca vai expirar.  
  
         O valor padrão é definido na opção **Retenção de mídia de backup padrão (em dias)** da caixa de diálogo **Propriedades do Servidor** (página**Configurações do Banco de Dados** ). Para acessar essa caixa de diálogo, clique com o botão direito do mouse no nome do servidor no Pesquisador de Objetos, selecione propriedades e a página **Configurações do Banco de Dados** .  
  
    -   Para que o conjunto de backup expire em uma data específica, clique no campo **Em**e digite a data de expiração do conjunto.  
  
11. Escolha o tipo do destino de backup clicando em **Disco**, **URL** ou **Fita**. Para selecionar os caminhos de até 64 unidades de disco ou fita que contêm um único conjunto de mídia, clique em **Adicionar**. Os caminhos selecionados são exibidos na caixa de listagem **Backup** .  
  
     Para remover um destino de backup, selecione-o e clique em **Remover**. Para exibir o conteúdo de um destino de backup, selecione-o e clique em **Conteúdo**.  
  
12. Para exibir ou selecionar as opções avançadas, clique em **Opções** no painel **Selecionar uma página** .  
  
13. Selecione uma opção **Substituir Mídia** , com um clique em uma das opções a seguir:  
  
    -   **Fazer backup no conjunto de mídias existente**  
  
         Para essa opção, clique em **Anexar ao conjunto de backup existente** ou **Substituir todos os conjuntos de backup existentes**. Para obter mais informações, veja [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Opcionalmente, selecione **Verificar nome do conjunto de mídias e validade do conjunto de backup** para que a operação de backup verifique a data e a hora em que o conjunto de mídias e de backup expiram.  
  
         Como opção, digite um nome na caixa de texto **Nome do conjunto de mídias** . Se nenhum nome for especificado, um conjunto de mídias com um nome em branco será criado. Se você especificar um nome de conjunto de mídias, a mídia (fita ou disco) é verificada para ver se o nome real corresponde ao nome digitado.  
  
         Se você deixar o nome da mídia em branco e marcar a caixa para verificar a mídia, a verificação terá sucesso se o nome da mídia também estiver em branco na mídia.  
  
    -   **Fazer backup em um novo conjunto de mídias e apagar todos os conjuntos de backup existentes**  
  
         Para essa opção, digite um nome na caixa de texto **Nome do novo conjunto de mídias** e, opcionalmente, descreva o conjunto de mídias na caixa de texto **Descrição do novo conjunto de mídias** . Para obter mais informações, consulte [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
14. Na seção **Confiabilidade** , como opção, marque:  
  
    -   **Verificar backup quando concluído**  
  
    -   **Executar soma de verificação antes de gravar na mídia**e, como opção, **Continuar com erro da soma de verificação**. Para obter informações sobre somas de verificação, veja [Erros de mídia possíveis durante backup e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
15. Na seção **Log de transações** :  
  
    -   Para fazer backups de log rotineiros, mantenha a seleção padrão **Truncar o log de transações removendo entradas inativas**.  
  
    -   Para fazer backup da parte final do log (ou seja, o log ativo), marque **Fazer backup da parte final do log e deixar o banco de dados no estado de restauração**.  
  
         Um backup da parte final do log é realizado após a falha do backup final do log a fim de evitar perda de trabalho. Fazer backup de log ativo (backup da parte final do log) após uma falha, antes do início da restauração do banco de dados ou ao executar failover em um banco de dados secundário. Selecionar esta opção é equivalente a especificar a opção NORECOVERY na instrução BACKUP LOG do Transact-SQL. Para obter mais informações sobre backups da parte final do log, veja [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
16. Se o backup estiver sendo feito em uma unidade de fita (conforme especificado na seção **Destino** da página **Geral** ), a opção **Descarregar a fita após o backup** estará ativa. Clicar nessa opção ativa a opção **Rebobinar a fita antes de descarregar** .  
  
17. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e posteriores dão suporte para [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md). Por padrão, a compactação de um backup depende do valor da opção de configuração de servidor **padrão de compactação de backup**. Porém, independentemente do padrão atual do nível do servidor, é possível compactar um backup, marcando a opção **Compactar backup**e evitar a compactação marcando **Não compactar o backup**.  
  
     **Para exibir o padrão de compactação de backup atual**  
  
    -   [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
 **Criptografia**  
  
 Para criptografar o arquivo de backup, marque a caixa de seleção **Criptografar backup** . Selecione um algoritmo de criptografia a ser usado para criptografar o arquivo de backup e forneça um Certificado ou uma Chave Assimétrica. Os algoritmos de criptografia disponíveis são:  
  
-   AES 128  
  
-   AES 192  
  
-   AES 256  
  
-   Triple DES  
  
 
## <a name="back-up-using-t-sql"></a>Fazer backup usando T-SQL  
  
1.  Execute a instrução BACKUP LOG para fazer backup do log de transações, especificando o seguinte:  
  
    -   O nome do banco de dados a que pertence o log de transações a ser feito backup.  
  
    -   O dispositivo de backup em que o backup de log de transações será gravado.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
  
> **IMPORTANTE!** Este exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , que usa o modelo de recuperação simples. Para permitir backups de log, antes de fazer um backup de banco de dados completo, o banco de dados foi definido para usar o modelo de recuperação completa. Para obter mais informações, veja [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
 Este exemplo cria um backup de log de transações do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] para o dispositivo de backup criado anteriormente e denominado `MyAdvWorks_FullRM_log1`.  
  
```sql  
BACKUP LOG AdventureWorks2012  
   TO MyAdvWorks_FullRM_log1;  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
  
1.  Use o **Backup-SqlDatabase** cmdlet e especifique **Log** para o valor do parâmetro **-BackupAction** .  
  
     O exemplo a seguir cria um backup do log do banco de dados `MyDB` para o local de backup padrão da instância de servidor `Computer\Instance`.  
  
    ```sql  
    --Enter this command at the PowerShell command prompt, C:\PS>  
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Log  
    ```  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Related tasks  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   [Solução de problemas de um log de transação completa &#40;Erro do SQL Server 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
## <a name="more-information"></a>Mais informações 
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Backups completos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)  
  
  
