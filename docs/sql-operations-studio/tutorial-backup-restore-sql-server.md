---
title: Fazer backup e restaurar um banco de dados usando o Studio de operações do SQL (visualização) | Microsoft Docs
description: Saiba como fazer backup e restaurar um banco de dados usando o Studio de operações do SQL (visualização)
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22a453caa9d29432381da6861a0f0c4e3e61d77e
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582448"
---
# <a name="backup-and-restore-using-includename-sosincludesname-sos-shortmd"></a>Backup e restauração usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Neste tutorial, você aprenderá a usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Fazer backup de um banco de dados 
> * Exibir o status do backup
> * Gerar o script usado para realizar o backup
> * Restaurar um banco de dados
> * Exibir o status da tarefa de restauração

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server *TutorialDB*. Para criar o *TutorialDB* banco de dados, conclua um dos tutoriais a seguir:

- [Conectar e consultar usando o SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)


## <a name="backup-a-database"></a>Fazer backup de um banco de dados

1. Abra o painel de banco de dados TutorialDB (abrir o **servidores** barra lateral (**CTRL + G**), expanda **bancos de dados**, clique com botão direito **TutorialDB**, e selecione **gerenciar**). 

2. Abra o **banco de dados de Backup** caixa de diálogo (clique **Backup** no **tarefas** widget).

   ![Widget de tarefas](./media/tutorial-backup-restore-sql-server/tasks.png)

3. Este tutorial usa as opções de backup padrão, clique em **Backup**.
   ![caixa de diálogo](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Depois de clicar em **Backup**, o **banco de dados de Backup** desaparece da caixa de diálogo e começa o processo de backup.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>Exibir o status do backup e exibir o script de backup

1. Abra o **histórico de tarefa** barra lateral clicando no ícone de relógio no *barra de ação* ou pressione **CTRL + T**.

   ![Histórico de tarefas](./media/tutorial-backup-restore-sql-server/task-history.png)

2. Para exibir o script de backup no editor, clique com botão direito **Backup de banco de dados bem-sucedida** e selecione **Script**.

   ![script de backup](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>Restaurar um banco de dados de um arquivo de backup


1. Abra o **servidores** barra lateral (**CTRL + G**), o servidor e selecione **gerenciar**. 

2. Abra o **restaurar banco de dados** caixa de diálogo (clique **restaurar** no **tarefas** widget).

2. Selecione **arquivo de Backup** no **restaurar de** campo. 

3. Clique nas reticências (...) no **caminho do arquivo de Backup** campo e selecione o arquivo de backup mais recente para *TutorialDB*.

3. Tipo **TutorialDB_Restored** no **banco de dados de destino** campo o **destino** seção para restaurar o arquivo de backup para um novo banco de dados.

   ![restaurar](./media/tutorial-backup-restore-sql-server/restore.png)

4. Clique em **restaurar**

5. Para exibir o status da operação de restauração, pressione **CTRL + T** para abrir o **histórico de tarefa** barra lateral.

   ![restaurar](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Fazer backup de um banco de dados 
> * Exibir o status do backup
> * Gerar o script usado para realizar o backup
> * Restaurar um banco de dados
> * Exibir o status da tarefa de restauração

