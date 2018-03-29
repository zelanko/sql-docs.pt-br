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
ms.openlocfilehash: bc20cc573c6b0890e5b16f4876636534f9fbb916
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
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
- Baixar [Bancos de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). As instruções para restaurar bancos de dados no SSMS podem ser encontradas aqui: [Restaurando um banco de dados](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 


## <a name="script-queries-from-gui"></a>Gerar script de consultas da GUI
Sempre que você executar uma tarefa usando a GUI no SSMS, também será possível gerar o código T-SQL associado à tarefa. Os exemplos a seguir mostram como fazer isso ao fazer um backup de um banco de dados e reduzir o log de transações.  Essas mesmas etapas podem ser aplicadas a qualquer ação que é concluída por meio da GUI. 

### <a name="script-t-sql-when-backing-up-a-database"></a>Gerar script de T-SQL ao fazer backup de um banco de dados
1. Conecte-se ao SQL Server.
2. Expanda o nó **Bancos de Dados** .
3. Clique com o botão direito do mouse no banco de dados > **Tarefas** > **Fazer backup**:

    ![Fazer backup do banco de dados](media/scripting-ssms/backupdb.png)

4. Configure o backup como desejar. Para a finalidade deste Tutorial, tudo foi deixado nos valores padrão. Entretanto, as alterações feitas na janela também serão refletidas no script. 
5. Clique na opção para **Gerar script** > **Gerar script de ação para a janela de consulta**:
 
    ![Gerar script de backup de BD](media/scripting-ssms/scriptdbbackup.PNG)
6. Examine o T-SQL populado na janela de consulta: 

    ![Gerar script para backup de BD](media/scripting-ssms/dbbackupscript.PNG)


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>Gerar script de T-SQL ao reduzir o log de transações
1. Clique com o botão direito do mouse no banco de dados > **Tarefas** > **Reduzir** > **Arquivos**:

     ![Reduzir Arquivos](media/scripting-ssms/shrinkfiles.png)

2. Selecione **Log** na lista suspensa **Tipo de Arquivo**:

    ![Reduzir o Log de Transações](media/scripting-ssms/shrinktlog.png)

3. Clique na opção **Gerar script** e **Gerar script de ação para área de transferência**:

    ![Script para Área de Transferência](media/scripting-ssms/scriptactiontoclipboard.png)

4. Abra uma janela **Nova Consulta** e cole (clique com o botão direito do mouse na janela > **Colar**):

    ![Excluir Script](media/scripting-ssms/paste.png)


## <a name="script-databases"></a>Gerar script de bancos de dados
A seção a seguir ensina como gerar o script do banco de dados, tanto usando a opção **Escrever script como** quanto a **Gerar Scripts**.  A opção **Escrever script como** recriará o banco de dados e as opções de configuração para ele. A opção **Gerar scripts** criará o script de todos os objetos no banco de dados, mas não os dados. Para criar o script também dos dados, será necessário usar o [Assistente de Importação e Exportação](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/start-the-sql-server-import-and-export-wizard).  


### <a name="script-database-using-script-option"></a>Script de banco de dados usando a opção Criar script
1. Conecte-se ao SQL Server.
2. Expanda o nó **Bancos de Dados** .
3. Clique com o botão direito do mouse no banco de dados > **Criar script de banco de dados como**:

    ![Criar script de BD](media/scripting-ssms/scriptdb.png)

4. Revise a consulta de criação de banco de dados na janela: 

    ![Script de BD gerado](media/scripting-ssms/scriptedoutdb.png)
    - Essa opção só criará as opções de configuração do banco de dados.  

### <a name="script-database-using-generate-scripts-option"></a>Script de banco de dados usando a opção de Gerar Scripts
1. Conecte-se ao SQL Server.
2. Expanda o nó **Bancos de Dados** .
3. Clique com o botão direito do mouse no banco de dados > **Tarefas** > **Gerar Scripts**:

    ![Gerar scripts para BD](media/scripting-ssms/generatescriptsfordb.png)

4. Selecione **Avançar** e você verá que é possível optar por gerar o script de todo o banco de dados ou de objetos específicos no banco de dados: 
 
    ![Gerar scripts para objetos](media/scripting-ssms/scriptobjects.png)
 
5. Selecione **Avançar**. É nesta tela que você configura onde o script será salvo. 
    - Também é possível configurar opções avançadas selecionando **Avançado**:

    ![Opções de Script Avançadas](media/scripting-ssms/advancedscripts.png)

6. Quando estiver pronto para continuar, continue clicando em **Avançar** até que os scripts sejam gerados e você chegue até o **Concluir**. O script de banco de dados se encontrará onde ele foi salvo na Etapa 5. 
    - Isso gerará o script do esquema e de vários objetos no banco de dados, mas não dos dados. 
 
## <a name="script-tables"></a>Gerar script de tabelas
Esta seção aborda como gerar o script de tabelas do banco de dados.

1. Conecte-se ao SQL Server.
2. Expanda o nó **Bancos de Dados**.
3. Expanda o nó **AdventureWorks** do banco de dados. 
4. Expanda o nó **Tabelas**.
5. Clique com o botão direito do mouse na tabela para a qual você deseja gerar o script > **Criar script de tabela como**:
    - Há várias opções aqui, como criar a tabela ou inserir dados nela: 
    
    ![Tabela de script](media/scripting-ssms/scripttable.png)
 
## <a name="script-stored-procedures"></a>Gerar script de procedimentos armazenados
Esta seção aborda como gerar o script de procedimentos armazenados. 

1. Conecte-se ao SQL Server.
2. Expanda o nó **Bancos de Dados**.
3. Expanda o nó **Programação**. 
4. Expanda o nó **Procedimento Armazenado**.
5. Clique com o botão direito do mouse no procedimento armazenado de seu interesse > **Criar script de procedimento armazenado como**:
    
    ![Gerar script de procedimentos armazenados](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>Gerar script de eventos estendidos
Esta seção aborda como gerar o script de [eventos estendidos](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events). 

1. Conecte-se ao SQL Server.
2. Expanda o nó **Gerenciamento**.
3. Expanda o nó **Eventos Estendidos**.
4. Expanda o nó **Sessões**.
5. Clique com o botão direito do mouse na sessão estendida de seu interesse > **Criar script de sessão como**:

    ![Gerar script de xEvents](media/scripting-ssms/scriptxevents.png) 

## <a name="next-steps"></a>Próximas etapas
O próximo artigo apresentará os modelos predefinidos encontrados no SSMS. 

Prossiga para o próximo artigo para saber mais
> [!div class="nextstepaction"]
> [Botão Próximas etapas](templates-ssms.md)


