---
title: Fazendo backup e restaurando bancos de dados do DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3091f62-2234-4a80-a615-cf14c2a1da85
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 50b051cf2780fc1a94830c461d9ae30674bb7dad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481150"
---
# <a name="backing-up-and-restoring-dqs-databases"></a>Fazendo backup e restaurando banco de dados do DQS
  Este tópico descreve como fazer backup e restaurar os bancos de dados do DQS.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve saber ou se lembrar da senha da chave mestra do banco de dados que forneceu durante a instalação do servidor DQS.  
  
-   Verifique se não há nenhuma atividade ou processo em execução no DQS. Isso pode ser verificado com o uso da tela **Monitoramento de atividade** . Para obter informações detalhadas sobre como trabalhar nessa tela, consulte [Monitor DQS Activities](../../2014/data-quality-services/monitor-dqs-activities.md).  
  
-   Verifique se não há usuários conectados no servidor DQS.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
  
-   Sua conta de usuário do Windows deve ser um membro da função de servidor fixa sysadmin na instância do SQL Server para executar as operações de backup e restauração.  
  
-   Você deve ter a função dqs_administrator no banco de dados DQS_MAIN para terminar as atividades em execução ou interromper os processos em execução no DQS.  
  
##  <a name="BackupRestore"></a> Backup e restauração de bancos de dados do DQS  
  
1.  Inicie o Microsoft SQL Server Management Studio e conecte-se à instância apropriada do SQL Server.  
  
2.  No Pesquisador de Objetos, expanda o nó **Bancos de Dados** .  
  
3.  Faça um backup do banco de dados DQS_STAGING_DATA. Para obter instruções passo a passo de como fazer backup de um banco de dados do SQL Server, consulte [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
4.  Faça backup do banco de dados DQS_PROJECTS.  
  
5.  Faça backup do banco de dados DQS_MAIN.  
  
6.  Desconecte-se da instância atual do SQL Server e conecte-se à instância do SQL Server em que você deseja restaurar esses bancos de dados.  
  
7.  Restaure o banco de dados DQS_MAIN. Para obter instruções passo a passo restaurar um banco de dados do SQL Server, consulte [restaurar um Backup de banco de dados &#40;SQL Server Management Studio&#41;](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).  
  
8.  Restaure o banco de dados DQS_PROJECTS.  
  
9. Restaure o banco de dados DQS_STAGING_DATA.  
  
10. No Pesquisador de Objetos, clique com o botão direito do mouse no servidor e, depois, clique em **Nova Consulta**.  
  
11. Na janela Editor de Consultas, copie as seguintes instruções SQL e substitua *\<PASSWORD>* pela senha fornecida durante a instalação do DQS para a chave mestra do banco de dados:  
  
    ```  
    USE [DQS_MAIN]  
    GO  
    EXECUTE [internal_core].[RestoreDQDatabases] '<PASSWORD>'  
    GO  
  
    ```  
  
12. Pressione F5 para executar as instruções. Consulte o painel **Resultados** para verificar se as instruções foram executadas com êxito.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar bancos de dados do DQS](../../2014/data-quality-services/manage-dqs-databases.md)  
  
  
