---
Title: 'Tutorial: Script Objects in SQL Server Management Studio'
description: Um Tutorial para gerar scripts de objetos no SSMS.
keywords: SQL Server, SSMS, SQL Server Management Studio, Scripts, Gerar script
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: a931ddb3cf3229970de4b301e18002484acbaf53
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-script-objects-in-sql-server-management-studio"></a>Tutorial: gerar script de objetos no SQL Server Management Studio
Este tutorial ensinará como gerar scripts T-SQL (Transact-SQL) para vários objetos encontrados no SQL Server Management Studio.  Neste tutorial, você encontrará exemplos de como gerar script para os seguintes objetos: 

> [!div class="checklist"]
> * Consultas ao executar ações na GUI
> * Bancos de dados de duas maneiras diferentes (“Escrever script como” e “Gerar Script”)
> * Tabelas
> * Procedimentos armazenados
> * Eventos estendidos

O resumo deste tutorial indica que é possível gerar o script de qualquer objeto no **Pesquisador de Objetos** clicando com o botão direito do mouse nele e selecionando a opção **Gerar script de objeto como**. 


## <a name="prerequisites"></a>Prerequisites
Para concluir este Tutorial, você precisará do SQL Server Management Studio, bem como acesso a um SQL Server e um banco de dados do AdventureWorks. 

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Baixar [Bancos de dados de exemplo do AdventureWorks2016](https://github.com/Microsoft/sql-server-samples/releases). As instruções para restaurar bancos de dados no SSMS podem ser encontradas aqui: [Restaurando um banco de dados](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 


## <a name="script-queries-from-gui"></a>Gerar script de consultas da GUI
Sempre que você executar uma tarefa usando a GUI no SSMS, também será possível gerar o código T-SQL associado à tarefa. Os exemplos a seguir mostram como fazer isso ao fazer um backup de um banco de dados e reduzir o log de transações.  Essas mesmas etapas podem ser aplicadas a qualquer ação que é concluída por meio da GUI. 

### <a name="script-t-sql-when-backing-up-a-database"></a>Gerar script de T-SQL ao fazer backup de um banco de dados
1. Conecte-se ao SQL Server.
2. Expanda o nó **Bancos de Dados** .
3. Clique com o botão direito do mouse no banco de dados do **Adventureworks2016** > **Tarefas** > **Fazer backup**:

    ![Fazer backup do banco de dados](media/scripting-ssms/backupdb.png)

4. Configure o backup como desejar. Para a finalidade deste Tutorial, tudo foi deixado nos valores padrão. Entretanto, as alterações feitas na janela também serão refletidas no script. 
5. Clique na opção para **Gerar script** > **Gerar script de ação para a janela de consulta**:
 
    ![Gerar script de backup de BD](media/scripting-ssms/scriptdbbackup.PNG)
6. Examine o T-SQL populado na janela de consulta: 

    ![Gerar script para backup de BD](media/scripting-ssms/dbbackupscript.PNG)
7. Selecione **Executar** para executar a consulta para fazer backup do banco de dados por meio do T-SQL. 


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>Gerar script de T-SQL ao reduzir o log de transações
1. Clique com o botão direito do mouse no banco de dados do **AdventureWorks2016** > **Tarefas** > **Reduzir** > **Arquivos**:

     ![Reduzir Arquivos](media/scripting-ssms/shrinkfiles.png)

2. Selecione **Log** na lista suspensa **Tipo de Arquivo**:

    ![Reduzir o Log de Transações](media/scripting-ssms/shrinktlog.png)

3. Clique na opção **Gerar script** e **Gerar script de ação para área de transferência**:

    ![Script para Área de Transferência](media/scripting-ssms/scriptactiontoclipboard.png)

4. Abra uma janela **Nova Consulta** e cole (clique com o botão direito do mouse na janela > **Colar**):

    ![Excluir Script](media/scripting-ssms/paste.png)
5. Selecione **Executar** para executar a consulta e reduzir o log de transações. 


## <a name="script-databases"></a>Gerar script de bancos de dados
A seção a seguir ensina como gerar o script do banco de dados, tanto usando a opção **Escrever script como** quanto a **Gerar Scripts**.  A opção **Escrever script como** recriará o banco de dados e as opções de configuração para ele. A opção **Gerar scripts** permitirá que você gere scripts do esquema e dos dados. Nesta seção, você criará dois novos bancos de dados, o *AdventureWorks2016a* será criado com a opção **Escrever script como**. O *AdventureWorks2016b* será criado com a opção **Gerar scripts**. 


### <a name="script-database-using-script-option"></a>Script de banco de dados usando a opção Criar script
1. Conecte-se ao SQL Server.
2. Expanda o nó **Bancos de Dados** .
3. Clique com o botão direito do mouse no banco de dados do **AdventureWorks2016** > **Gerar script de banco de dados como** > **Criar para** > **Nova janela de consulta**:

    ![Criar script de BD](media/scripting-ssms/scriptdb.png)

4. Revise a consulta de criação de banco de dados na janela: 

    ![Script de BD gerado](media/scripting-ssms/scriptedoutdb.png)
    - Essa opção só criará as opções de configuração do banco de dados.
5. No teclado, pressione **Ctrl + F** para abrir a caixa de diálogo **Localizar** e pressione a seta para baixo para abrir a opção **Substituir**. Na linha superior **Localizar**, digite *AdventureWorks2016*; na linha inferior **Substituir**, digite *AdventureWorks2016a*. 
6. Clique em **Substituir tudo** para substituir todas as instâncias do *AdventureWorks2016* pelo *AdventureWorks2016a*. 

    ![Localizar e Substituir](media/scripting-ssms/findandreplace.png)

1. Clique em **Executar** para executar a consulta e crie o novo banco de dados *AdventureWorks2016a*. 

### <a name="script-database-using-generate-scripts-option"></a>Script de banco de dados usando a opção de Gerar Scripts
1. Conecte-se ao SQL Server.
2. Expanda o nó **Bancos de Dados** .
3. Clique com o botão direito do mouse no banco de dados do **AdventureWorks2016** > **Tarefas** > **Gerar scripts**:

    ![Gerar scripts para BD](media/scripting-ssms/generatescriptsfordb.png)

4. A página **Introdução** será aberta. Selecione **Próximo** para abrir a página **Objetos escolhidos**. Você tem a opção de selecionar o banco de dados inteiro ou objetos específicos no banco de dados. Selecione a opção **Gerar script de todo o banco de dados e todos os objetos de banco de dados** 
 
    ![Gerar scripts para objetos](media/scripting-ssms/scriptobjects.png)
 
5. Clique em **Próximo** para abrir a página **Definir Opções de Script**, na qual é possível configurar onde salvar o script, bem como algumas opções avançadas. 

    A. Selecione a opção de **Salvar em nova janela de consulta**. 

    B. Clique em **Avançado** e certifique-se de que estas opções estejam definidas: 

      - **Estatísticas do Script** definida como *Estatísticas do Script*
      - **Tipos de dados para script** definida como *Somente esquema*
      - **Índices do Script** definida como *true*

   ![Objetos de script](media/scripting-ssms/advancedscripts.png)

   > [!NOTE]
   > Você pode gerar scripts dos dados do banco de dados ao selecionar *Esquema e dados* na opção **Tipos de dados dos quais gerar script**. No entanto, isso não é o ideal em bancos de dados grandes, pois pode ocupar mais memória do que o SSMS consegue alocar. Isso pode ser feito em bancos de dados menores, mas se você quiser mover dados para um banco de dados maior, precisará usar o [Assistente de Importação e Exportação](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).



1. Clique em **OK** e em **Próximo**. 
2. Clique em **Próximo** no **Resumo** e, em seguida, clique em **Próximo** novamente para gerar o script para uma **Nova janela de consulta**.  
3. No teclado, pressione **Ctrl + F** para abrir a caixa de diálogo **Localizar** e pressione a seta para baixo para abrir a opção **Substituir**. Na linha superior **Localizar**, digite *AdventureWorks2016*; na linha inferior **Substituir**, digite *AdventureWorks2016b*. 
    A. Clique em **Substituir tudo** para substituir todas as instâncias do *AdventureWorks2016* pelo *AdventureWorks2016b*. 

    ![AdventureWorks2016b](media/scripting-ssms/adventureworks2016b.png)
7. Clique em **Executar** para executar a consulta e criar o novo banco de dados *AdventureWorks2016b*. 
 
## <a name="script-tables"></a>Gerar script de tabelas
Esta seção aborda como gerar o script de tabelas do banco de dados. Usando essa opção, você pode criar a tabela ou soltá-la e criá-la. Também é possível usar essa opção para gerar scripts do T-SQL associado com a modificação da tabela, como inserções ou atualizações dela. Nesta seção, você soltará uma tabela e, em seguida, a recriará. 

1. Conecte-se ao SQL Server.
2. Expanda o nó **Bancos de Dados**.
3. Expanda o nó **AdventureWorks** do banco de dados. 
4. Expanda o nó **Tabelas**.
5. Clique com o botão direito do mouse em **dbo.ErrorLog** >  **Gerar script da tabela como** > **Soltar e criar em** > **Nova janela de edição de consultas**:
    
    ![Tabela de script](media/scripting-ssms/scripttable.png)

6. Selecione **Executar** para executar a consulta – isso removerá a tabela *Errorlog* e a recriará. 

    >[!NOTE]
    > A tabela *Errorlog* está vazia por padrão no banco de dados AdventureWorks2016, então você não perderá dados ao soltá-la. No entanto, seguir essas etapas em uma tabela com os dados causará a perda deles. 
 
## <a name="script-stored-procedures"></a>Gerar script de procedimentos armazenados
Nesta seção, você aprenderá a soltar e criar um procedimento armazenado.  

1. Conecte-se ao SQL Server.
2. Expanda o nó **Bancos de Dados**.
3. Expanda o nó **Programação**. 
4. Expanda o nó **Procedimento Armazenado**.
5. Clique com o botão direito do mouse no procedimento armazenado **dbo.uspGetBillOfMaterials**> **Gerar script de procedimento armazenado como** > **Soltar e criar para** > **Nova janela de consulta**:
    
    ![Gerar script de procedimentos armazenados](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>Gerar script de eventos estendidos
Esta seção aborda como gerar o script de [eventos estendidos](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events). 

1. Conecte-se ao SQL Server.
2. Expanda o nó **Gerenciamento**.
3. Expanda o nó **Eventos Estendidos**.
4. Expanda o nó **Sessões**.
5. Clique com o botão direito do mouse na sessão estendida de seu interesse em > **Criar script de sessão como** > **Nova janela de edição de consulta**:

    ![Gerar script de xEvents](media/scripting-ssms/scriptxevents.png) 
6. Na **Nova janela de consulta**, modifique o novo nome da sessão de *system_health* para *system_health2* e clique em **Executar** para executar a consulta. 

    A. Clique com o botão direito do mouse em **Sessões**, no **Pesquisador de Objetos**, e selecione **Atualizar** para ver a nova Sessão de Eventos Estendido. O ícone verde ao lado da sessão indica que ela está em execução, enquanto o ícone vermelho indica que a sessão está parada. 

    ![Novo xEvent](media/scripting-ssms/newxevent.png)

    >[!NOTE]
    > É possível iniciar a sessão clicando com o botão direito do mouse e selecionando **Iniciar**. No entanto, como essa é uma cópia da sessão *system_health* que já está em execução, esta etapa pode ser ignorada. Você pode excluir a cópia da sessão de evento estendido clicando com o botão direito do mouse e selecionando **Excluir**. 

## <a name="next-steps"></a>Próximas etapas
O próximo artigo apresentará os modelos predefinidos do T-SQL encontrados no SSMS. 

Prossiga para o próximo artigo para saber mais:
> [!div class="nextstepaction"]
> [Próximas etapas](templates-ssms.md)


