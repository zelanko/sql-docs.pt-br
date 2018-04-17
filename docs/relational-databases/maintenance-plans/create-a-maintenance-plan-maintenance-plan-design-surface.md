---
title: Criar um plano de manutenção (superfície de design do plano de manutenção) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Maintenance Plan Design Surface
ms.assetid: 2ef803ee-a9f8-454a-ad63-fedcbe6838d1
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 30a9e1d1a02e44de418a7d6d8de4acfe694e83f2
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/10/2018
---
# <a name="create-a-maintenance-plan-maintenance-plan-design-surface"></a>Criar um plano de manutenção (Superfície de Design do Plano de Manutenção)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como criar um plano de manutenção de servidor único ou vários servidores usando a Superfície de Design do Plano de Manutenção no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Embora o **Assistente de Plano de Manutenção** seja melhor para criar planos de manutenção básicos, a criação de planos usando a superfície de design permite utilizar o fluxo de trabalho aprimorado.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   [Criando um plano de manutenção usando a Superfície de Design do Plano de Manutenção](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Para criar um plano de manutenção multisservidor, é necessário configurar um ambiente multisservidor contendo um servidor mestre e um ou mais servidores de destino. Devem ser criados e mantidos planos de manutenção multisservidor no servidor mestre. Os planos podem ser exibidos, mas não mantidos, nos servidores de destino.  
  
-   Os membros das funções **db_ssisadmin** e **dc_admin** podem elevar seus privilégios para **sysadmin**. Essa elevação de privilégios pode ocorrer porque essas funções podem modificar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ; esses pacotes podem ser executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o contexto de segurança **sysadmin** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para se proteger contra essa elevação de privilégio ao executar planos de manutenção, conjuntos de coletas de dados e outros pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , configure os trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executam pacotes para usar uma conta proxy com privilégios limitados ou apenas adicione membros **sysadmin** às funções **db_ssisadmin** e **dc_admin** .  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para criar ou gerenciar planos de manutenção, é necessário ser membro da função de servidor fixa **sysadmin** . O Pesquisador de Objetos só exibe o nó **Planos de Manutenção** para usuários que são membros da função de servidor fixa **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Usando a Superfície de Design do Plano de Manutenção  
  
#### <a name="to-create-a-maintenance-plan"></a>Para criar um plano de manutenção  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir o servidor em que você deseja criar um plano de manutenção.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique com o botão direito do mouse na pasta **Planos de Manutenção** e selecione **Novo Plano de Manutenção**.  
  
4.  Na caixa de diálogo **Novo Plano de Manutenção** , na caixa **Nome** , digite um nome para o plano e clique em **OK**. Isso abre a Caixa de Ferramentas e a superfície *maintenance_plan_name* **[Design]** com o subplano **Subplan_1** criado na grade principal.  
  
     As opções a seguir estão disponíveis no cabeçalho do espaço de design.  
  
     **Adicionar Subplano**  
     Adiciona um subplano que você pode configurar.  
  
     **Propriedades do Subplano**  
     Exibe a caixa de diálogo **Propriedades do Subplano** do subplano selecionado na grade principal. Alternativamente, clique duas vezes no subplano na grade para exibir a caixa de diálogo **Propriedades do Subplano** . Consulte abaixo para obter mais informações sobre essa caixa de diálogo.  
  
     **Exclua o Subplano Selecionado**  
     Exclui o subplano selecionado.  
  
     **Agenda do Subplano**  
     Exibe a caixa de diálogo **Nova Agenda de Trabalho** para o subplano selecionado.  
  
     **Remover Agenda**  
     Remove uma agenda do subplano selecionado.  
  
     **Gerenciar Conexões**  
     Exibe a caixa de diálogo **Gerenciar Conexões** . Usado para adicionar conexões de instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adicionais ao plano de manutenção. Consulte abaixo para obter mais informações sobre essa caixa de diálogo.  
  
     **Relatório e Registro em Log**  
     Exibe a caixa de diálogo **Relatório e Registro em Log** . Consulte abaixo para obter mais informações sobre essa caixa de diálogo.  
  
     **Servidores**  
     Exiba a caixa de diálogo **Servidores** , que é usada para selecionar os servidores em que serão executadas as tarefas do subplano. Essa opção só está habilitada em servidores mestre em ambientes multisservidor. Para obter mais informações, consulte [Criar um ambiente multisservidor](http://msdn.microsoft.com/library/edc2b60d-15da-40a1-8ba3-f1d473366ee6) e [Plano de manutenção &#40;Servers&#41;](../../relational-databases/maintenance-plans/maintenance-plan-servers.md).  
  
     **Nome**  
     Exibe o nome do plano de manutenção. Para planos de manutenção novos, o nome é especificado em uma caixa de diálogo antes que o designer de plano de manutenção seja aberto. Para renomear um plano de manutenção, clique com o botão direito do mouse no plano no Pesquisador de Objetos e clique em **Renomear**.  
  
     **Descrição**  
     Exiba ou especifique uma descrição para o plano de manutenção. O comprimento máximo para uma descrição é 512 caracteres.  
  
     **Superfície do Designer**  
     Executa design e mantém os planos de manutenção. Use a superfície de designer para adicionar tarefas de manutenção a um plano, remover tarefas de um plano, especificar os links com precedência entre tarefas e para indicar a ramificação ou paralelismo de uma tarefa.  
  
     Um link de precedência entre duas tarefas estabelece uma relação entre elas. A segunda tarefa (a *tarefa dependente*) é executada somente se o resultado da execução da primeira tarefa (a *tarefa precedente*) corresponde aos critérios especificados. Normalmente o resultado da execução especificado é **Êxito**, **Falha**ou **Conclusão**. Para obter mais informações, consulte a etapa **8** abaixo.  
  
5.  No cabeçalho do espaço de design, clique duas vezes em **Subplano_1** e insira um nome e uma descrição para o subplano na caixa de diálogo **Propriedades do Subplano** .  
  
     As opções a seguir estão disponíveis na caixa de diálogo **Propriedades do Subplano** .  
  
     **Nome**  
     O nome do subplano.  
  
     **Descrição**  
     Uma descrição breve do subplano.  
  
     **Agenda**  
     Indica em qual agendamento o subplano será executado. Clique em **Agenda do Subplano** para abrir a caixa de diálogo **Nova Agenda de Trabalho** . Clique em **Remover Agenda** para excluir a agenda do subplano.  
  
     Lista**Executar como**   
     Selecione a conta a ser usada para executar esta subtarefa.  
  
6.  Clique no ícone **Agenda do Subplano** para inserir detalhes de agenda na caixa de diálogo **Nova Agenda de Trabalho** .  
  
7.  Para criar o subplano, arraste e solte elementos de fluxo de tarefas da **Caixa de Ferramentas** para a superfície de design do plano. Clique duas vezes nas tarefas, para abrir as caixas de diálogo e configurar suas opções.  
  
     As seguintes tarefas de plano de manutenção estão disponíveis na **Caixa de Ferramentas**:  
  
    -   **Tarefa Backup de Banco de Dados**  
  
    -   **Tarefa Verificar Integridade do Banco de Dados**  
  
    -   **Tarefa Executar Trabalho do SQL Server Agent**  
  
    -   **Tarefa Executar Instrução T-SQL**  
  
    -   **Tarefa Limpeza do Histórico**  
  
    -   **Tarefa Limpeza de Manutenção**  
  
    -   **Tarefa de Notificação do Operador**  
  
    -   **Tarefa Recriar Índice**  
  
    -   **Tarefa Reorganizar Índice**  
  
    -   **Tarefa Reduzir Banco de Dados**  
  
    -   **Tarefa Atualizar Estatísticas**  
  
     Para adicionar tarefas à **Caixa de Ferramentas**:  
  
    1.  No menu **Ferramentas** , clique em **Escolher Itens da Caixa de Ferramentas**.  
  
    2.  Selecione as ferramentas que devem aparecer na **Caixa de Ferramentas**e clique em **OK**.  
  
     A adição de tarefas do plano de manutenção à **Caixa de Ferramentas** também as disponibiliza no **Assistente de Plano de Manutenção**. Para obter mais informações sobre as tarefas individuais acima, consulte [Usando o Assistente de Plano de Manutenção](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure) em **Iniciar o Assistente de Plano de Manutenção**.  
  
8.  Para definir um fluxo de trabalho entre tarefas:  
  
    1.  Clique com o botão direito do mouse na tarefa anterior e selecione **Adicionar Restrição de Precedência**.  
  
    2.  Na caixa de diálogo **Fluxo de Controle** , na lista **Para** , selecione a tarefa dependente e clique em **OK**.  
  
    3.  Clique duas vezes no conector entre as duas tarefas para abrir a caixa de diálogo **Editor de Restrição de Precedência** .  
  
         As opções a seguir estão disponíveis na caixa de diálogo **Editor de Restrição de Precedência** .  
  
         **Opção de restrição**  
         Define como uma restrição funciona entre duas tarefas.  
  
         Lista**Operação de avaliação**    
         Especifica a operação de avaliação usada pela restrição de precedência. As operações são: **Constraint**, **Expression**, **Expression and Constraint**e **Expression or Constraint**.  
  
         Lista**Valor**   
         Especifique o valor de restrição: **Êxito**, **Falha**ou **Conclusão**. **Êxito** é o padrão.  
  
        > [!NOTE]  
        >  A linha de restrição de precedência é verde para **Êxito**, vermelha para **Falha**e azul para **Conclusão**.  
  
         **Expressão**  
         Se usar as operações **Expression**, **Expression and Constraint**ou **Expression or Constraint**, digite uma expressão. A expressão deve ser avaliada como um booliano.  
  
         **Teste**  
         Valide a expressão.  
  
         **Várias restrições**  
         Defina como várias restrições interoperam para controlar a execução da tarefa restrita.  
  
         **AND lógico**  
         Selecione para especificar que várias restrições de precedência no mesmo executável devem ser avaliadas juntas. Todas as restrições devem ser avaliadas como True. Essa é a opção padrão.  
  
        > [!NOTE]  
        >  Este tipo de restrição de precedência aparece como uma linha sólida nas cores verde, vermelho ou azul.  
  
         **OR lógico**  
         Selecione para especificar que várias restrições de precedência no mesmo executável devem ser avaliadas juntas. Pelo menos uma restrição deve ser avaliada como True.  
  
        > [!NOTE]  
        >  Este tipo de restrição de precedência aparece como uma linha pontilhada nas cores verde, vermelho ou azul.  
  
9. Para adicionar outro subplano, contendo tarefas executadas em uma agenda diferente, clique em **Adicionar Subplano** na barra de ferramentas para abrir a caixa de diálogo **Propriedades do Subplano** .  
  
10. Para adicionar conexões a servidores diferentes:  
  
    1.  Na barra de ferramentas do espaço de design, clique em **Gerenciar Conexões**.  
  
    2.  Na caixa de diálogo **Gerenciar Conexões** , clique em **Adicionar**.  
  
    3.  Na caixa de diálogo **Propriedades de Conexão** , na caixa **Nome da conexão** , insira o nome da conexão que você está criando.  
  
    4.  Em **Especifique o seguinte para conectar-se aos dados do SQL Server**, na caixa **Selecione ou digite um nome de servidor** , digite o nome do SQL Server que deseja usar ou clique nas reticências **(…)** e selecione um servidor na caixa de diálogo **SQL Server** . Se você selecionar um servidor na caixa de diálogo **SQL Server** , clique em **OK**.  
  
    5.  Em **Insira as informações para fazer logon no servidor**, selecione **Usar Segurança Integrada do Windows NT** ou **Usar nome de usuário e senha específicos**. Se você optar por usar um nome e uma senha de usuário específicos, insira essas informações nas caixas **Nome de usuário** e **Senha** , respectivamente.  
  
    6.  Na caixa de diálogo **Propriedades de Conexão** , clique em **OK**.  
  
    7.  Na caixa de diálogo **Gerenciar Conexões** , clique em **Fechar**.  
  
11. Para especificar opções de relatório:  
  
    1.  Na barra de ferramentas do espaço de design, clique em **Relatório e Registro em Log**.  
  
    2.  Na caixa de diálogo **Relatório e Registro em Log** , em **Relatório**, selecione **Gerar um relatório de arquivo de texto** ou **Enviar relatório para um destinatário de email** ou ambas as opções.  
  
        1.  Se você selecionar **Gerar um relatório de arquivo de texto**, selecione **Criar um novo arquivo** ou **Acrescentar ao arquivo**.  
  
        2.  Dependendo da seleção acima, insira o nome e o caminho completo do novo arquivo ou do arquivo a ser adicionado inserindo as informações nas caixas **Pasta** ou **Nome do arquivo** . Como alternativa, clique nas reticências **(…)** e selecione o caminho para a pasta ou nome de arquivo nas caixas de diálogo **Localizar Pasta –***server_name* ou **Localizar Arquivos de Banco de Dados –***server_name*.  
  
        3.  Se você selecionar **Enviar relatório para um destinatário de email**, na lista **Operador do agente** , selecione o destinatário do relatório enviado por e-mail.  
  
            > [!NOTE]  
            >  O SQL Server Agent deve ser configurado para usar o Database Mail para o envio de email. Para obter mais informações, consulte [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  Para salvar informações mais detalhadas, em **Log**, selecione **Registrar informações estendidas em log**.  
  
    4.  Para gravar informações de resultados do plano de manutenção em outro servidor, selecione **Registrar no servidor remoto** e selecione uma conexão de servidor na lista **Conexão** ou clique em **Nova** e insira as informações de conexão na caixa de diálogo **Propriedades de Conexão** .  
  
    5.  Na caixa de diálogo **Relatório e Registro em Log** , clique em **OK**.  
  
12. Para exibir os resultados no visualizador de arquivo de log, no **Pesquisador de Objetos**, clique com o botão direito do mouse na pasta **Planos de Manutenção** ou no plano de manutenção específico e selecione **Exibir Histórico**.  
  
     As opções a seguir estão disponíveis na caixa de diálogo **Visualizador do Arquivo de Log –***server_name*.  
  
     **Carregar Log**  
     Abra uma caixa de diálogo onde seja possível especificar um arquivo de log a ser carregado.  
  
     **Exportar**  
     Abra uma caixa de diálogo que permita exportar as informações mostradas na grade **Resumo do arquivo de log** para um arquivo de texto.  
  
     **Atualizar**  
     Atualize a exibição dos logs selecionados. O botão **Atualizar** relê os logs selecionados do servidor de destino ao aplicar qualquer configuração de filtro.  
  
     **Filtro**  
     Abra uma caixa de diálogo que permita especificar configurações usadas para filtrar o arquivo de log, como **Conexão**, **Data**ou outros critérios de filtragem **Gerais** .  
  
     **Pesquisa**  
     Pesquise o texto específico no arquivo de log. Não há suporte à pesquisa com caracteres curinga.  
  
     **Parar**  
     Interrompe o carregamento das entradas do arquivo de log. Por exemplo, você poderá usar essa opção se um arquivo de log remoto ou offline demorar muito tempo para ser carregado e você desejar exibir apenas as entradas mais recentes.  
  
     **Resumo do arquivo de log**  
     Esse painel de informações exibe um resumo da filtragem do arquivo de log. Se o arquivo não for filtrado, você verá o seguinte texto, **Nenhum filtro aplicado**. Se um filtro for aplicado ao log, você verá o seguinte texto **Filtrar entradas do log, em que:**  \<filter criteria>.  
  
     **Data**  
     Exibe a data do evento.  
  
     **Origem**  
     Exibe o recurso de origem do qual o evento é criado, como o nome do serviço (MSSQLSERVER, por exemplo). Isso não é exibido para todos os tipos de log.  
  
     **Mensagem**  
     Exibe todas as mensagens associadas ao evento.  
  
     **Tipo de Log**  
     Exibe o tipo de log ao qual o evento pertence. Todos os logs selecionados são exibidos na janela de resumo de arquivo de log.  
  
     **Origem do Log**  
     Exibe uma descrição do log de origem no qual o evento é capturado.  
  
     **Detalhes da linha selecionada**  
     Selecione uma linha para exibir detalhes adicionais sobre a linha de evento selecionada na parte inferior da página. As colunas podem ser reordenadas arrastando-as para locais novos na grade. As colunas podem ser redimensionadas arrastando para a esquerda ou direta as barras separadoras de coluna no cabeçalho de grade. Clique duas vezes nas barras separadoras de coluna no cabeçalho da grade para dimensionar automaticamente a coluna para a largura do conteúdo.  
  
     **Instância**  
     O nome da instância do na qual ocorreu o evento. Esse nome é exibido como *nome do computador*\\*nome da instância*.  
  
  
