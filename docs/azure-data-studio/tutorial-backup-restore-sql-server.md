---
title: Fazer backup e restaurar um banco de dados
description: Siga este tutorial para saber como fazer backup e restaurar bancos de dados usando o Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: a7d3ca36634e449dd26dfdb0df75f09608d25f51
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283687"
---
# <a name="tutorial-backup-and-restore-databases-using-azure-data-studio"></a>Tutorial: Fazer backup e restaurar bancos de dados usando o Azure Data Studio

Neste tutorial, você aprenderá a usar o Azure Data Studio para:
> [!div class="checklist"]
> * Fazer o backup de um banco de dados 
> * Exibir o status do backup do banco de dados
> * Gerar o script usado para executar o backup
> * Restaurar um banco de dados
> * Exibir o status da tarefa de restauração

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial requer o *TutorialDB* do SQL Server. Para criar o banco de dados *TutorialDB*, siga um destes guias de início rápido:

* [Conectar e consultar o SQL Server usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)

Este tutorial requer a conexão com um banco de dados do SQL Server. O Banco de Dados SQL do Azure tem backups automatizados, portanto, o Azure Data Studio não executa o backup e a restauração do Banco de Dados SQL do Azure. Para obter detalhes, confira [Saiba mais sobre backups automáticos do Banco de Dados SQL](/azure/sql-database/sql-database-automated-backups).

## <a name="back-up-a-database"></a>Fazer o backup de um banco de dados

1. Abra o painel do banco de dados do TutorialDB (abra a barra lateral **SERVIDORES** [**CTRL + G**], expanda **Bancos de Dados**, use o botão direito do mouse para selecionar **TutorialDB** e escolha **Gerenciar**).

2. Abra a caixa de diálogo **Fazer backup do banco de dados** (selecione **Backup** no widget **Tarefas**).

   ![Widget de tarefas](./media/tutorial-backup-restore-sql-server/tasks.png)

3. Este tutorial usa as opções de backup padrão; portanto, selecione **Backup**.
   ![caixa de diálogo de backup](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Após a seleção de **Backup**, a caixa de diálogo **Fazer backup do banco de dados** desaparece e o processo de backup é iniciado.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>Exibir o status e o script de backup

1. O painel **Histórico de Tarefas** é exibido ou pressione **CTRL+T**.

   ![Histórico de tarefas](./media/tutorial-backup-restore-sql-server/task-history.png)

2. Para ver o script de backup no editor, use o botão direito do mouse para selecionar **Backup do banco de dados bem-sucedido** e escolha **Script**.

   ![script de backup](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>Restaurar um banco de dados usando um arquivo de backup

1. Abra a barra lateral **SERVIDORES** (**CTRL + G**), use o botão direito do mouse para selecionar seu servidor e escolha **Gerenciar**.

2. Abra a caixa de diálogo **Restaurar banco de dados** (selecione **Restaurar** no widget **Tarefas**).

   ![Restauração de tarefa](media/tutorial-backup-restore-sql-server/tasks-restore.png)

3. Selecione **Arquivo de backup** no campo **Restaurar de**.

4. Selecione as reticências (...) no campo **Caminho do arquivo de backup** e selecione o arquivo de backup mais recente do *TutorialDB*.

5. Digite **TutorialDB_Restored** no campo **Banco de dados de destino** na seção **Destino** para restaurar o arquivo de backup para um novo banco de dados. Em seguida, selecione **Restaurar**.

   ![Restaurar backup](./media/tutorial-backup-restore-sql-server/restore.png)

6. Para exibir o status da operação de restauração, pressione **CTRL+T** para abrir o **Histórico de Tarefas**.

   ![Restauração de tarefa do histórico](./media/tutorial-backup-restore-sql-server/task-history-restore.png)