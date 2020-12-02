---
title: Backup diferencial
description: Este artigo mostra como criar um backup de banco de dados diferencial no SQL Server usando o SQL Server Management Studio ou o Transact-SQL.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full differential backups [SQL Server]
- database backups [SQL Server], full differential backups
- backing up databases [SQL Server], full differential backups
- backups [SQL Server], creating
ms.assetid: 70f49794-b217-4519-9f2a-76ed61fa9f99
author: cawrites
ms.author: chadam
ms.openlocfilehash: 5362d3ddde85b21c5450a162fff0fdc5f23cda7f
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130462"
---
# <a name="create-a-differential-database-backup-sql-server"></a>Criar um backup diferencial de banco de dados (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Crie um backup de banco de dados diferencial no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Seções neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para criar um backup de banco de dados diferencial usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   A instrução BACKUP não é permitida em uma transação explícita ou implícita.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   A criação de um backup diferencial de banco de dados exige um backup completo de banco de dados anterior. Se seu banco de dados nunca tiver sido salvo, faça um backup completo antes de criar qualquer backup diferencial. Para obter mais informações, veja [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Como os backups diferenciais aumentam em tamanho, a restauração de um backup diferencial aumentará de forma significativa o tempo necessário para restaurar um banco de dados. Recomendamos que você use um backup completo novo em intervalos definidos para estabelecer uma nova base diferencial para os dados. Por exemplo, você poderia usar um backup completo semanal de todo o banco de dados (isto é, um backup completo do banco de dados) seguido de uma série regular de backups diferenciais do banco de dados durante a semana.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="check-your-permissions-first"></a><a name="Permissions"></a> Verifique suas permissões primeiro!  
 As permissões BACKUP DATABASE e BACKUP LOG usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator** .  
  
 Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup vão interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa deve ter permissões de gravação. No entanto, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, **não** verifica permissões de acesso a arquivos. Os problemas de permissões no arquivo físico do dispositivo de backup não serão óbvios até o recurso físico ser acessado quando você tentar fazer backup ou restaurar.  
  
##  <a name="sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio  
  
#### <a name="create-a-differential-database-backup"></a>Criar um backup diferencial de banco de dados  

1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], em Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados** e, dependendo do banco de dados, selecione um banco de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas** e clique em **Backup**. Será exibida a caixa de diálogo **Backup de Banco de Dados** .  
  
4.  Na caixa de listagem **Banco de Dados** , verifique o nome do banco de dados. Você pode, como opção, selecionar um banco de dados diferente da lista.  
  
     É possível executar um backup diferencial para qualquer modelo de recuperação (completo, bulk-logged ou simples).  
  
5.  Na caixa de listagem **Tipo de backup** , selecione **Diferencial**.  
  
    > [!IMPORTANT]  
    >  Quando você selecionar **Diferencial** , verifique se a caixa de seleção **Copiar Somente Backup** está desmarcada.  
  
6.  Para **Componente de backup**, clique em **Banco de Dados**.  
  
7.  Aceite o nome do conjunto de backup padrão sugerido na caixa de texto **Nome** ou digite um nome diferente para o conjunto de backup.  
  
8.  Opcionalmente, na caixa de texto **Descrição** , digite uma descrição do conjunto de backup.  
  
9. Especifique quando o conjunto de backup irá expirar:  
  
    -   Para que o conjunto de backup expire depois de um número específico de dias, clique em **Depois** (a opção padrão) e digite quantos dias depois da criação do conjunto ele deve expirar. Esse valor pode ser de 0 a 99999 dias; 0 dias significa que o conjunto de backup nunca vai expirar.  
  
         O valor padrão é definido na opção **Retenção de mídia de backup padrão (em dias)** da caixa de diálogo **Propriedades do Servidor** (página **Configurações do Banco de Dados** ). Para acessar, clique com o botão direito do mouse no nome do servidor em Pesquisador de Objetos e selecione propriedades. Depois, selecione a página **Configurações de Banco de Dados** .  
  
    -   Para que o conjunto de backup expire em uma data específica, clique no campo **Em** e digite a data de expiração do conjunto.  
  
10. Escolha o tipo do destino de backup clicando em **Disco** ou **Fita**. Para selecionar o caminho de até 64 unidades de disco ou de fita que contém um único conjunto de mídias, clique em **Adicionar**. Os caminhos selecionados são exibidos na caixa de listagem **Backup** .  
  
     Para remover um destino de backup, selecione-o e clique em **Remover**. Para exibir o conteúdo de um destino de backup, selecione-o e clique em **Conteúdo**.  
  
11. Para exibir ou selecionar as opções avançadas, clique em **Opções** no painel **Selecionar uma página** .  
  
12. Selecione uma opção **Substituir Mídia** , com um clique em uma das opções a seguir:  
  
    -   **Fazer backup no conjunto de mídias existente**  
  
         Para essa opção, clique em **Anexar ao conjunto de backup existente** ou **Substituir todos os conjuntos de backup existentes**. Como opção, marque a caixa de verificação **Verificar nome do conjunto de mídias e validade do conjunto de backup** e especifique a caixa de texto do **Nome do conjunto de mídias** . Se nenhum nome for especificado, um conjunto de mídias com um nome em branco será criado. Se você especificar um nome de conjunto de mídias, a mídia (fita ou disco) será verificada para conferir se o nome real corresponde ao nome inserido aqui.  
  
         Se você deixar o nome da mídia em branco e marcar a caixa para verificar a mídia, a verificação terá sucesso se o nome da mídia também estiver em branco na mídia.  
  
    -   **Fazer backup em um novo conjunto de mídias e apagar todos os conjuntos de backup existentes**  
  
         Para essa opção, digite um nome na caixa de texto **Nome do novo conjunto de mídias** e, opcionalmente, descreva o conjunto de mídias na caixa de texto **Descrição do novo conjunto de mídias** .  
  
13. Na seção **Confiabilidade** , como opção, marque:  
  
    -   **Verificar backup quando concluído**  
  
    -   **Executar soma de verificação antes de gravar na mídia** e, como opção, **Continuar com erro da soma de verificação**. Para obter informações sobre somas de verificação, consulte [Possible Media Errors During Backup and Restore &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md) [Possíveis erros de mídia durante backup e restauração (SQL Server)].  
  
14. Se o backup estiver sendo feito em uma unidade de fita (conforme especificado na seção **Destino** da página **Geral** ), a opção **Descarregar a fita após o backup** estará ativa. Clicar nessa opção ativa a opção **Rebobinar a fita antes de descarregar** .  
  
    > [!NOTE]  
    >  As opções na seção **Log de transações** estarão inativos exceto se o backup estiver sendo feito em um log de transações (como especificado na seção **Tipo de backup** da página **Geral** ).  
  
15. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e posteriores dão suporte para [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md). Por padrão, a compactação de um backup depende do valor da opção de configuração de servidor **padrão de compactação de backup**. Porém, independentemente do padrão atual do nível do servidor, é possível compactar um backup, marcando a opção **Compactar backup** e evitar a compactação marcando **Não compactar o backup**.  
  
     **Para exibir o padrão de compactação de backup atual**  
  
    -   [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
    > [!NOTE]  
    >  Como alternativa, é possível usar o Assistente para Plano de Manutenção para criar backups de banco de dados diferenciais.  
  
##  <a name="transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL  
  
#### <a name="create-a-differential-database-backup"></a>Criar um backup diferencial de banco de dados  
  
1.  Execute a instrução BACKUP DATABASE para criar o backup de banco de dados diferencial, especificando:  
  
    -   O nome do banco de dados do qual fazer backup.  
  
    -   O dispositivo de backup em que o backup completo do banco de dados será gravado.  
  
    -   A cláusula DIFFERENTIAL, para especificar que o backup só será feito nas partes do banco de dados que foram alteradas depois da criação do último backup completo.  
  
     A sintaxe necessária é:  
  
     BACKUP DATABASE *database_name* TO <backup_device> WITH DIFFERENTIAL  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Este exemplo cria um backup completo e diferencial de banco de dados para o banco de dados `MyAdvWorks` .  
  
```sql  
-- Create a full database backup first.  
BACKUP DATABASE MyAdvWorks   
   TO MyAdvWorks_1   
   WITH INIT;  
GO  
-- Time elapses.  
-- Create a differential database backup, appending the backup  
-- to the backup device containing the full database backup.  
BACKUP DATABASE MyAdvWorks  
   TO MyAdvWorks_1  
   WITH DIFFERENTIAL;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)   
 [Fazer backup de arquivos e de grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Restaurar um backup de banco de dados diferencial &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)   
 [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Backups completos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)  
  
  
