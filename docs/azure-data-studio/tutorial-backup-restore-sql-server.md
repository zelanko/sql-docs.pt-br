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
ms.date: 11/04/2019
ms.openlocfilehash: bdf3bb3151cfac9f68a9765a2c59232b9fb59f56
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287210"
---
# <a name="backup-and-restore-databases-using-name-sos"></a>Backup e restauração de bancos de dados usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Neste tutorial, você aprenderá a usar o [!INCLUDE[name-sos](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Fazer backup de um banco de dados 
> * Exibir o status do backup do banco de dados
> * Gerar o script usado para executar o backup
> * Restaurar um banco de dados
> * Exibir o status da tarefa de restauração

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial requer o *TutorialDB* do SQL Server. Para criar o banco de dados *TutorialDB*, siga um destes guias de início rápido:

* [Conectar e consultar o SQL Server usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)

Este tutorial requer a conexão com um banco de dados do SQL Server. O Banco de Dados SQL do Azure tem backups automatizados, portanto, o Azure Data Studio não executa o backup e a restauração do Banco de Dados SQL do Azure. Para obter detalhes, confira [Saiba mais sobre backups automáticos do Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).

## <a name="back-up-a-database"></a>Fazer o backup de um banco de dados

1. Abra o painel do banco de dados do TutorialDB (abra a barra lateral **SERVIDORES** (**CTRL+G**), expanda **Bancos de Dados**, clique com o botão direito do mouse em **TutorialDB** e selecione **Gerenciar**).

2. Abra a caixa de diálogo **Fazer backup do banco de dados** (clique em **Backup** no widget **Tarefas**).

   ![Widget de tarefas](./media/tutorial-backup-restore-sql-server/tasks.png)

3. Este tutorial usa as opções de backup padrão, sendo assim, clique em **Backup**.
   ![caixa de diálogo de backup](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Após você clicar em **Backup**, a caixa de diálogo **Fazer backup do banco de dados** desaparece e o processo de backup é iniciado.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>Exibir o status e o script de backup

1. O painel **Histórico de Tarefas** é exibido ou pressione **CTRL+T**.

   ![Histórico de tarefas](./media/tutorial-backup-restore-sql-server/task-history.png)

2. Para exibir o script de backup no editor, clique com o botão direito do mouse em **Backup do banco de dados bem-sucedido** e selecione **Script**.

   ![script de backup](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>Restaurar um banco de dados usando um arquivo de backup

1. Abra a barra lateral **SERVIDORES** (**CTRL+G**), clique com o botão direito do mouse em seu servidor e selecione **Gerenciar**.

2. Abra a caixa de diálogo **Restaurar banco de dados** (clique em **Restaurar** no widget **Tarefas**).

   ![Tarefa de restauração](media/tutorial-backup-restore-sql-server/tasks-restore.png)

3. Selecione **Arquivo de backup** no campo **Restaurar de**.

4. Clique nas reticências (...) no campo **Caminho do arquivo de backup** e selecione o arquivo de backup mais recente do *TutorialDB*.

5. Digite **TutorialDB_Restored** no campo **Banco de dados de destino** na seção **Destino** para restaurar o arquivo de backup para um novo banco de dados. Em seguida, selecione **Restaurar**.

   ![restaurar](./media/tutorial-backup-restore-sql-server/restore.png)

6. Para exibir o status da operação de restauração, pressione **CTRL+T** para abrir o **Histórico de Tarefas**.

   ![restaurar](./media/tutorial-backup-restore-sql-server/task-history-restore.png)