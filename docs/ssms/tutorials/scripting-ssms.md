---
title: 'Tutorial: gerar script de objetos no SQL Server Management Studio'
description: Um tutorial para gerar scripts de objetos no SSMS
keywords: SQL Server, SSMS, SQL Server Management Studio, Scripts, Gerar script
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: d4bf028163905763ae87f04e03c0a95ddf4abcaf
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263358"
---
# <a name="script-objects-in-sql-server-management-studio"></a>gerar script de objetos no SQL Server Management Studio

Este tutorial ensina a gerar scripts T-SQL (Transact-SQL) para vários objetos encontrados no SQL Server Management Studio (SSMS). Neste tutorial, você encontra exemplos de como gerar script para os seguintes objetos:

> [!div class="checklist"]
> * Consultas ao executar ações na GUI
> * Bancos de dados de duas maneiras diferentes (Escrever Script como e Gerar Script)
> * Tabelas
> * Procedimentos armazenados
> * Eventos estendidos

Para gerar script de qualquer objeto no **Pesquisador de Objetos**, clique duas vezes e selecione a opção **Gerar script de objeto como**. Este tutorial mostra o processo.

## <a name="prerequisites"></a>Prerequisites

Para concluir este tutorial, você precisará do SQL Server Management Studio, bem como acesso a um servidor que executa o SQL Server e um banco de dados do AdventureWorks.

* Instalar o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
* Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
* Baixar [Bancos de dados de exemplo do AdventureWorks2016](https://github.com/Microsoft/sql-server-samples/releases).

Instruções para restaurar bancos de dados no SSMS são encontradas aqui: [Restaurar um banco de dados](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 

## <a name="script-queries-from-the-gui"></a>Gerar script de consultas da GUI

Você pode gerar o código T-SQL associado para uma tarefa sempre que você usa a GUI no SSMS para concluí-la. Os exemplos a seguir mostram como fazer isso ao fazer backup de um banco de dados e reduzir o log de transações. Essas mesmas etapas podem ser aplicadas a qualquer ação que é concluída por meio da GUI.

### <a name="script-t-sql-when-you-back-up-a-database"></a>Gerar script de T-SQL ao fazer backup de um banco de dados

1. Conecte-se a um servidor que executa o SQL Server.

2. Expanda o nó **Bancos de Dados** .

3. Clique com o botão direito do mouse no banco de dados do **Adventureworks2016** > **Tarefas** > **Backup**:

    ![Fazer o backup de um banco de dados](media/scripting-ssms/backupdb.png)

4. Configure o backup como desejar. Para este tutorial, tudo foi deixado nos valores padrão. Entretanto, as alterações feitas na janela também serão refletidas no script. 

5. Selecione **Script** > **Ação do Script para a Nova Janela de Consulta**:

    ![Gerar backup de banco de dados de script – ação de script](media/scripting-ssms/scriptdbbackup.PNG)
6. Examine o T-SQL populado na janela de consulta.

    ![Gerar backup de banco de dados de script – revisar T-SQL](media/scripting-ssms/dbbackupscript.PNG)
7. Selecione **Executar** para executar a consulta para fazer backup do banco de dados por meio do T-SQL. 

### <a name="script-t-sql-when-you-shrink-the-transaction-log"></a>Gerar script de T-SQL ao reduzir o log de transações

1. Clique com o botão direito do mouse no banco de dados do **AdventureWorks2016TasksShrinkFiles** > **Tarefas** > **Reduzir** > **Arquivos**:

     ![Reduzir arquivos](media/scripting-ssms/shrinkfiles.png)

2. Selecione **Log** da caixa de listagem suspensa **Tipo de arquivo**:

    ![Reduzir o log de transações](media/scripting-ssms/shrinktlog.png)

3. Selecione **Gerar script** e **Gerar script de ação para área de transferência**:

    ![Script para área de transferência](media/scripting-ssms/scriptactiontoclipboard.png)

4. Abra uma janela **Nova Consulta** e cole. (Clique com o botão direito do mouse na janela. Selecione **Colar**).

    ![Colar script](media/scripting-ssms/paste.png)

5. Selecione **Executar** para executar a consulta e reduzir o log de transações.

## <a name="script-databases"></a>Gerar script de bancos de dados

A seção a seguir ensina como gerar o script do banco de dados, tanto usando a opção **Escrever script como** quanto a **Gerar Scripts**. A opção **Escrever script como** recria o banco de dados e suas opções de configuração. Você pode escrever script do esquema e dos dados usando a opção **Gerar Scripts**. Nesta seção, você cria dois novos bancos de dados. Você usa a opção **Script como** para criar *AdventureWorks2016a*. Você usa a opção **Gerar Scripts** para criar *AdventureWorks2016b*.

### <a name="script-a-database-by-using-the-script-option"></a>Escrever script de um banco de dados usando a opção Script

1. Conecte-se a um servidor que executa o SQL Server.

2. Expanda o nó **Bancos de Dados** .

3. Clique com o botão direito do mouse no banco de dados do **AdventureWorks2016** > **Gerar script de banco de dados como** > **Criar para** > **Janela do Editor de Nova Consulta**:

    ![Gerar script de banco de dados](media/scripting-ssms/scriptdb.png)

4. Revise a consulta de criação de banco de dados na janela:

    ![Banco de dados gerado por script](media/scripting-ssms/scriptedoutdb.png) Essa opção gera scripts apenas das opções de configuração do banco de dados.

5. No teclado, selecione Ctrl + F para abrir a caixa de diálogo **Localizar**. Selecione a seta para baixo para abrir a opção **Substituir**. Na linha superior **Localizar**, digite AdventureWorks2016; na linha inferior **Substituir**, digite AdventureWorks2016a.

6. Clique em **Substituir tudo** para substituir todas as instâncias do *AdventureWorks2016* pelo *AdventureWorks2016a*. 

    ![Localizar e substituir](media/scripting-ssms/findandreplace.png)

7. Clique em **Executar** para executar a consulta e crie o novo banco de dados AdventureWorks2016a. 

### <a name="script-a-database-by-using-the-generate-scripts-option"></a>Escrever script de um banco de dados usando a opção Gerar Scripts

1. Conecte-se a um servidor que executa o SQL Server.

2. Expanda o nó **Bancos de Dados** .

3. Clique com botão direito **AdventureWorks2016** > **Tarefas** > **Gerar Scripts**:

    ![Gerar scripts para banco de dados](media/scripting-ssms/generatescriptsfordb.png)

4. A página **Introdução** é aberta. Selecione **Avançar** para abrir a página **Escolher Objetos**. Você pode selecionar o banco de dados inteiro ou objetos específicos no banco de dados. Selecione **Gerar script de todo o banco de dados e todos os objetos de banco de dados**.

    ![Gerar scripts para objetos](media/scripting-ssms/scriptobjects.png)

5. Selecione **Avançar** para abrir a página **Definir Opções de Script**. Aqui você pode configurar onde salvar o script e outras opções avançadas. 

    A. Selecione **Salvar em nova janela de consulta**.

    B. Clique em **Avançado** e certifique-se de que estas opções estejam definidas:

      * **Estatísticas do Script** definida como *Estatísticas do Script*.
      * **Tipos de dados para script** definida como *Somente esquema*.
      * **Índices do Script** definida como *true*.

   ![Objetos de script](media/scripting-ssms/advancedscripts.png)

   > [!NOTE]
   > Você pode gerar scripts dos dados do banco de dados ao selecionar *Esquema e dados* na opção **Tipos de dados dos quais gerar script**. No entanto, isso não é ideal com grandes bancos de dados. Pode consumir mais memória do que o SSMS pode alocar. Essa limitação pode ser usada para bancos de dados pequenos. Se você quiser mover dados para um banco de dados maior, use o [Assistente de importação e exportação](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).

6. Selecione **OK**e selecione **Avançar**.

7. Selecione **Avançar** no **Resumo**. Selecione **Avançar** novamente para gerar o script em uma janela **Nova Consulta**.

8. No teclado, abra a caixa de diálogo **Localizar** (Ctrl + F). Selecione a seta para baixo para abrir a opção **Substituir**. Na linha superior de **Localizar**, digite *AdventureWorks2016*. Na linha inferior de **Substituir**, digite *AdventureWorks2016b*.

9. Clique em **Substituir tudo** para substituir todas as instâncias do *AdventureWorks2016* pelo *AdventureWorks2016b*.

    ![AdventureWorks2016b](media/scripting-ssms/adventureworks2016b.png)

10. Clique em **Executar** para executar a consulta e criar o novo banco de dados AdventureWorks2016b.

## <a name="script-tables"></a>Gerar script de tabelas

Esta seção aborda como gerar o script de tabelas do banco de dados. Use essa opção para criar a tabela ou soltá-la e criá-la. Também é possível usar essa opção para gerar scripts do T-SQL associado com a modificação da tabela. Um exemplo é inserir nele ou atualizá-lo. Nesta seção, você solta uma tabela e, em seguida, a recria. 

1. Conecte-se a um servidor que executa o SQL Server.

2. Expanda o nó **Bancos de Dados**.

3. Expanda o nó **AdventureWorks2016** do banco de dados. 

4. Expanda o nó **Tabelas**.

5. Clique com o botão direito do mouse em **dbo.ErrorLog** > **Gerar script da tabela como** > **Soltar e criar em** > **Nova janela de edição de consultas**:

    ![Gerar script de tabela](media/scripting-ssms/scripttable.png)

6. Selecione **Executar** para executar a consulta. Esta ação cancela a tabela *Errorlog* e a recria. 

    >[!NOTE]
    > A tabela *Errorlog* está vazia por padrão no banco de dados AdventureWorks2016. Portanto, você não está perdendo dados pela remoção da tabela. No entanto, seguir estas etapas em uma tabela com os dados causará a perda deles.

## <a name="script-stored-procedures"></a>Gerar script de procedimentos armazenados

Nesta seção, você aprenderá a soltar e criar um procedimento armazenado.  

1. Conecte-se a um servidor que executa o SQL Server.

2. Expanda o nó **Bancos de Dados**.

3. Expanda o nó **Programação**. 

4. Expanda o nó **Procedimento Armazenado**.

5. Clique com o botão direito do mouse no procedimento armazenado **dbo.uspGetBillOfMaterials** > **Gerar script de procedimento armazenado como** > **Soltar e criar para** > **Janela do Editor de Nova Consulta**:

    ![Gerar script de procedimentos armazenados](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>Gerar script de eventos estendidos

Esta seção aborda como gerar o script de [eventos estendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events).

1. Conecte-se a um servidor que executa o SQL Server.

2. Expanda o nó **Gerenciamento**.

3. Expanda o nó **Eventos Estendidos**.

4. Expanda o nó **Sessões**.

5. Clique com o botão direito do mouse na sessão estendida de seu interesse em > **Criar script de sessão como** > **Nova janela de edição de consulta**:

    ![Sessão estendida da Janela do Editor de Nova Consulta](media/scripting-ssms/scriptxevents.png)

6. Na **Janela do Editor de Nova Consulta**, modifique o novo nome da sessão de *system_health* para *system_health2*. Selecione **Executar** para executar a consulta.

7. Clique com o botão direito do mouse em **Sessões** no **Pesquisador de Objetos**. Selecione **Atualizar** para ver a nova sessão de evento estendido. O ícone verde ao lado da sessão indica que a sessão está em execução. O ícone vermelho indica que a sessão está interrompida.

    ![Nova sessão de eventos estendidos](media/scripting-ssms/newxevent.png)

    >[!NOTE]
    > É possível iniciar a sessão clicando com o botão direito do mouse e selecionando **Iniciar**. No entanto, essa é uma cópia da sessão **system_health** que já está em execução, então esta etapa pode ser ignorada. Você pode excluir a cópia da sessão de evento estendido clicando com o botão direito do mouse e selecionando **Excluir**.

## <a name="next-steps"></a>Próximas etapas

O melhor modo de se familiarizar com o SSMS é praticando. Estes artigos com *tutoriais* e *instruções* ajudam nos diversos recursos disponíveis no SSMS. Estes artigos ensinam a administrar os componentes do SSMS e a encontrar os recursos que você usa com regularidade.

* [Conectar-se e consultar uma instância](connect-query-sql-server.md)
* [Usando modelos no SSMS](../template/templates-ssms.md)
* [Configuração do SSMS](ssms-configuration.md)
* [Mais dicas e truques para usar o SSMS](ssms-tricks.md)