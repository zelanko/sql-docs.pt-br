---
title: 'Solução de problemas: localizar erros com replicação transacional do SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 705bf95c2bcff4062962166249055ec940f00d5b
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769346"
---
# <a name="troubleshooter-find-errors-with-sql-server-transactional-replication"></a>Solução de problemas: localizar erros com replicação transacional do SQL Server 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

Solucionar problemas de erros de replicação pode ser frustrante sem uma compreensão básica de como a replicação transacional funciona. A primeira etapa para se criar uma publicação é fazer com que o Agente de Instantâneo crie o instantâneo e salvá-lo na pasta de instantâneos. Em seguida, o Agente de Distribuição aplica o instantâneo ao assinante. 

Esse processo cria a publicação e a coloca no estado *sincronizando*. A sincronização funciona em três fases:
1. As transações ocorrerem em objetos que são replicados e marcados como "para replicação" no log de transações. 
2. O Agente de Leitor de Log examina o log de transações e procura por transações marcadas como "para replicação." Essas transações são então salvas no banco de dados de distribuição. 
3. O Agente de Distribuição examina o banco de dados de distribuição usando o thread de leitura. Em seguida, usando o thread de gravação, esse agente se conecta ao assinante para aplicar essas alterações ao assinante.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

Erros podem ocorrer em qualquer etapa desse processo. Localizar os erros pode ser o aspecto mais difícil da solução de problemas de sincronização. Felizmente, o uso do Replication Monitor facilita esse processo. 

>[!NOTE]
> - A finalidade deste guia de solução de problemas é ensinar a metodologia para essa atividade. Ele foi projetado não para resolver o erro específico, mas para fornecer diretrizes gerais sobre como localizar erros com a replicação. Alguns exemplos específicos são fornecidos, mas a resolução para eles pode variar dependendo do ambiente. 
> - Os erros que este guia fornece como exemplos têm base no tutorial [Configurando a replicação transacional](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md).



## <a name="troubleshooting-methodology"></a>Metodologia de solução de problemas 

### <a name="questions-to-ask"></a>Perguntas a fazer
1. Em que ponto do processo de sincronização a replicação está falhando?
2. Qual agente está sofrendo um erro?
1. Quando foi a última vez em que a replicação teve êxito? Alguma coisa foi alterada desde então?  

### <a name="steps-to-take"></a>Etapas a serem executadas
1. Use o Replication Monitor para identificar o ponto em que a replicação está encontrando o erro (qual agente?):
   - Se os erros estão ocorrendo na seção do **Publicador para o Distribuidor**, o problema é com o Agente de Leitor de Log. 
   - Se os erros estão ocorrendo na seção do **Distribuidor para o Assinante**, o problema é com o Agente de Distribuição.  
2. Examine o histórico de trabalhos do agente no Monitor de Atividade do Trabalho para identificar os detalhes do erro. Se o histórico de trabalhos não está mostrando detalhes suficientes, você pode [habilitar o log detalhado](#enable-verbose-logging-on-any-agent) nesse agente específico.
3. Tente determinar uma solução para o erro.


## <a name="find-errors-with-the-snapshot-agent"></a>Localizar erros com o Agente de Instantâneo
O Agente de Instantâneo gera o instantâneo e grava-o na pasta de instantâneos especificada. 

1. Exiba o status do Agente de Instantâneo:

    A. No Pesquisador de Objetos, expanda o nó **Publicação Local** em **Replicação**.

    B. Clique com o botão direito do mouse na publicação **AdvWorksProductTrans** > **Exibir o Status do Agente de Instantâneo**. 

    ![Comando "Exibir o status do Agente de Instantâneo" no menu de atalho](media/troubleshooting-tran-repl-errors/view-snapshot-agent-status.png)

1. Se um erro for relatado no status do Agente de Instantâneo, mais detalhes poderão ser encontrados no histórico de trabalhos do Agente de Instantâneo:

    A. Expanda **SQL Server Agent** no Pesquisador de Objetos e abra o Monitor de Atividade do Trabalho. 

    B. Classifique por **Categoria** e identifique o Agente de Instantâneo pela categoria **REPL-Snapshot**.

    c. Clique com o botão direito do mouse no Agente de Instantâneo e selecione **Exibir Histórico**. 

   ![Seleções para abrir o histórico do Agente de Instantâneo](media/troubleshooting-tran-repl-errors/snapshot-agent-history.png)
    
1. No histórico do Agente de Instantâneo, selecione a entrada de log relevante. Isso geralmente é uma linha ou duas *antes* da entrada que está relatando o erro. (Um X vermelho indica erros.) Examine o texto da mensagem na caixa abaixo dos logs: 

    ![Erro do Agente de Instantâneo para acesso negado](media/troubleshooting-tran-repl-errors/snapshot-access-denied.png)

        The replication agent had encountered an exception.
        Exception Message: Access to path '\\node1\repldata.....' is denied.

Se as permissões do Windows não estiverem configuradas corretamente para a pasta de instantâneos, você verá um erro "acesso negado" para o Agente de Instantâneo. Você precisará verificar as permissões para a pasta em que o instantâneo é armazenado; verifique também se a conta usada para executar o Agente de Instantâneo tem permissões para acessar o compartilhamento.  

## <a name="find-errors-with-the-log-reader-agent"></a>Localizar erros com o Agente de Leitor de Log
O Agente de Leitor de Log se conecta ao banco de dados publicador e verifica o log de transações em busca de todas as transações marcadas como "para replicação". Em seguida, ele adiciona as transações ao banco de dados de distribuição. 

1.  Conectar ao Editor em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Expanda o nó de servidor, clique com o botão direito do mouse na pasta **Replicação** e, em seguida, selecione **Iniciar o Replication Monitor**:  

    ![Comando "Iniciar o Monitor de replicação" no menu de atalho](media/troubleshooting-tran-repl-errors/launch-repl-monitor.png)
  
    O Monitor de replicação abrirá: ![Replication Monitor](media/troubleshooting-tran-repl-errors/repl-monitor.png) 
   
2. O X vermelho é uma indicação de que a publicação não está sendo sincronizada. Expanda **Meus Publicadores** no lado esquerdo e, em seguida, expanda o servidor do publicador relevante.  
  
3.  Selecione a publicação **AdvWorksProductTrans** à esquerda e, em seguida, procure o X vermelho em uma das guias para identificar onde está o problema. Nesse caso, o X vermelho está na guia **Agentes**, indicando que um dos agentes está apresentando um erro: 

    ![X vermelho na guia "Agentes"](media/troubleshooting-tran-repl-errors/agent-error.png)

4. Selecione a guia **Agentes** para identificar qual agente está encontrando o erro: 

    ![X vermelho no Agente de Leitor de Log com falha](media/troubleshooting-tran-repl-errors/log-reader-agent-failure.png)


5. Esta exibição mostra dois agentes, o Agente de Instantâneo e o Agente de Leitor de Log. Aquele que está encontrando um erro tem um X vermelho. Nesse caso, é o Agente de Leitor de Log. 

    Clique duas vezes na linha que está relatando o erro para abrir o histórico do Agente de Leitor de Log. Esse histórico fornece mais informações sobre o erro: 
    
    ![Detalhes do erro para o Agente de Leitor de Log](media/troubleshooting-tran-repl-errors/log-reader-error.png)

       Status: 0, code: 20011, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.
       The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.
       Status: 0, code: 15517, text: 'Cannot execute as the database principal because the principal "dbo" does not exist, this type of principal cannot be impersonated, or you do not have permission.'.
       Status: 0, code: 22037, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.        

6. O erro normalmente ocorre quando o proprietário do banco de dados do publicador não está definido corretamente. Isso pode ocorrer quando um banco de dados é restaurado. Para verificar isso:

    A. Expanda **Bancos de Dados** no Pesquisador de Objetos.

    B. Clique com o botão direito do mouse em **AdventureWorks2012** > **Propriedades**. 

    c. Verifique se existe um proprietário na página **Arquivos**. Se essa caixa estiver vazia, esta será a causa provável do problema. 

   ![Página "Arquivos" nas propriedades do banco de dados, com uma caixa "Proprietário" em branco](media/troubleshooting-tran-repl-errors/db-properties.png)

7. Se o proprietário estiver em branco na página **Arquivos**, abra uma janela **Nova Consulta** dentro do contexto do banco de dados AdventureWorks2012. Execute o seguinte código T-SQL:

    ```sql
    -- set the owner of the database to 'sa' or a specific user account, without the brackets. 
    EXEC sp_changedbowner '<useraccount>'
    -- example for sa: exec sp_changedbowner 'sa'
    -- example for user account: exec sp_changedbowner 'sqlrepro\administrator' 
    ```

8. Talvez você precise reiniciar o Agente de Leitor de Log:

    A. Expanda o nó do **SQL Server Agent** no Pesquisador de Objetos e abra o Monitor de Atividade do Trabalho.

    B. Classifique por **Categoria** e identifique o Agente de Leitor de Log pela categoria **REPL-LogReader**. 

    c. Clique com o botão direito do mouse no trabalho do **Agente de Leitor de Log** e selecione **Iniciar Trabalho na Etapa**. 

    ![Seleções para reiniciar o Agente de Leitor de Log](media/troubleshooting-tran-repl-errors/start-job-at-step.png)

9. Valide se agora a publicação está sincronizando abrindo o Replication Monitor novamente. Se ainda ele ainda não estiver aberto, ele poderá ser encontrado clicando com o botão direito do mouse em **Replicação** no Pesquisador de Objetos. 
10. Selecione a publicação **AdvWorksProductTrans**, selecione a guia **Agentes** e clique duas vezes no Agente de Leitor de Log para abrir o histórico do agente. Agora você deverá ver que o Agente de Leitor de Log está em execução e replicando comandos ou que ele mostra a mensagem "nenhuma transação replicada":

    ![Agente de Leitor de Log em execução sem nenhuma transação replicada](media/troubleshooting-tran-repl-errors/log-reader-running.png)

## <a name="find-errors-with-the-distribution-agent"></a>Encontrar erros com o Agente de Distribuição
O Agente de Distribuição localiza os dados no banco de dados de distribuição e, em seguida, aplica-os ao assinante. 

1. Conectar ao Editor em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Expanda o nó de servidor, clique com o botão direito do mouse na pasta **Replicação** e, em seguida, selecione **Iniciar o Replication Monitor**.  
2. Em **Replication Monitor**, selecione a publicação **AdvWorksProductTrans** e a guia **Todas as Assinaturas**. Clique com o botão direito do mouse na Assinatura e selecione **Exibir Detalhes**:

    ![Comando "Exibir Detalhes" no menu de atalho](media/troubleshooting-tran-repl-errors/view-details.png)

2. A caixa de diálogo **Histórico do Distribuidor para Assinante** é aberta e esclarece qual é o erro que o agente está apresentando: 

     ![Detalhes do erro para o Agente de Distribuição](media/troubleshooting-tran-repl-errors/dist-history-error.png)
    
        Error messages:
        Agent 'NODE1\SQL2016-AdventureWorks2012-AdvWorksProductTrans-NODE2\SQL2016-7' is retrying after an error. 89 retries attempted. See agent job history in the Jobs folder for more details.

3. O erro indica que o Agente de Distribuição está tentando novamente. Para obter mais informações, verifique o histórico de trabalhos do Agente de Distribuição: 

    A. Expanda **SQL Server Agent** em Pesquisador de Objetos > **Monitor de Atividade do Trabalho**. 
    
    B. Classifique os trabalhos por **Categoria**. 

    c. Identifique o Agente de Distribuição pela categoria **REPL-Distribution**. Clique com o botão direito do mouse no agente e selecione **Exibir Histórico**.

    ![Seleções para exibir o histórico do Agente de Distribuição](media/troubleshooting-tran-repl-errors/view-dist-agent-history.png)

5. Selecione uma das entradas de erro e exiba o texto de erro na parte inferior da janela:  

    ![Texto de erro que indica uma senha incorreta para o agente de distribuição](media/troubleshooting-tran-repl-errors/dist-pw-wrong.png)
    
        Message:
        Unable to start execution of step 2 (reason: Error authenticating proxy NODE1\repl_distribution, system error: The user name or password is incorrect.)

6. Esse erro é uma indicação de que a senha usada pelo Agente de Distribuição está incorreta. Para resolvê-lo:

    A. Expanda o nó **Replicação** no Pesquisador de Objetos.
    
    B. Clique com o botão direito do mouse na assinatura > **Propriedades**.
    
    c. Selecione as reticências (...) ao lado de **Conta de Processo do Agente** e modifique a senha.

    ![Seleções para modificar a senha do Agente de Distribuição](media/troubleshooting-tran-repl-errors/dist-agent-pw-change.png)

7. Verifique o Replication Monitor novamente clicando com o botão direito do mouse em **Replicação** no Pesquisador de Objetos. Um X vermelho em **Todas as Assinaturas** indica que o Agente de Distribuição ainda está encontrando um erro. 

    Abra o histórico de **Distribuição ao Assinante** clicando com o botão direito do mouse na assinatura em **Replication Monitor** > **Exibir Detalhes**. Aqui, o erro agora é diferente: 

    ![Erro que indica que o Agente de Distribuição não pode se conectar](media/troubleshooting-tran-repl-errors/dist-agent-cant-connect.png)
           
        Connecting to Subscriber 'NODE2\SQL2016'        
        Agent message code 20084. The process could not connect to Subscriber 'NODE2\SQL2016'.
        Number:  18456
        Message: Login failed for user 'NODE2\repl_distribution'.

8. Esse erro indica que o Agente de Distribuição não pôde se conectar ao assinante, pois houve uma falha de logon do usuário **NODE2\repl_distribution**. Para investigar melhor, conecte-se ao assinante e abra o log de erros do SQL Server *atual* no nó **Gerenciamento** do Pesquisador de Objetos: 

    ![Erro que indica que o logon falhou para o assinante](media/troubleshooting-tran-repl-errors/login-failed.png)
    
    Se você está vendo esse erro, o logon está ausente no assinante. Para resolver esse erro, consulte [Permissões para replicação](../../relational-databases/replication/security/security-role-requirements-for-replication.md).

9. Depois que o erro de logon for resolvido, verifique o Replication Monitor novamente. Se todos os problemas foram resolvidos, você deverá ver uma seta verde ao lado do **Nome da Publicação** e o status **Em execução** em **Todas as Assinaturas**. 

    Clique com o botão direito do mouse na assinatura para abrir o histórico do **Distribuidor para Assinante** mais uma vez para verificar o êxito. Se essa é a primeira vez que o Agente de Distribuição é executado, você vê que o instantâneo foi copiado em massa para o assinante: 

     ![Agente de Distribuição com um status "Em execução" e uma mensagem sobre cópia em massa](media/troubleshooting-tran-repl-errors/dist-agent-success.png)   


## <a name="enable-verbose-logging-on-any-agent"></a>Habilitar o log detalhado em qualquer agente
Você pode usar o log detalhado para ver informações mais detalhadas sobre erros que ocorrem com qualquer agente na topologia de replicação. As etapas são as mesmas para cada agente. Apenas verifique se você está selecionando o agente correto no Monitor de Atividade do Trabalho. 

   >[!NOTE]   
   > Os agentes podem ser no publicador ou no assinante, dependendo de se tratar de uma assinatura pull ou push. Se você não conseguir encontrar o agente desejado no servidor em que está procurando, tente verificar o outro servidor.  

1. Decida onde você deseja que o log detalhado seja salvo e verifique se a pasta existe. Este exemplo usa c:\temp. 
2. Expanda o nó do **SQL Server Agent** no Pesquisador de Objetos e abra o Monitor de Atividade do Trabalho. 

    ![Comando "Exibir Atividade do Trabalho" no menu de atalho para o Monitor de Atividade do Trabalho](media/troubleshooting-tran-repl-errors/job-activity-monitor.png)    

1. Classifique por **Categoria** e identifique o agente de interesse. Este exemplo usa o Agente de Leitor de Log. Clique com o botão direito do mouse no agente de interesse > **Propriedades**.

    ![Seleções para abrir as propriedades do agente](media/troubleshooting-tran-repl-errors/log-agent-properties.png)

1. Selecione a página **Etapas** e, em seguida, realce a etapa **Executar agente**. Selecione **Editar**. 

    ![Seleções para editar a etapa "Executar agente"](media/troubleshooting-tran-repl-errors/edit-steps.png)

1. Na caixa **Comando**, inicie uma nova linha, digite o texto a seguir e selecione **OK**: 

       -Output C:\Temp\OUTPUTFILE.txt -Outputverboselevel 3
    
    Você pode modificar o local e o nível de detalhes de acordo com sua preferência.

    ![Saída detalhada nas propriedades da etapa de trabalho](media/troubleshooting-tran-repl-errors/verbose.png)

   > [!NOTE]
   > Estas coisas podem fazer seu agente falhar ou o arquivo de saída ficar ausente quando você está adicionando o parâmetro de saída detalhada:
   > - Há um problema de formatação onde o traço se tornou um hífen. 
   > - O local não existe no disco, ou a conta que está executando o agente não tem permissão para gravar no local especificado. 
   > - Há um espaço ausente entre o último parâmetro e o parâmetro `-Output`. 
   > - Diferentes agentes dão suporte a diferentes níveis de detalhamento. Se você habilitar o log detalhado mas seu agente falhar ao iniciar, tente diminuir o nível de detalhes especificado por 1. 

1. Reinicie o Agente de Leitor de Log clicando com o botão direito do mouse no agente > **Parar o Trabalho na Etapa**. Atualize selecionando o ícone **Atualização** da barra de ferramentas. Clique com o botão direito do mouse no agente > **Iniciar Trabalho na Etapa**.
2. Examine a saída no disco. 

    ![Arquivo de texto de saída](media/troubleshooting-tran-repl-errors/output.png)

    
1. Para desabilitar o log detalhado, siga as mesmas etapas anteriores para remover toda a linha `-Output` que você adicionou anteriormente. 

Para obter mais informações, consulte [Habilitar log detalhado para agentes de replicação](https://support.microsoft.com/help/312292/how-to-enable-replication-agents-for-logging-to-output-files-in-sql-se). 


## <a name="see-also"></a>Confira também
<br>[Visão geral da replicação transacional](../../relational-databases/replication/transactional/transactional-replication.md)
<br>[Tutoriais de replicação](../../relational-databases/replication/replication-tutorials.md)
<br>[Blog de ReplTalk](https://blogs.msdn.microsoft.com/repltalk)

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]

