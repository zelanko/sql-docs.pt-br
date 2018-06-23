---
title: Configurar o Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Sql12.swb.sqlimail.newaccount.f1
- Sql12.swb.sqlimail.manageexistingaccount.f1
- Sql12.swb.dbmail.manageexistingaccount.f1
- Sql12.swb.sqlimail.manageexistingprofile.f1
- Sql12.swb.sqlimail.newprofile.f1
- Sql12.swb.sqlimail.profileandaccountmanagement.f1
- Sql12.swb.dbmail.configuresystem.f1
- Sql12.swb.dbmail.profileandaccountmanagement.f1
- Sql12.swb.dbmail. manageprofilesecurity.profileview.f1
- Sql12.swb.dbmail.selectconfiguration.f1
- Sql12.swb.dbmail.newsqlimailaccount.f1
- Sql12.swb.sqlimail.manageprofilesecurity.profileview.f1
- Sql12.swb.sqlimail.newsqlimailaccount.f1
- Sql12.swb.dbmail.newaccount.f1
- Sql12.swb.dbmail.manageexistingprofile.f1
- Sql12.swb.sqlimail.configuresystem.f1
- Sql12.swb.sqlimail.selectconfiguration.f1
- Sql12.swb.dbmail.completewizard.f1
- Sql12.swb.sqlimail.welcome.f1
- sql12.swb.dbmail.sendtestemail.f1
- Sql12.swb.sqlimail.addaccounttoprofile.f1
- Sql12.swb.dbmail.welcome.f1
- Sql12.swb.dbmail.newprofile.f1
- Sql12.swb.dbmail.addaccounttoprofile.f1
- sql12.swb.dbmail.sendtestemail.test.f1
- Sql12.swb.sqlimail.completewizard.f1
- Sql12.swb.sqlimail.manageprofilesecurity.principalview.f1
- Sql12.swb.dbmail.manageprofilesecurity.principalview.f1
ms.assetid: 7edc21d4-ccf3-42a9-84c0-3f70333efce6
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a56c620c26a7ef2a7af3dccf59f2f6bcdb0bf3ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121307"
---
# <a name="configure-database-mail"></a>Configurar o Database Mail
  Este tópico descreve como habilitar e configurar o Database Mail usando o Assistente para Configuração do Database Mail e cria um script de Configuração do Database Mail usando modelos.  
  

  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Use a opção **DatabaseMail XPs** para habilitar o Database Mail neste servidor. Para obter mais informações, confira o tópico de referência [Opção Database Mail XPs de configuração de servidor](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) .  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 A habilitação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker em qualquer banco de dados exige um bloqueio de banco de dados. Se o Service Broker tiver sido desabilitado no **msdb**, para habilitar o Database Mail primeiro interrompa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para que o Service Broker possa obter o bloqueio necessário.  
  
###  <a name="Security"></a> Segurança  
 Para configurar o Database Mail, é necessário ser membro da função de servidor fixa **sysadmin** . Para enviar Database Mail, é necessário ser membro da função de banco de dados **DatabaseMailUserRole** no banco de dados **msdb** .  
  
##  <a name="SSMSProcedure"></a> Usando o assistente para configuração do Database Mail  
 **Para configurar o Database Mail usando um assistente**  
  
1.  No Pesquisador de Objetos, expanda o nó da instância desejada para configurar o Database Mail.  
  
2.  Expanda o nó **Gerenciamento** .  
  
3.  Clique estreito **Database Mail**e, em seguida, clique em **configurar o Database Mail**.  
  
4.  Conclua os diálogos do Assistente:  
  

  
  
  
###  <a name="Welcome"></a> Página de boas-vindas  
 Esta página descreve as etapas de configuração do Database Mail.  
  
 **Não mostrar esta página novamente** – Marque essa opção para não exibir a página de boas-vindas no futuro novamente.  
  
 **Avançar** – Segue para a página **Selecionar uma tarefa de configuração** .  
  
 **Cancelar** – Encerra o assistente sem configurar o Database Mail  
  
 
  
###  <a name="ConfigTask"></a> Selecionar Tarefa de Configuração  
 Use a página **Selecionar Tarefa de Configuração** para indicar qual tarefa você concluirá sempre que usar o assistente. Se você mudar de ideia antes de concluir o assistente, use o botão **Voltar** para voltar para essa página e selecionar outra tarefa.  
  
> [!NOTE]  
>  Se o Database Mail não foi habilitado, você receberá a mensagem: **O recurso Database Mail não está disponível.  Deseja habilitar este recurso?** Responder **Sim**equivale a habilitar o Database Mail usando a [opção Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) do procedimento armazenado do sistema **sp_configure** .  
  
 **Instalar Database Mail executando as seguintes tarefas**  
 Execute todas as tarefas exigidas para instalar o Database Mail pela primeira vez. Essa opção inclui todas as outras três opções.  
  
 **Gerenciar contas e perfis do Database Mail**  
 Crie novas contas e perfis do Database Mail ou exiba, altere ou exclua contas e perfis existentes do Database Mail.  
  
 **Gerenciar segurança do perfil**  
 Configure quais usuários têm acesso a perfis do Database Mail.  
  
 **Exibir ou alterar parâmetros do sistema**  
 Configure parâmetros de sistema do Database Mail, como o tamanho máximo de arquivo para anexos.  
  

  
###  <a name="NewAccount"></a> Página Nova Conta  
 Use esta página para criar uma nova conta do Database Mail. Uma conta do Database Mail contém informações para enviar email a um servidor SMTP.  
  
 Uma conta do Database Mail contém as informações que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para enviar mensagens de email a um servidor SMTP. Cada conta contém informações de um servidor de email.  
  
 Uma conta do Database Mail só é usada no Database Mail. Uma conta do Database Mail não corresponde a uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou uma conta do Microsoft Windows. O Database Mail pode ser enviado usando as credenciais do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]usando outras credenciais que você forneça ou anonimamente. Quando a autenticação básica é usada, o nome do usuário e a senha em uma conta do Database Mail só são usados para autenticação no servidor de email. Uma conta não precisa corresponder a um usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a um usuário no computador que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Nome da conta**  
 Digite o nome da nova conta.  
  
 **Descrição**  
 Digite uma descrição da conta. A descrição é opcional.  
  
 **Endereço de email**  
 Digite o nome do endereço de email da conta. Este é o endereço de email da conta que o enviou. Por exemplo, uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode enviar emails do endereço SqlAgent@Adventure-Works.com.  
  
 **Nome para exibição**  
 Digite o nome que será exibido nas mensagens de email enviadas por essa conta. O nome para exibição é opcional. Este é o nome exibido em mensagens enviadas desta conta. Por exemplo, uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode exibir o nome “SQL Server Agent Automated Mailer” em mensagens de email.  
  
 **Email de resposta**  
 Digite o endereço de email que será usado em respostas a mensagens de email enviadas por esta conta. O email de resposta é opcional. Por exemplo, respostas a uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent podem ir para o administrador de banco de dados, danw@Adventure-Works.com.  
  
 **Nome do servidor**  
 Digite o nome ou o endereço IP do servidor SMTP que a conta usa para enviar email. Geralmente, está em um formato semelhante a `smtp.` *< sua_empresa >*`.com`. Para obter mais ajuda sobre isso, consulte o administrador de mail.  
  
 **Número da porta**  
 Digite o número da porta do servidor SMTP para a conta. A maioria dos servidores SMTP usa a porta 25.  
  
 **Esse servidor requer uma conexão segura (SSL)**  
 Criptografa a comunicação usando o Protocolo SSL.  
  
 **Autenticação do Windows usando as credenciais do serviço Mecanismo de Banco de Dados**  
 A conexão é feita com o servidor SMTP usando as credenciais configuradas para o serviço do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] .  
  
 **Autenticação Básica**  
 Especifique o nome do usuário e a senha exibidos pelo servidor SMTP.  
  
 **Nome de usuário**  
 Digite o nome de usuário que o Database Mail usa para fazer logon no servidor SMTP. O nome do usuário será necessário se o servidor SMTP exigir autenticação básica.  
  
 **Senha**  
 Digite a senha que o Database Mail usa para fazer logon no servidor SMTP. A senha será necessária se o servidor SMTP exigir autenticação básica.  
  
 **Confirmar senha**  
 Digite a senha novamente para confirmar. A senha será necessária se o servidor SMTP exigir autenticação básica.  
  
 **Autenticação anônima**  
 O email é enviado ao servidor SMTP sem credenciais de logon. Use essa opção quando o servidor SMTP não exigir autenticação.  
  
 
  
###  <a name="ExistingAccount"></a> Página Gerenciar Conta Existente  
 Use esta página para gerenciar uma conta de Database Mail existente.  
  
 **Nome da conta**  
 Selecione a conta a exibir, atualizar ou excluir.  
  
 **Delete (excluir)**  
 Excluir a conta selecionada. Você deve remover esta conta de perfis associados, ou excluir esses perfis, antes de excluir a conta selecionada.  
  
 **Descrição**  
 Exiba ou atualize a descrição da conta. A descrição é opcional.  
  
 **Endereço de email**  
 Exiba ou atualize o nome do endereço de email da conta. Este é o endereço de email da conta que o enviou. Por exemplo, uma conta do Microsoft SQL Server Agent pode enviar email do endereço **SqlAgent@Adventure-Works.com**.  
  
 **Nome para exibição**  
 Exiba ou atualize o nome a ser exibido em mensagens de email enviadas desta conta. O nome para exibição é opcional. Este é o nome exibido em mensagens enviadas desta conta. Por exemplo, uma conta do SQL Server Agent pode exibir o nome **SQL Server Agent Automated Mailer** em mensagens de email.  
  
 **Email de resposta**  
 Exiba ou atualize o endereço de email que será usado em respostas a mensagens de email enviadas desta conta. O email de resposta é opcional. Por exemplo, respostas a uma conta do SQL Server Agent podem ir para o administrador de banco de dados, **danw@Adventure-Works.com**.  
  
 **Nome do servidor**  
 Exibe ou atualiza o nome do servidor SMTP que a conta usa para enviar email. Geralmente, está em um formato semelhante a **smtp.<your_company>.com**. Para obter mais ajuda sobre isso, consulte o administrador de mail.  
  
 **Número da porta**  
 Exiba ou atualize o número da porta do servidor SMTP desta conta. A maioria dos servidores SMTP usa a porta 25.  
  
 **Esse servidor requer uma conexão segura (SSL)**  
 Criptografa a comunicação usando o Protocolo SSL.  
  
 **Autenticação do Windows usando as credenciais do serviço Mecanismo de Banco de Dados**  
 A conexão é feita com o servidor SMTP usando as credenciais configuradas para o serviço do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] .  
  
 **Autenticação Básica**  
 Especifique o nome do usuário e a senha exibidos pelo servidor SMTP.  
  
 **Nome de usuário**  
 Exiba ou atualize o nome do usuário que o Database Mail usa para fazer logon no servidor SMTP. O nome do usuário será necessário se o servidor SMTP exigir autenticação básica.  
  
 **Senha**  
 Altere a senha que o Database Mail usa para fazer logon no servidor SMTP. A senha será necessária se o servidor SMTP exigir autenticação básica.  
  
 **Confirmar senha**  
 Digite a senha novamente para confirmar. A senha será necessária se o servidor SMTP exigir autenticação básica.  
  
 **Autenticação anônima**  
 O email é enviado ao servidor SMTP sem credenciais de logon. Use essa opção quando o servidor SMTP não exigir autenticação.  
  

  
###  <a name="NewProfile"></a> Página Novo Perfil  
 Use essa página para criar um perfil do Database Mail. Um perfil do Database Mail é uma coleção de contas do Database Mail. Os perfis melhoram a confiabilidade nos casos em que um servidor de email não pode ser acessado, oferecendo contas alternativas do Database Mail. É necessário pelo menos uma conta do Database Mail. Para obter mais informações sobre como definir a prioridade das contas do Database Mail no perfil, veja [Criar um perfil do Database Mail](create-a-database-mail-profile.md).  
  
 Use os botões **Mover para Cima** e **Mover para Baixo** para alterar a ordem na qual as contas do Database Mail são usadas. Essa ordem é determinada por um valor chamado número de sequência. **Mover para Cima** diminui o número de sequência e **Mover para Baixo** aumenta o número de sequência. O número de sequência determina a ordem na qual o Database Mail usa as contas no perfil. Para uma nova mensagem de email, o Database Mail inicia com a conta que tem o número de sequência mais baixo. Se essa conta falhar, o Database Mail usará a conta com o próximo número de sequência mais alto, e assim por diante, até que o Database Mail envie a mensagem com êxito ou a conta com o número de sequência mais alto falhe. Se a conta com o número de sequência mais alto falhar, o Database Mail pausará as tentativas de envio de email pelo tempo configurado no parâmetro **AccountRetryDelay** no Database Mail e iniciará o processo de tentar enviar o email novamente, começando pelo número de sequência mais baixo. Use o parâmetro **AccountRetryAttempts** do Database Mail para configurar o número de vezes em que o processo de email externo tenta enviar a mensagem de email usando cada conta no perfil especificado. Você pode configurar os parâmetros **AccountRetryDelay** e **AccountRetryAttempts** na página **Configurar Parâmetros do Sistema** do Assistente para Configuração do Database Mail.  
  
 **Nome do perfil**  
 Digite o nome para o novo perfil. O perfil é criado com esse nome. Não use o nome de um perfil existente.  
  
 **Descrição**  
 Digite uma descrição para o perfil. A descrição é opcional.  
  
 **Contas SMTP**  
 Escolha uma ou mais contas para o perfil. A prioridade define a ordem na qual o Database Mail usa as contas. Se nenhuma conta for listada, é necessário clicar em **Adicionar** para continuar e adicionar uma nova conta SMTP.  
  
 **Adicionar**  
 Adiciona uma conta ao perfil.  
  
 **Remover**  
 Remove a conta selecionada do perfil.  
  
 **Mover para Cima**  
 Aumente a prioridade da conta selecionada.  
  
 **Mover para Baixo**  
 Diminua a prioridade da conta selecionada.  
  

  
###  <a name="ExistingProfile"></a> Página Gerenciar Perfil Existente  
 Use esta página para gerenciar um perfil existente no Database Mail. Um perfil do Database Mail é uma coleção de contas do Database Mail. Os perfis melhoram a confiabilidade nos casos em que um servidor de email não pode ser acessado, oferecendo contas alternativas do Database Mail. É necessário pelo menos uma conta do Database Mail. Para obter mais informações sobre como definir a prioridade das contas do Database Mail no perfil, veja [Criar um perfil do Database Mail](create-a-database-mail-profile.md).  
  
 Use os botões **Mover para Cima** e **Mover para Baixo** para alterar a ordem na qual as contas do Database Mail são usadas. Essa ordem é determinada por um valor chamado número de sequência. **Mover para Cima** diminui o número de sequência e **Mover para Baixo** aumenta o número de sequência. O número de sequência determina a ordem na qual o Database Mail usa as contas no perfil. Para uma nova mensagem de email, o Database Mail inicia com a conta que tem o número de sequência mais baixo. Se essa conta falhar, o Database Mail usará a conta com o próximo número de sequência mais alto, e assim por diante, até que o Database Mail envie a mensagem com êxito ou a conta com o número de sequência mais alto falhe. Se a conta com o número de sequência mais alto falhar, o Database Mail pausará as tentativas de envio de email pelo tempo configurado no parâmetro **AccountRetryDelay** no Database Mail e iniciará o processo de tentar enviar o email novamente, começando pelo número de sequência mais baixo. Use o parâmetro **AccountRetryAttempts** do Database Mail para configurar o número de vezes em que o processo de email externo tenta enviar a mensagem de email usando cada conta no perfil especificado. Você pode configurar os parâmetros **AccountRetryDelay** e **AccountRetryAttempts** na página **Configurar Parâmetros do Sistema** do Assistente para Configuração do Database Mail.  
  
 **Nome do perfil**  
 Selecione o nome do perfil a gerenciar.  
  
 **Delete (excluir)**  
 Exclui o perfil selecionado. Você será solicitado a selecionar **Sim** para excluir o perfil selecionado e para optar por falhar em todas as mensagens não enviadas ou a selecionar **Não** para excluir o perfil selecionado apenas se não houver mensagens não enviadas.  
  
 **Descrição**  
 Exibe ou altera a descrição do perfil selecionado. A descrição é opcional.  
  
 **Contas SMTP**  
 Escolha uma ou mais contas para o perfil. A prioridade de failover define a ordem na qual o Database Mail usa a conta no caso de um failover.  
  
 **Adicionar**  
 Adiciona uma conta ao perfil.  
  
 **Remover**  
 Remove a conta selecionada do perfil.  
  
 **Mover para Cima**  
 Aumenta a prioridade de failover da conta selecionada.  
  
 **Mover para Baixo**  
 Diminui a prioridade de failover da conta selecionada.  
  
 **Prioridade**  
 Exibe a prioridade de failover atual da conta.  
  
 **Nome da conta**  
 Exibe o nome da conta.  
  
 **E-mail Address**  
 Exibe o endereço de email da conta.  
  

  
###  <a name="AddAccount"></a> Add Account to Profile Page  
 Use esta página para escolher a conta a ser adicionada ao perfil. Escolha uma conta existente na caixa **Nome da conta** ou clique em **Nova Conta**.  
  
 **Nome da conta**  
 Selecione o nome da conta a ser adicionada ao perfil.  
  
 **Endereço de email**  
 Visualize o endereço de email da conta selecionada. Você não pode alterar o endereço de email nesta página. Para alterar o endereço de email dessa conta, volte para a página principal do assistente e selecione a opção **Gerenciar contas e perfis do Database Mail** .  
  
 **Nome do servidor**  
 Visualize o nome do servidor de email da conta selecionada. Você não pode alterar o nome do servidor nesta página. Para alterar o nome do servidor dessa conta, volte para a página principal do assistente e selecione a opção **Gerenciar contas e perfis do Database Mail** .  
  
 **Nova Conta**  
 Crie uma conta nova.  
  

  
###  <a name="AccountsProfiles"></a> Página Gerenciar Contas e Perfis  
 Use esta página para escolher uma tarefa para gerenciar um perfil ou conta.  
  
 **Criar uma conta nova**  
 Crie uma conta nova.  
  
 **Visualizar, alterar ou excluir uma conta existente**  
 Gerencie ou exclua uma conta existente.  
  
 **Criar um novo perfil**  
 Crie um novo perfil.  
  
 **Exibir, alterar ou excluir um perfil existente. Também é possível gerenciar contas associadas ao perfil.**  
 Atualize ou exclua um perfil existente. Essa opção também permite gerenciar contas associadas ao perfil.  
  

  
###  <a name="ProfileSecurityPublic"></a> Gerenciar Segurança do Perfil, guia Público  
 Use essa página para configurar um perfil público.  
  
 Perfis são públicos ou privados. Um perfil privado é acessível somente para usuários ou funções específicas. Um perfil público permite a qualquer usuário ou função com acesso ao banco de dados do host de email (**msdb**) enviar um email usando esse perfil.  
  
 Um perfil pode ser um perfil padrão. Nesse caso, usuários ou funções podem enviar e-mails por meio do perfil sem especificá-lo explicitamente. Se o usuário ou função que envia a mensagem de e-mail tiver um perfil privado padrão, o Database Mail irá utilizá-lo. Se o usuário ou função não tiver nenhum perfil privado padrão, **sp_send_dbmail** usará o perfil público padrão para o banco de dados **msdb** . Se não houver nenhum perfil privado padrão para o usuário ou função e nenhum perfil público padrão para o banco de dados, **sp_send_dbmail** retornará um erro. Somente um perfil pode ser marcado como o perfil padrão.  
  
 **Público**  
 Selecione essa opção para tornar público o perfil especificado.  
  
 **Profile Name**  
 Exibe o nome do perfil.  
  
 **Perfil Padrão**  
 Selecione essa opção para transformar o perfil especificado em perfil padrão.  
  
 **Mostrar somente os perfis públicos existentes**  
 Selecione essa opção para mostrar somente perfis públicos no banco de dados especificado.  
  

  
###  <a name="ProfileSecurityPrivate"></a> Gerenciar Segurança do Perfil, guia Particular  
 Use essa página para configurar um perfil privado.  
  
 Perfis são públicos ou privados. Um perfil privado é acessível somente para usuários ou funções específicas. Um perfil público permite a qualquer usuário ou função com acesso ao banco de dados do host de email (**msdb**) enviar um email usando esse perfil.  
  
 Um perfil pode ser um perfil padrão. Nesse caso, usuários ou funções podem enviar e-mails por meio do perfil sem especificá-lo explicitamente. Se o usuário ou função que envia a mensagem de e-mail tiver um perfil privado padrão, o Database Mail irá utilizá-lo. Se o usuário ou função não tiver nenhum perfil privado padrão, **sp_send_dbmail** usará o perfil público padrão para o banco de dados **msdb** . Se não houver nenhum perfil privado padrão para o usuário ou função e nenhum perfil público padrão para o banco de dados, **sp_send_dbmail** retornará um erro.  
  
 **Nome de usuário**  
 Selecione o nome de um usuário ou função no banco de dados **msdb** .  
  
 **Acesso**  
 Selecione se o usuário ou função tem acesso ao perfil especificado.  
  
 **Nome do perfil**  
 Exibir nome do perfil.  
  
 **É Perfil Padrão**  
 Selecione se o perfil é o perfil padrão para o usuário ou função. Cada usuário ou função pode ter apenas um perfil de padrão.  
  
 **Mostrar somente os perfis particulares existentes deste usuário**  
 Selecione essa opção para exibir apenas perfis aos quais o usuário ou função especificados já tenham acesso.  
  

  
###  <a name="SystemParameters"></a> Configurar Parâmetros do Sistema  
 Use esta página para especificar parâmetros de sistema do Database Mail. Exibe os parâmetros de sistema e o valor atual de cada parâmetro. Selecione um parâmetro para exibir uma breve descrição no painel de informações.  
  
 **Tentativas de Repetição de Conta**  
 O número de vezes que o processo de email externo tenta enviar a mensagem de email usando cada conta no perfil especificado.  
  
 **Atraso na Repetição de Conta (segundos)**  
 O tempo, em segundos em que o processo de email externo espera, depois de tentar enviar uma mensagem usando todas as contas no perfil, antes de tentar todas as contas novamente.  
  
 **Tamanho Máximo do Arquivo (Bytes)**  
 O tamanho máximo de um anexo, em bytes.  
  
 **Extensões de Arquivo de Anexo Proibidas**  
 Uma lista separada por vírgula de extensões que não podem ser enviadas como um anexo a uma mensagem de email. Clique no botão Procurar (**...**) para adicionar outras extensões.  
  
 **Tempo Mínimo de Vida do Executável do Database Mail (segundos)**  
 O período mínimo de tempo, em segundos, que o processo de email externo permanece ativo. O processo permanece ativo enquanto houver emails na fila do Database Mail. Esse parâmetro especifica o tempo que o processo permanece ativo se não houver nenhuma mensagem a processar.  
  
 **Nível de log**  
 Especifique quais mensagens são registradas no log do Database Mail. Os valores possíveis são:  
  
-   Normal - só registra erros  
  
-   Estendido - registra erros, avisos e mensagens informativas  
  
-   Detalhado - registra erros, avisos, mensagens informativas, mensagens de êxito e mensagens internas adicionais. Use log detalhado para solucionar problemas.  
  
 O valor padrão é Estendido.  
  
 **Redefinir Tudo**  
 Selecione esta opção para restaurar os valores da página aos valores padrão originais.  
  

  
###  <a name="CompleteWizard"></a> Página Concluir o Assistente  
 Use essa página para ver as ações que o **Assistente para Configuração do Database Mail** executará. Nenhuma alteração é feita até que você conclua o assistente.  
  

  
###  <a name="TestEmail"></a> Send Test E-Mail Page  
 Use a página **Enviar Email de Teste de***<nome_da_instância>* para enviar uma mensagem de email usando o perfil especificado do Database Mail. Só os membros da função de servidor fixa **sysadmin** podem enviar email de teste usando essa página.  
  
 **Perfil do Database Mail**  
 Selecione um perfil da lista do Database Mail. Esse é um campo obrigatório. Se nenhum perfil for mostrado, não há nenhum perfil ou você não tem permissão para um perfil. Use o **Assistente para Configuração do Database Mail** para criar e configurar perfis. Se nenhum perfil for listado, use o Assistente para Configuração do Database Mail para criar um perfil para seu uso.  
  
 **Para**  
 O endereço de email dos destinatários da mensagem. Exige-se pelo menos um destinatário.  
  
 **Assunto**  
 A linha de assunto para o email de teste. Altere o assunto padrão para identificar melhor seu email para solucionar problemas.  
  
 **Corpo**  
 O corpo do email de teste. Altere o assunto padrão para identificar melhor seu email para solucionar problemas.  
  
 A caixa de diálogo **Email de Teste do Database Mail** confirma que o Database Mail tentou enviar a mensagem de teste e fornece a **mailitem_id** para a mensagem de teste de email. Confirme com o destinatário para determinar se o email foi recebido. Geralmente, o email é recebido dentro de poucos minutos, mas o email pode ser atrasado por um desempenho lento da rede, por uma lista de pendências de mensagens no servidor de email ou caso o servidor esteja temporariamente indisponível. Use **mailitem_id** para solucionar problemas.  
  
 **Enviar email**  
 A **mailitem_id** da mensagem de teste de email.  
  
 **Solucionar problemas**  
 Clique para abrir os Manuais Online no tópico [Solucionando problemas do Database Mail](http://msdn.microsoft.com/library/ms188663.aspx).  
  

  
##  <a name="Template"></a> Usando modelos  
 **Para criar um script de configuração do Database Mail**  
  
1.  No menu **Exibir** , selecione **Explorador de Modelos**.  
  
2.  Na janela **Explorador de Modelos** , expanda a pasta **Database Mail** .  
  
3.  Clique duas vezes em **Configuração Simples do Database Mail**. O modelo é aberto em uma nova janela de consulta.  
  
4.  No menu **Consulta** , selecione **Especificar Valores para Parâmetros de Modelo**. A janela **Substituir Parâmetros de Modelo** é exibida.  
  
5.  Digite os valores para **profile_name**, **account_name**, **SMTP_servername**, **email_address**e **display_name**. O SQL Server Management Studio preenche o modelo com os valores fornecidos por você.  
  
6.  Execute o script para criar a configuração.  
  
7.  O script não concede nenhum acesso de usuário de banco de dados ao perfil. Portanto, por padrão, o perfil pode ser usado apenas por membros da função de segurança fixa **sysadmin**. Para obter mais informações sobre como conceder acesso a perfis, veja [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql)  
  
  
