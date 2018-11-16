---
title: Usar o Assistente para Copiar Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.cdw.packageconfiguration.f1
- sql13.swb.cdw.schedule.f1
- sql13.swb.cdw.transfermethod.f1
- sql13.swb.cdw.databases.f1
- sql13.swb.cdw.destinationconfiguration.f1
- sql13.swb.cdw.destination.f1
- sql13.swb.cdw.locationofsourcedbfiles.f1
- sql13.swb.cdw.source.f1
- sql13.swb.cdw.selectdatabaseobjects.f1
- sql13.swb.cdw.complete.f1
- sql13.swb.cdw.welcome.f1
helpviewer_keywords:
- Copy Database Wizard
- starting Copy Database Wizard
ms.assetid: 7a999fc7-0a26-4a0d-9eeb-db6fc794f3cb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3513d85607582a8aab726804f2501ee675859460
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560503"
---
# <a name="use-the-copy-database-wizard"></a>Usar o Assistente para Copiar Banco de Dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O Assistente para Copiar Banco de Dados move ou copia bancos de dados e determinados objetos de servidor facilmente de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  para outra instância, sem tempo de inatividade do servidor. Com esse assistente, é possível fazer o seguinte: 
  
-   Selecionar um servidor de origem e de destino.  
  
-   Selecione os bancos de dados a serem migrados ou copiados.  
  
-   Especifique o local de arquivo dos bancos de dados.  
  
-   Copie os logons no servidor de destino.  
  
-   Copiar objetos, trabalhos, procedimentos armazenados definidos pelo usuário e mensagens de erro de suporte adicionais.  
  
-   Agende a movimentação ou cópia dos bancos de dados.  
  

  
##  <a name="Restrictions"></a> Limitações e restrições  
  
-   O Assistente para Copiar Banco de Dados não está disponível na edição Express.  
  
-   O Assistente para Copiar Banco de Dados não pode ser usado para copiar ou mover os bancos de dados que:
  
    -   São do Sistema.
  
    -   São marcados para replicação.
  
    -   São marcados como Inacessível, Carregando, Offline, Recuperando, Suspeito ou em Modo de Emergência.
    
    -   Armazene dados ou arquivos de log no armazenamento do Microsoft Azure.
  
-   Um banco de dados não pode ser movido nem copiado para uma versão anterior do SQL Server.
  
-   Se você selecionar a opção **Migrar** , o assistente excluirá o banco de dados de origem automaticamente após migrá-lo. Se você selecionar **Copiar** , o Assistente para Copiar Banco de Dados não excluirá o banco de dados de origem.  Além disso, os objetos de servidor selecionados são copiados, em vez de movidos para o destino; o banco de dados é o único objeto que é realmente movido.
  
-   Se você usar o método [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object para mover o catálogo de texto completo, deverá repopular o índice após a movimentação.  
  
-   O método **desanexar e anexar** desanexa o banco de dados, move ou copia os arquivos .mdf, .ndf e .ldf do banco de dados e os reanexa ao banco de dados no novo local. Ao utilizar o método **desanexar e anexar** , para evitar perda ou inconsistência de dados, as sessões ativas não podem ser anexadas ao banco de dados que está sendo movido ou copiado. No método [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object, permitem-se sessões ativas porque o banco de dados nunca é colocado offline.  

-    A transferência de trabalhos do SQL Server Agent que faz referência a bancos de dados que ainda não existem no servidor de destino causará a falha de toda a operação.  O Assistente tenta criar um trabalho do SQL Server Agent antes de criar o banco de dados.  Como uma solução alternativa:
     1. Crie um banco de dados do shell no servidor de destino com o mesmo nome do banco de dados a ser copiado ou movido.  Veja [Criar um banco de dados](../../relational-databases/databases/create-a-database.md).
     
     2. Na página **Configurar Banco de Dados de Destino** , selecione **Remover qualquer banco de dados no servidor de destino que tenha o mesmo nome e continuar a transferência do banco de dados, substituindo arquivos de banco de dados existentes**.

> **IMPORTANTE:** O método **desanexar e anexar** fará com que a propriedade de banco de dados de origem e destino seja definida como o logon que executa o **Assistente para Copiar Banco de Dados**.  Veja [ALTER AUTHORIZATION (Transact-SQL)](../../t-sql/statements/alter-authorization-transact-sql.md) para alterar a propriedade de um banco de dados.
  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
-   Verifique se o SQL Server Agent foi iniciado no servidor de destino.  

-   Verifique se os diretórios de dados e de arquivos de log no servidor de origem podem ser acessados por meio do servidor de destino.

-   No método **desanexar e anexar** , deve existir um Proxy do SQL Server Agent para o subsistema SSIS no servidor de destino com uma credencial que possa acessar o sistema de arquivos dos servidores de origem e de destino. Para obter mais informações sobre proxies, veja [Criar um proxy do SQL Server Agent](~/ssms/agent/create-a-sql-server-agent-proxy.md).

> **IMPORTANTE:** No método **desanexar e anexar** , o processo de cópia ou movimentação falhará se não for usada uma conta Proxy do Integration Services.  Em determinadas situações, o banco de dados de origem não será reanexado ao servidor de origem e todas as permissões de segurança do NTFS serão extraídas dos dados e arquivos de log.  Se isso acontecer, navegue até os arquivos, aplique novamente as permissões relevantes e reanexe o banco de dados à instância do SQL Server.
  
##  <a name="Recommendations"></a> Recomendações  
  
-   Para garantir o desempenho ideal de um banco de dados atualizado, execute [sp_updatestats (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md) (atualização de estatísticas) nele.  
  
-   Ao mover ou copiar um banco de dados para outra instância do servidor, para oferecer uma experiência consistente aos usuários e aplicativos, pode ser necessário recriar alguns ou todos os metadados do banco de dados, como logons e trabalhos, na outra instância de servidor. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  

  
###  <a name="Permissions"></a> Permissões  
 Você deve ser membro da função de servidor fixa **sysadmin** em ambos os servidores, de origem e de destino.  
  
##  <a name="Overview"></a> As páginas Copiar Banco de Dados do assistente 
Inicie o **Assistente para Copiar Banco de Dados** no SQL Server Management Studio por meio do **Pesquisador de Objetos** e expanda **Bancos de Dados**.  Em seguida, clique com o botão direito do mouse em um banco de dados, aponte para **Tarefas**e clique em **Copiar Banco de Dados**.  Se a tela inicial **Bem-vindo ao Assistente para Copiar Banco de Dados** for exibida, clique em **Avançar**.


### <a name="select-a-source-server"></a>Selecionar um servidor de origem
Usado para especificar o servidor com o banco de dados a ser movido ou copiado e para inserir as informações de logon.  Depois de selecionar o método de autenticação e digitar as informações de logon, clique em **Avançar** para estabelecer conexão com o servidor de origem.  Essa conexão permanece aberta durante a sessão.

-    **Servidor de origem**  
Usado para identificar o nome do servidor no qual os bancos de dados que você deseja mover ou copiar estão localizados.  Insira manualmente ou clique nas reticências para navegar até o servidor desejado.  O servidor deve ser, pelo menos, SQL Server 2005.

-    **Usar Autenticação do Windows**  
Permite que um usuário se conecte por meio de uma conta de usuário do Microsoft Windows.

-    **Usar Autenticação do SQL Server**  
Permite que um usuário se conecte fornecendo um nome de usuário e uma senha da Autenticação do SQL Server.

     -    **User name**  
Usado para inserir o nome de usuário que será usado para se conectar. Esta opção só estará disponível se você tiver optado por conectar-se usando a **Autenticação do SQL Server**.

     -    **Senha**  
Usado para inserir a senha do logon. Esta opção só estará disponível se você tiver optado por conectar-se usando a **Autenticação do SQL Server**.

###  <a name="select-a-destination-server"></a>Selecionar um servidor de destino
Usado para especificar o servidor para o qual o banco de dados será movido ou copiado.  Se você definiu os servidores de origem e destino com a mesma instância de servidor, você fará uma cópia do banco de dados.  Nesse caso, renomeie o banco de dados em um ponto posterior do assistente.  O nome do banco de dados de origem poderá ser usado somente para o banco de dados copiado ou migrado se não houver conflitos de nome no servidor de destino.  Se houver conflitos de nome, será preciso resolvê-los manualmente no servidor de destino para poder usar o nome do banco de dados de origem nele.
  
-    **Servidor de destino**  
Usado para identificar o nome do servidor para o qual os bancos de dados que você deseja mover ou copiar estão localizados.  Insira manualmente ou clique nas reticências para navegar até o servidor desejado.  O servidor deve ser, pelo menos, SQL Server 2005.

     >**OBSERVAÇÃO** Você pode usar um destino que é um servidor clusterizado; o Assistente para Copiar Banco de Dados garantirá que você selecionará somente unidades compartilhadas em um servidor de destino clusterizado.

-    **Usar Autenticação do Windows**  
Permite que um usuário se conecte por meio de uma conta de usuário do Microsoft Windows.

-    **Usar Autenticação do SQL Server**  
Permite que um usuário se conecte fornecendo um nome de usuário e uma senha da Autenticação do SQL Server.

     -    **User name**  
Usado para inserir o nome de usuário que será usado para se conectar. Esta opção só estará disponível se você tiver optado por conectar-se usando a **Autenticação do SQL Server**.

     -    **Senha**  
Usado para inserir a senha do logon. Esta opção só estará disponível se você tiver optado por conectar-se usando a **Autenticação do SQL Server**.

###  <a name="select-the-transfer-method"></a>Selecionar o método de transferência
 
-    **Usar o método desanexar e anexar**  
Desanexa o banco de dados do servidor de origem, copia os arquivos do banco de dados (.mdf, .ndf e . ldf) para o servidor de destino e anexa o banco de dados ao servidor de destino. Esse método é geralmente o mais rápido porque o trabalho principal é ler o disco de origem e gravar o disco de destino. Nenhuma lógica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é exigida para criar objetos dentro do banco de dados ou para criar estruturas de armazenamento de dados. Porém, este método pode ser mais lento se o banco de dados contiver uma grande quantidade de espaço alocado, mas não utilizado. Por exemplo, um banco de dados novo e praticamente vazio que seja criado alocando 100 MB, copia todos os 100 MB, mesmo que apenas 5 MB estejam completos.

     > **OBSERVAÇÃO** Esse método torna o banco de dados indisponível para os usuários durante a transferência.

     -    **Se ocorrer uma falha, anexar novamente o banco de dados de origem**  
     Quando um banco de dados é copiado, os arquivos do banco de dados original são sempre anexados novamente ao servidor de origem. Use essa caixa para anexar novamente os arquivos originais ao banco de dados de origem se não for possível mover um banco de dados. 
  
-    **Usar o método SQL Management Object**  
     Esse método lê a definição de cada objeto de banco de dados no banco de dados de origem e cria cada objeto no banco de dados de destino. Depois ele transfere os dados das tabela de origem para as tabelas de destino, recriando os índices e os metadados.
  
     > [!NOTE]
     >  Os usuários do banco de dados podem continuar a acessar o banco de dados durante a transferência. 
  
###  <a name="select-database"></a>Selecionar banco de dados
Selecione os bancos de dados que deseja mover ou copiar do servidor de origem para o servidor de destino.  Consulte [Limitações e restrições](#Restrictions) na parte superior do tópico.  
  
-    **Migrar**  
Mova o banco de dados para o servidor de destino.

-    **Copiar**  
Copie o banco de dados no servidor de destino.

-    **Origem**  
Exibe os bancos de dados existentes no servidor de origem.

-    **Status**  
Exibe várias informações do banco de dados de origem.

-    **Atualizar**  
Atualize a lista de bancos de dados.
  
### <a name="configure-destination-database"></a>Configurar Banco de Dados de Destino
Altere o nome de banco de dados se apropriado e especifique o local e os nomes dos arquivos de banco de dados.  Essa página aparece uma vez para cada banco de dados que é movido ou copiado.

-    **Banco de Dados de Origem**  
O nome do banco de dados de origem.  A caixa de texto não é editável.

-    **Banco de Dados de Destino**  
O nome do banco de dados de destino a ser criado (modifique conforme desejado).

-    **Arquivos de banco de dados de destino:**  
     
     -    **Filename**  
O nome do arquivo de banco de dados de destino a ser criado (modifique conforme desejado).

     -    **Tamanho (MB)**  
Tamanho do arquivo de banco de dados de destino em megabytes.

     -    **Pasta de Destino**  
A pasta no servidor de destino para hospedar o arquivo de banco de dados de destino (modifique conforme desejado).

     -    **Status**  
Status

-    **Se o banco de dados de destino já existir:**  
     Decida qual ação será tomada se o banco de dados de destino já existir.

     -    **Parar a transferência se existir um banco de dados ou arquivo com o mesmo nome no destino.**

     -    **Descartar qualquer banco de dados no servidor de destino que tenha o mesmo nome e continuar a transferência do banco de dados, substituindo arquivos de banco de dados existentes.**

###  <a name="select-server-objects"></a>Selecionar objetos do servidor 
Essa página está disponível apenas quando os servidores de origem e de destino forem diferentes.  
  
-    **Objetos relacionados disponíveis**  
Lista os objetos disponíveis a serem transferidos para o servidor de destinos.  Para incluir um objeto, clique no nome do objeto na caixa **Objetos relacionados disponíveis** e clique no botão **>>** para mover o objeto para a caixa **Objetos relacionados selecionados** . 

-    **Objetos relacionados selecionados**  
Lista os objetos que serão transferidos para o servidor de destinos.  Para excluir um objeto, clique no nome do objeto na caixa **Objetos relacionados selecionados** e clique no botão **<\<** para mover o objeto para a caixa **Objetos relacionados disponíveis** .  Por padrão, são transferidos todos os objetos de cada tipo selecionado. Para escolher objetos individuais de qualquer tipo, clique no botão de reticências ao lado de qualquer tipo de objeto na caixa **Objetos relacionados selecionados** .  Isso abre uma caixa de diálogo onde você pode selecionar objetos individuais.

-    **Lista de objetos de servidor** 

      -    **Logons (Selecionados por padrão.)** 
  
     -    **trabalhos do SQL Server Agent**  
  
     -    **Mensagens de erro definidas pelo usuário**  
  
     -    **Pontos de extremidade**  
  
     -    **Catálogo de texto completo** 
  
     -    **Pacote SSIS**  
     
     -    **Procedimentos armazenados do banco de dados mestre** 
          >**OBSERVAÇÃO** Procedimentos armazenados estendidos e seus DLLs associados não são qualificados para cópia automatizada.  
    
  
###   <a name="location-of-source-database-files"></a>Local dos arquivos de banco de dados de origem
Essa página está disponível apenas quando os servidores de origem e de destino forem diferentes.  Especifique um compartilhamento de sistema de arquivos que contém os arquivos de banco de dados no servidor de origem.
  
-    **Backup de banco de dados**  
     Exibe o nome de cada banco de dados que é movido.  
  
-    **Local da pasta**  
O local da pasta dos arquivos de banco de dados no servidor de origem.
Por exemplo: `C:\Program Files\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\DATA`.

  
-    **Compartilhamento de arquivo no servidor de origem**  
O compartilhamento de arquivos que contém os arquivos de banco de dados no servidor de origem.  Insira manualmente o compartilhamento ou clique nas reticências para navegar até ele.
Por exemplo: `\\server_name\C$\Program Files\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\Data`.

### <a name="configure-the-package"></a>Configurar o pacote
O Assistente para Copiar Banco de Dados cria um pacote SSIS para transferir o banco de dados.

-    **Local do pacote**  
Exibe o local em que o pacote SSIS será gravado.

-    **Nome do pacote**  
Será criado um nome padrão para o pacote SSIS (modifique conforme desejado).

-    **Opções de log**  
Selecione se as informações de log serão armazenadas no log de eventos do Windows ou em um arquivo de texto.

-    **Caminho do arquivo de log de erros**  
Essa opção só estará disponível se a opção de log de arquivo de texto for selecionada.  Forneça um caminho para o local do arquivo de log. 

### <a name="schedule-the-package"></a>Agendar o pacote
Especifique quando deseja que a operação de mover ou copiar seja iniciada.  Se você não for um administrador do sistema, deverá especificar uma conta proxy do SQL Server Agent que tenha acesso ao subsistema de execução de Pacote SSIS (Integration Services).

> **IMPORTANTE:** Deve-se usar uma conta Proxy do Integration Services no método **desanexar e anexar** .  

-    **Executar imediatamente**  
     O Pacote SSIS será executado após a conclusão do assistente.
  
-    **Agenda**  
     O Pacote SSIS será executado de acordo com um agendamento. 
  
     -    **Alterar agendamento**   
Abre a caixa de diálogo **Novo Agendamento de Trabalho** .  Configure-a, conforme desejado.  Clique em **OK** quando terminar.


-    **Conta proxy do Integration Services** Selecione uma conta proxy disponível na lista suspensa.  Para agendar a transferência, deve haver, pelo menos, uma conta proxy disponível para o usuário, configurada com permissão para o **subsistema de execução do pacote SSIS**.

        Para criar uma conta proxy para a execução do pacote SSIS, no **Pesquisador de Objetos**, expanda **SQL Server Agent**, expanda **Proxies**, clique com o botão direito do mouse em **Execução do Pacote SSIS**e clique em **Novo Proxy**.

### <a name="complete-the-wizard"></a>Concluir o assistente
Exibe um resumo das opções selecionadas.  Clique em **Voltar** para alterar uma opção.  Clique em **Concluir** para criar o pacote SSIS. A página **Executando operação** monitora informações de status sobre a execução do **Assistente para Copiar Banco de Dados**.

-    **Ação**  
 Lista cada ação que está sendo executada.

-    **Status**  
 Indica se a ação como um todo obteve êxito ou falhou.

-    **Mensagem**  
Fornece qualquer mensagem que retornou de cada etapa.

##  <a name="Examples"></a> Exemplos
### <a name="common-steps"></a>**Etapas comuns** 
Independentemente de você optar por **Mover** ou **Copiar**, **Desanexar e Anexar** ou **SMO**, as cinco etapas listadas abaixo serão as mesmas.  Para resumir, as etapas são listadas aqui uma vez e todos os exemplos serão iniciados na **Etapa 6**.

1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.

2.  Expanda **Bancos de Dados**, clique com o botão direito do mouse em um banco de dados, aponte para **Tarefas**e clique em **Copiar Banco de Dados...**

3.  Se a tela inicial **Bem-vindo ao Assistente para Copiar Banco de Dados** for exibida, clique em **Avançar**.

4.  Página**Selecionar um Servidor de Origem** : especifique o servidor com o banco de dados a ser movido ou copiado.  Selecione o método de autenticação.  Se você escolher a opção **Usar Autenticação do SQL Server** , será necessário inserir suas credenciais de logon.  Clique em **Avançar** para estabelecer a conexão com o servidor de origem.  Essa conexão permanece aberta durante a sessão.

5.  Na página**Selecionar um Servidor de Destino** : especifique o servidor para o qual o banco de dados será movido ou copiado.  Selecione o método de autenticação.  Se você escolher a opção **Usar Autenticação do SQL Server** , será necessário inserir suas credenciais de logon.  Clique em **Avançar** para estabelecer a conexão com o servidor de origem.  Essa conexão permanece aberta durante a sessão.

     > **OBSERVAÇÃO** É possível iniciar o Assistente para Copiar Banco de Dados em qualquer banco de dados.  Você pode usar o Assistente para Copiar Banco de Dados por meio do servidor de origem ou de destino.
  
### <a name="a--move-database-using-detach-and-attach-method-to-an-instance-on-a-different-physical-server--a-login-and-sql-server-agent-job-will-be-moved-as-well"></a>**A.  Mova o banco de dados usando o método desanexar e anexar para uma instância em um servidor físico diferente.  Um logon e um trabalho do SQL Server Agent também serão movidos.**  
O exemplo a seguir moverá o banco de dados `Sales` , um logon do Windows chamado `contoso\Jennie` e um trabalho do SQL Server Agent denominado `Jennie’s Report` de uma instância de 2008 do SQL Server no `Server1` para uma instância de 2016 do SQL Server no `Server2`.  `Jennie’s Report` usa o banco de dados `Sales` .  `Sales` ainda não existir no servidor de destino, `Server2`.  `Server1` será reatribuída a uma equipe diferente após a movimentação do banco de dados.
  
6.  Conforme observado em [Limitações e restrições](#Restrictions)acima, um banco de dados shell precisa ser criado no servidor de destino durante a transferência de um trabalho do SQL Server Agent que faz referência a um banco de dados que ainda não existe no servidor de destino.  Crie um banco de dados shell chamado `Sales` no servidor de destino. 

7.  De volta ao **Assistente**, página **Selecionar Método de Transferência** : examine e mantenha os valores padrão.  Clique em **Avançar**.
  
8.  Página**Selecionar Bancos de Dados** : marque a caixa de seleção **Mover** do banco de dados desejado, `Sales`.  Clique em **Avançar**.
  
9.  Página**Configurar Banco de Dados de Destino** : o **Assistente** identificou que `Sales` já existe no servidor de destino, que foi criado na **Etapa 6** acima, e acrescentou `_new` ao nome do **Banco de dados de destino** .  Exclua `_new` da caixa de texto **Banco de dados de destino** .  Se desejar, altere o **Nome do Arquivo**e a **Pasta de Destino**.  Selecione **Remover qualquer banco de dados no servidor de destino que tenha o mesmo nome e continuar a transferência do banco de dados, substituindo arquivos de banco de dados existentes**.  Clique em **Avançar**.
  
10. Página**Selecionar Objetos do Servidor** : no painel **Objetos relacionados selecionados:** , clique no botão de reticências de **Logons de nome de objeto**.  Em **Opções de Cópia** , selecione **Copiar somente os logons selecionados:**.  Marque a caixa de **Mostrar todos os logons de servidor**.  Marque a caixa **Logon** de `contoso\Jennie`.  Clique em **OK**.  No painel **Objetos relacionados disponíveis:** , selecione **Trabalhos do SQL Server Agent** e clique no botão **>** .  No painel **Objetos relacionados selecionados:** , clique no botão de reticências de **Trabalhos do SQL Server Agent**.  Em **Opções de Cópia** , selecione **Copiar somente os trabalhos selecionados**.  Marque a caixa de `Jennie’s Report`.  Clique em **OK**.  Clique em **Avançar**.  
  
11. Página**Local dos arquivos de banco de dados de origem** : clique no botão de reticências de **Compartilhamento de arquivos no servidor de origem** e navegue até o local da Pasta especificado.  Por exemplo, para o local da Pasta `D:\MSSQL13.MSSQLSERVER\MSSQL\DATA` , use `\\Server1\D$\MSSQL13.MSSQLSERVER\MSSQL\DATA` em **Compartilhamento de arquivos no servidor de origem**.  Clique em **Avançar**.
  
12. Página**Configurar o pacote** : na caixa de texto **Nome do pacote:** insira `SalesFromServer1toServer2_Move`.  Marque a caixa **Salvar logs de transferência?** .  Na lista suspensa **Opções de Log** , selecione **Arquivo de texto**.  Observe o **Caminho do arquivo de log de erros**; examine, conforme desejado.  Clique em **Avançar**.  
  
     > **OBSERVAÇÃO** O **Caminho do arquivo de log de erros** é o caminho no servidor de destino.
  
13. Página**Agendar o pacote** : selecione o proxy relevante na lista suspensa **Conta proxy do Integration Services** .  Clique em **Avançar**.

14. Página**Concluir o Assistente** : examine o resumo das opções selecionadas.  Clique em **Voltar** para alterar uma opção.  Clique em **Concluir** para executar a tarefa.  Durante a transferência, a página **Executando operação** monitora informações de status sobre a execução do **Assistente**.

15. Página**Executando a operação** : se a operação for bem-sucedida, clique em **Fechar**.  Se a operação for bem-sucedida, examine o log de erros e, possivelmente, selecione **Voltar** para uma análise posterior.  Caso contrário, clique em **Fechar**.
  
16. **Etapas pós-movimentação** Considere a execução das seguintes instruções T-SQL no novo host, `Server2`:
  
     ~~~ tsql 
     ALTER AUTHORIZATION ON DATABASE::Sales TO sa;

     ALTER DATABASE Sales 
     SET COMPATIBILITY_LEVEL = 130;

     USE Sales
     GO

     EXEC sp_updatestats;
     ~~~
 
17. **Limpeza de etapas pós-movimentação**  
Como `Server1` será movido para uma equipe diferente e a operação **Move** não será repetida, considere a execução das seguintes etapas:
     -    Exclua o pacote SSIS `SalesFromServer1toServer2_Move` no `Server2`.
     -    Excluindo um trabalho `SalesFromServer1toServer2_Move` do SQL Server Agent no `Server2`.
     -    Excluindo um trabalho `Jennie’s Report` do SQL Server Agent no `Server1`.
     -    Removendo o logon `contoso\Jennie` no `Server1`.


### <a name="b-----copy-database-using-detach-and-attach-method-to-the-same-instance-and-set-recurring-schedule"></a>**B.     Copie o banco de dados usando o método desanexar e anexar na mesma instância e defina o agendamento recorrente.**  
Neste exemplo, o banco de dados `Sales` será copiado e criado como `SalesCopy` na mesma instância.  Depois disso, `SalesCopy`será recriado semanalmente.

6.  Página**Selecionar um Método de Transferência** : examine e mantenha os valores padrão.  Clique em **Avançar**.

7.  Página**Selecionar Bancos de Dados** : marque a caixa de seleção **Copiar** do banco de dados `Sales` .  Clique em **Avançar**.

8.  Página**Configurar Banco de Dados de Destino** : altere o nome do **Banco de dados de destino** para `SalesCopy`.  Se desejar, altere o **Nome do Arquivo**e a **Pasta de Destino**.  Selecione **Remover qualquer banco de dados no servidor de destino que tenha o mesmo nome e continuar a transferência do banco de dados, substituindo arquivos de banco de dados existentes**.  Clique em **Avançar**.

9.  Página**Configurar o pacote** : na caixa de texto **Nome do pacote:** insira `SalesCopy Weekly Refresh`.  Marque a caixa **Salvar logs de transferência?** .  Clique em **Avançar**.

10. Página**Agendar o pacote** : clique no botão de opção **Agendamento:** e no botão **Alterar Agendamento** . 
 
    1. Página**Novo agendamento de trabalho** : na caixa de texto **Nome** , insira `Weekly on Sunday`. 
          
    2. Clique em **OK**.

11. Selecione o proxy relevante na lista suspensa **Conta proxy do Integration Services** .  Clique em **Avançar**.

12. Página**Concluir o Assistente** : examine o resumo das opções selecionadas.  Clique em **Voltar** para alterar uma opção.  Clique em **Concluir** para executar a tarefa.  Durante a criação de pacote, a página **Executando operação** monitora informações de status sobre a execução do **Assistente**.

13. Página**Executando a operação** : se a operação for bem-sucedida, clique em **Fechar**.  Se a operação for bem-sucedida, examine o log de erros e, possivelmente, selecione **Voltar** para uma análise posterior.  Caso contrário, clique em **Fechar**.

14. Inicie manualmente o Trabalho `SalesCopy weekly refresh`do SQL Server Agent recém-criado.  Examine o histórico de trabalhos e garanta que `SalesCopy` agora existe na instância.

  
##  <a name="FollowUp"></a> Acompanhamento: Após a atualização de um banco de dados  
 Após o uso do Assistente para Copiar Banco de Dados para atualizar um banco de dados de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados é disponibilizado imediatamente e é atualizado de forma automática. Se o banco de dados tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices dependendo da configuração da propriedade de servidor **Opção de Atualização de Texto Completo** . Se a opção de atualização for definida como **Importar** ou **Recriar**, os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação pode levar várias horas, e a recriação pode ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida como **Importar**, se não houver um catálogo de texto completo disponível, os índices de texto completo associados serão recompilados. Para obter informações sobre como exibir ou alterar a configuração da propriedade **Full-Text Upgrade Option** , veja [Gerenciar e monitorar a pesquisa de texto completo para uma instância de servidor](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
 Se o nível de compatibilidade de um banco de dados de usuário era 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização. Se o nível de compatibilidade era 90, no banco de dados atualizado, o nível de compatibilidade será definido como 100, que é o nível de compatibilidade mais baixo com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
 
 ## <a name="Post"></a> Considerações sobre pós-cópia ou movimentação
 Considere a possibilidade de executar as seguintes etapas após uma **Cópia** ou **Movimentação**:
-    Alteração da propriedade dos bancos de dados quando o método desanexar e anexar é usado.
-    Remoção de objetos do servidor no servidor de origem após uma **Movimentação**.
-    Remoção do pacote SSIS criado pelo Assistente no servidor de destino.
-    Remoção do trabalho do SQL Server Agent criado pelo Assistente no servidor de destino.

  
## <a name="more-information"></a>Mais informações! 
 [Atualizar um banco de dados usando Desanexar e Anexar &#40;Transact-SQL&#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md)   
 [Criar um proxy do SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
  

