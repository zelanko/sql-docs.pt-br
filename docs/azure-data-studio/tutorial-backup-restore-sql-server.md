---
title: Fazer backup e restaurar um banco de dados
description: Siga este tutorial para saber como fazer backup de bancos de dados e restaurá-los usando o Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 808dec10c92bffe66122bfa9a55d7db1cc64f62e
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364166"
---
# <a name="tutorial-back-up-and-restore-databases-using-azure-data-studio"></a>Tutorial: Fazer backup de bancos de dados e restaurá-los usando o Azure Data Studio

Neste tutorial, você aprenderá a usar o Azure Data Studio para:
> [!div class="checklist"]
> * Fazer backup de um banco de dados.
> * Exibir o status do backup.
> * Gerar o script usado para executar o backup.
> * Restaurar um banco de dados.
> * Exibir o status da tarefa de restauração.

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial requer o *TutorialDB* do SQL Server. Para criar o banco de dados TutorialDB, siga o seguinte guia de início rápido:

* [Usar o Azure Data Studio para conectar e consultar o SQL Server](quickstart-sql-server.md)

Esse tutorial requer uma conexão com um banco de dados do SQL Server. O Banco de Dados SQL do Azure tem backups automatizados, portanto, o Azure Data Studio não executa o backup e a restauração do Banco de Dados SQL do Azure. Para obter mais informações, consulte [Saiba mais sobre os backups automáticos do Banco de Dados SQL](/azure/sql-database/sql-database-automated-backups).

## <a name="back-up-a-database"></a>Fazer o backup de um banco de dados

1. Abra painel do banco de dados TutorialDB abrindo a barra lateral **SERVERS**. Em seguida, selecione **CTRL+G**, expanda **Bancos de Dados**, clique com o botão direito do mouse em **TutorialDB** e selecione **Gerenciar**.

1. Abra a caixa de diálogo **Fazer backup do banco de dados** selecionando **Backup** no widget **Tarefas**.

   ![Captura de tela que mostra o widget Tarefas.](./media/tutorial-backup-restore-sql-server/tasks.png)

1. Este tutorial usa as opções de backup padrão; portanto, selecione **Backup**.

   ![Captura de tela que mostra a caixa de diálogo Backup.](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Depois que você selecionar **Backup**, a caixa de diálogo **Fazer backup do banco de dados** desaparece e o processo de backup é iniciado.

## <a name="view-the-backup-status-and-the-backup-script"></a>Exibir o status e o script de backup

1. O painel **Histórico de Tarefas** é exibido ou pressione **CTRL+T** para abri-lo.

   ![Captura de tela que mostra o painel Histórico de Tarefas.](./media/tutorial-backup-restore-sql-server/task-history.png)

1. Para exibir o script de backup no editor, clique com o botão direito do mouse em **Backup do banco de dados bem-sucedido** e selecione **Script**.

   ![Captura de tela que mostra o script de backup.](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>Restaurar um banco de dados usando um arquivo de backup

1. Abra a barra lateral **SERIDORES** selecionando **CTRL+G**. Em seguida, clique com o botão direito do mouse no servidor e selecione **Gerenciar**.

1. Abra a caixa de diálogo **Restaurar banco de dados** selecionando **Restaurar** no widget **Tarefas**.

   ![Captura de tela que mostra a Restauração da tarefa.](media/tutorial-backup-restore-sql-server/tasks-restore.png)

1. Selecione **Arquivo de backup** na caixa **Restaurar de**.

1. Selecione as reticências (...) na caixa **Caminho do arquivo de backup** e selecione o arquivo de backup mais recente do *TutorialDB*.

1. Insira **TutorialDB_Restored** na caixa **Banco de dados de destino** na seção **Destino** para restaurar o arquivo de backup para um novo banco de dados. Em seguida, selecione **Restaurar**.

   ![Captura de tela que mostra Restaurar backup.](./media/tutorial-backup-restore-sql-server/restore.png)

1. Para exibir o status da operação de restauração, selecione **CTRL+T** para abrir o **Histórico de Tarefas**.

   ![Captura de tela que mostra a Restauração da tarefa de histórico.](./media/tutorial-backup-restore-sql-server/task-history-restore.png)