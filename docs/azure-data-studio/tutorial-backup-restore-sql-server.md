---
title: Backup e restauração de um banco de dados
titleSuffix: Azure Data Studio
description: Saiba como fazer backup e restauração de um banco de dados usando o Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 77679106577cd8f8374f932d8ddd22644beb63d8
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959108"
---
# <a name="backup-and-restore-databases-using-includename-sosincludesname-sos-shortmd"></a>Backup e restauração de bancos de dados usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Neste tutorial, você aprenderá a usar o [!INCLUDE[name-sos](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Fazer backup de um banco de dados 
> * Exibir o status do backup do banco de dados
> * Gerar o script usado para executar o backup
> * Restaurar um banco de dados
> * Exibir o status da tarefa de restauração

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o *TutorialDB* do SQL Server. Para criar o banco de dados *TutorialDB*, siga um destes guias de início rápido:

- [Conectar e consultar o SQL Server usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)

Este tutorial requer a conexão com um banco de dados do SQL Server. O Banco de Dados SQL do Azure tem backups automatizados, portanto o Azure Data Studio não executa o backup e restauração do Banco de Dados SQL do Azure. Para obter detalhes, confira [Saiba mais sobre backups automáticos do Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).

## <a name="backup-a-database"></a>Fazer backup de um banco de dados

1. Abra o painel do banco de dados do TutorialDB (abra a barra lateral **SERVIDORES** (**CTRL+G**), expanda **Bancos de Dados**, clique com o botão direito do mouse em **TutorialDB** e selecione **Gerenciar**).

2. Abra a caixa de diálogo **Fazer backup do banco de dados** (clique em **Backup** no widget **Tarefas**).

   ![Widget de tarefas](./media/tutorial-backup-restore-sql-server/tasks.png)

3. Este tutorial usa as opções de backup padrão, sendo assim, clique em **Backup**.
   ![caixa de diálogo de backup](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Após você clicar em **Backup**, a caixa de diálogo **Fazer backup do banco de dados** desaparece e o processo de backup é iniciado.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>Exibir o status e o script de backup

1. Abra a barra lateral **Histórico de Tarefas** clicando no ícone de relógio na *Barra de ação* ou pressione **CTRL+T**.

   ![Histórico de tarefas](./media/tutorial-backup-restore-sql-server/task-history.png)

2. Para exibir o script de backup no editor, clique com o botão direito do mouse em **Backup do banco de dados bem-sucedido** e selecione **Script**.

   ![script de backup](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>Restaurar um banco de dados usando um arquivo de backup


1. Abra a barra lateral **SERVIDORES** (**CTRL+G**), clique com o botão direito do mouse em seu servidor e selecione **Gerenciar**. 

2. Abra a caixa de diálogo **Restaurar banco de dados** (clique em **Restaurar** no widget **Tarefas**).

2. Selecione **Arquivo de backup** no campo **Restaurar de**. 

3. Clique nas reticências (...) no campo **Caminho do arquivo de backup** e selecione o arquivo de backup mais recente do *TutorialDB*.

3. Digite **TutorialDB_Restored** no campo **Banco de dados de destino** na seção **Destino** para restaurar o arquivo de backup para um novo banco de dados.

   ![restaurar](./media/tutorial-backup-restore-sql-server/restore.png)

4. Clique em **Restaurar**

5. Para exibir o status da operação de restauração, pressione **CTRL + T** para abrir a barra lateral **Histórico de Tarefas**.

   ![restaurar](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> * Fazer backup de um banco de dados 
> * Exibir o status do backup do banco de dados
> * Gerar o script usado para executar o backup
> * Restaurar um banco de dados
> * Exibir o status da tarefa de restauração

