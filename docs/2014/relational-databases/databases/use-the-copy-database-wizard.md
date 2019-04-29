---
title: Usar o Assistente para Copiar Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.cdw.transfermethod.f1
- sql12.swb.cdw.welcome.f1
- sql12.swb.cdw.packageconfiguration.f1
- sql12.swb.cdw.schedule.f1
- sql12.swb.cdw.destination.f1
- sql12.swb.cdw.complete.f1
- sql12.swb.cdw.destinationconfiguration.f1
- sql12.swb.cdw.selectdatabaseobjects.f1
- sql12.swb.cdw.databases.f1
- sql12.swb.cdw.source.f1
- sql12.swb.cdw.locationofsourcedbfiles.f1
helpviewer_keywords:
- Copy Database Wizard
- starting Copy Database Wizard
ms.assetid: 7a999fc7-0a26-4a0d-9eeb-db6fc794f3cb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e72b960db0fd5b733119cafeca98f124eaa15f38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62871133"
---
# <a name="use-the-copy-database-wizard"></a>Usar o Assistente para Copiar Banco de Dados
  O Assistente para Copiar Banco de Dados lhe permite migrar ou copiar bancos de dados e seus objetos facilmente de um servidor para outro, sem inatividade do servidor. Também é possível atualizar bancos de dados de uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Com esse assistente, é possível fazer o seguinte:  
  
-   Selecionar um servidor de origem e de destino.  
  
-   Selecionar bancos de dados para mover, copiar ou atualizar.  
  
-   Especificar o local de arquivo para os bancos de dados.  
  
-   Criar logons no servidor de destino.  
  
-   Copiar objetos, trabalhos, procedimentos armazenados definidos pelo usuário e mensagens de erro de suporte adicionais.  
  
-   Agendar a migração ou cópia dos bancos de dados.  
  
 Além de copiar bancos de dados, é possível copiar os metadados associados, como, por exemplo, logons e objetos do banco de dados **mestre** exigidos por um banco de dados copiado.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Usando o Assistente de cópia de banco de dados para:**  
  
     [Copiar, mover ou atualizar bancos de dados](#Copy_Move)  
  
-   **Acompanhamento: após a atualização:**  
  
     [Depois de atualizar um banco de dados do SQL Server](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O Assistente para Copiar Banco de Dados não está disponível na edição Express.  
  
-   O Assistente para Copiar Banco de Dados não pode ser usado para copiar ou mover os bancos de dados a seguir.  
  
    -   Bancos de dados do sistema  
  
    -   Bancos de dados marcados para replicação.  
  
    -   Bancos de dados marcados como Inacessível, Carregando, Offline, Recuperando, Suspeito ou em Modo de Emergência.  
  
-   Depois que um banco de dados é atualizado, ele não pode ser rebaixado para uma versão anterior.  
  
-   Se você selecionar a opção **Migrar** , o assistente excluirá o banco de dados de origem automaticamente após migrá-lo. Se você selecionar **Copiar** , o Assistente para Copiar Banco de Dados não excluirá o banco de dados de origem.  
  
-   Se você usar o método [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object para mover o catálogo de texto completo, deverá repopular o índice após a movimentação.  
  
-   O método desanexar-e-anexar desanexa o banco de dados, migra ou copia os arquivos .mdf, .ndf e .ldf do banco de dados e os reanexa ao banco de dados em um novo local. Ao utilizar o método desanexar-e-anexar, para evitar perda ou inconsistência de dados, as sessões ativas não podem ser anexadas ao banco de dados que está sendo migrado ou copiado. Se houver alguma sessão ativa, o Assistente para Copiar Banco de Dados não executará a operação de migração ou cópia. No método [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object, permitem-se sessões ativas porque o banco de dados nunca é colocado offline.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Verifique se o SQL Server Agent foi iniciado no servidor de destino.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Para garantir o desempenho perfeito de um banco de dados atualizado, execute sp_updatestats (atualização de estatísticas) nele.  
  
-   Ao copiar um banco de dados para outra instância do servidor, para oferecer uma experiência consistente aos usuários e aplicativos, pode ser necessário recriar alguns ou todos os metadados do banco de dados, como logons e trabalhos, na outra instância de servidor. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ser membro da função de servidor fixa **sysadmin** em ambos os servidores, de origem e de destino.  
  
##  <a name="Copy_Move"></a> Copiar, mover ou atualizar bancos de dados  
  
1.  Na [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de objetos, expanda **bancos de dados**, clique com botão direito a um banco de dados, aponte para **tarefas**e, em seguida, clique em **copiar banco de dados**.  
  
2.  Na página **Selecionar um Servidor de Origem** , especifique o servidor com o banco de dados que deseja mover ou copiar e digite as informações de logon. Depois de selecionar o método de autenticação e digitar as informações de logon, clique em **Avançar** para estabelecer conexão com o servidor de origem. Essa conexão permanece aberta durante a sessão.  
  
     **Servidor de origem**  
     Selecione o nome do servidor no qual o banco de dados ou bancos de dados que você deseja mover ou copiar estão localizados, ou clique no botão Procurar (**...** ) botão para localizar o servidor desejado. O servidor deve ser pelo menos [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
     **Usar Autenticação do Windows**  
     Permite que um usuário conecte por meio de uma conta de usuário [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
     **Usar Autenticação do SQL Server**  
     Permite que um usuário conecte-se fornecendo um nome de usuário e uma senha de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Nome de usuário**  
     Digite o nome do usuário com o qual se conectar. Essa opção estará disponível somente se você decidiu se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Senha**  
     Digite a senha do logon. Essa opção estará disponível somente se você decidiu conectar-se usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Próximo**  
     Conecta ao servidor e valida o usuário. Esse processo verifica se o usuário é membro da função de servidor fixa **sysadmin** no computador selecionado.  
  
3.  Na página **Selecione um Servidor de Destino** , especifique o servidor para o qual o banco de dados será movido ou copiado. Se você definiu os servidores de origem e destino com a mesma instância de servidor, fará uma cópia de um banco de dados. Nesse caso, renomeie o banco de dados em um ponto posterior do assistente. O nome do banco de dados de origem poderá ser usado somente para o banco de dados copiado ou migrado se não houver conflitos de nome no servidor de destino. Se houver conflitos de nome, será preciso resolvê-los manualmente no servidor de destino para poder usar o nome do banco de dados de origem nele.  
  
     **Servidor de destino**  
     Selecione o nome do servidor ao qual o banco de dados ou bancos de dados serão movidos ou copiado ou clique no botão Procurar (**...** ) botão para localizar um servidor de destino.  
  
    > [!NOTE]  
    >  Você pode usar um destino que está em um servidor clusterizado; o Assistente para Copiar Banco de Dados garantirá que você selecionará somente unidades compartilhadas de um servidor de destino clusterizado.  
  
     **Usar Autenticação do Windows**  
     Permite que um usuário conecte por meio de uma conta de usuário [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
     **Usar Autenticação do SQL Server**  
     Permite que um usuário conecte-se fornecendo um nome de usuário e uma senha de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Nome de usuário**  
     Digite o nome do usuário com o qual se conectar. Essa opção estará disponível apenas se você selecionou a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Senha**  
     Digite a senha do logon. Essa opção estará disponível apenas se você selecionou a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Próximo**  
     Conecta ao servidor e valida o usuário. Esse processo verifica se o usuário tem as permissões listadas acima nos computadores selecionados.  
  
4.  Na página **Selecione o Método de Transferência** , selecione o método de transferência.  
  
     **Usar o método desanexar e anexar**  
     Desanexa o banco de dados do servidor de origem, copia os arquivos do banco de dados (.mdf, .ndf e . ldf) para o servidor de destino e anexa o banco de dados ao servidor de destino. Esse método é geralmente o mais rápido porque o trabalho principal é ler o disco de origem e gravar o disco de destino. Nenhuma lógica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é exigida para criar objetos dentro do banco de dados ou para criar estruturas de armazenamento de dados. Porém, este método pode ser mais lento se o banco de dados contiver uma grande quantidade de espaço alocado, mas não utilizado. Por exemplo, um banco de dados novo e praticamente vazio que seja criado alocando 100 MB, copia todos os 100 MB, mesmo que apenas 5 MB estejam completos.  
  
    > [!NOTE]  
    >  Esse método torna o banco de dados indisponível para os usuários durante a transferência.  
  
     **Se ocorrer uma falha, anexar novamente o banco de dados de origem**  
     Quando um banco de dados é copiado, os arquivos do banco de dados original são sempre anexados novamente ao servidor de origem. Use essa caixa para anexar novamente os arquivos originais ao banco de dados de origem se não for possível mover um banco de dados.  
  
     **Usar o método SQL Management Object**  
     Esse método lê a definição de cada objeto de banco de dados no banco de dados de origem e cria cada objeto no banco de dados de destino. Depois ele transfere os dados das tabela de origem para as tabelas de destino, recriando os índices e os metadados.  
  
    > [!NOTE]  
    >  Os usuários do banco de dados podem continuar a acessar o banco de dados durante a transferência.  
  
5.  Na página **Selecionar Banco de Dados** , selecione o banco ou os bancos de dados que deseja mover ou copiar do servidor de origem para o servidor de destino. Consulte [Limitações e restrições](#Restrictions) na seção 'Antes de começar' deste tópico.  
  
     **Migrar**  
     Mova o banco de dados para o servidor de destino.  
  
     **Copiar**  
     Copie o banco de dados no servidor de destino.  
  
     **Origem**  
     Exibe os bancos de dados existentes no servidor de origem.  
  
     **Status**  
     Exibe **Okey** se o banco de dados pode ser movido. Caso contrário, exibe a razão pela qual o banco de dados não pode ser movido.  
  
     **Atualizar**  
     Atualize a lista de bancos de dados.  
  
     **Próximo**  
     Inicie o processo de validação e avance para a próxima tela.  
  
6.  Na página **Configurar Banco de Dados de Destino** , altere o nome do banco de dados, se apropriado, e especifique o local e os nomes dos arquivos de banco de dados. Essa página aparece uma vez para cada banco de dados que é movido ou copiado.  
  
7.  Na página **Selecionar Objetos de Banco de Dados** , selecione os objetos para incluir na operação de movimentação ou cópia. Essa página está disponível apenas quando os servidores de origem e de destino forem diferentes. Para incluir um objeto, clique no nome do objeto na caixa **Objetos relacionados disponíveis** e clique no botão **>>** para mover o objeto para a caixa **Objetos relacionados selecionados** . Para excluir um objeto, clique no nome do objeto na caixa **Objetos relacionados selecionados** e clique no botão **<\<** para mover o objeto para a caixa **Objetos relacionados disponíveis** . Por padrão, são transferidos todos os objetos de cada tipo selecionado. Para escolher objetos individuais de qualquer tipo, clique no botão de reticências ao lado de qualquer tipo de objeto na caixa **Objetos relacionados selecionados** . Isso abre uma caixa de diálogo onde você pode selecionar objetos individuais.  
  
     **Logons (todos os logons em tempo de execução)**  
     Inclua logons na operação de mover ou copiar. Selecionadas por padrão.  
  
     **Procedimentos armazenados do banco de dados mestre**  
     Inclua procedimentos armazenados do **mestre** na operação de mover ou copiar.  
  
    > [!NOTE]  
    >  Procedimentos armazenados estendidos e seus DLLs associados não são qualificados para cópia automatizada.  
  
     **trabalhos do SQL Server Agent**  
     Incluir trabalhos a partir de **msdb** na operação de mover ou copiar.  
  
     **Mensagens de erro definidas pelo usuário**  
     Inclua mensagens de erro definidas pelo usuário na operação de mover e copiar.  
  
     **Pontos de extremidade**  
     Inclua pontos de extremidade definidos no banco de dados de origem.  
  
     **Catálogo de texto completo**  
     Inclua catálogos de texto completo do banco de dados de origem.  
  
     **Pacote SSIS**  
     Inclua pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] definidos no banco de dados de origem.  
  
     **Descrição**  
     Uma descrição do objeto .  
  
8.  Na página **Local do Arquivos de Banco de Dados de Origem** , especifique um compartilhamento de sistema de arquivos que contém os arquivos de banco de dados no servidor de origem. Isso será necessário se as instâncias de servidor de origem e destino estiverem em computadores diferentes.  
  
     **Backup de banco de dados**  
     Exibe o nome de cada banco de dados que é movido.  
  
     **Local da pasta**  
     Especifique o local dos arquivos de banco de dados de origem no sistema de arquivos.  
  
     Por exemplo: C:\Program Files\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\DATA  
  
     **Compartilhamento de arquivo no servidor de origem**  
     Especifique o local dos arquivos de banco de dados de origem como um caminho de compartilhamento de arquivos.  
  
     Por exemplo: "\\\\*nome_do_servidor*\C$\Program Files\Microsoft SQL Server\MSSQL110. MSSQLSERVER\MSSQL\Data  
  
9. O Assistente para Copiar Banco de Dados cria um pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] para transferir o banco de dados. Na página **Configurar o Pacote** , personalize o pacote, se apropriado.  
  
     **Local do pacote**  
     Exibe onde o pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] será gravado.  
  
     **Nome do pacote**  
     Insira um nome para o pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
     **Opções de log**  
     Selecione se as informações de log serão armazenadas no log de eventos do Windows ou em um arquivo de texto.  
  
     **Caminho do arquivo de log de erros**  
     Forneça um caminho para o local do arquivo de log. Essa opção só estará disponível se a opção de log de arquivo de texto for selecionada.  
  
10. Na página **Agendar o Pacote** , especifique quando você quer que a operação de movimentação ou cópia seja iniciada. Se você não for um administrador do sistema, deverá especificar uma conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que tenha acesso ao subsistema de execução de Pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS).  
  
     **Run immediately**  
     Iniciar a operação de mover ou copiar depois de clicar em **próxima**.  
  
     **Agenda**  
     Iniciar a operação de mover ou copiar mais tarde. As configurações de agenda atuais aparecem na caixa de descrição. Para alterar a agenda, clique em **Alterar**.  
  
     **Alteração**  
     Abra o **nova agenda de trabalho** caixa de diálogo.  
  
     **Conta proxy do Integration Services**  
     Selecione uma conta proxy disponível. Para agendar a transferência, deve haver pelo menos uma conta proxy disponível para o usuário, configurada com permissão para o subsistema de **execução do pacote SQL Server Integration Services** .  
  
     Para criar uma conta proxy para [!INCLUDE[ssIS](../../includes/ssis-md.md)] pacote de execução, no Pesquisador de objetos, expanda **SQL Server Agent**, expanda **Proxies**, clique com botão direito **execução de pacotes do SSIS**e, em seguida, clique em **novo Proxy**.  
  
     Os membros da função de servidor fixa **sysadmin** podem selecionar a **Conta de Serviço do SQL Server Agent**que tenha as permissões necessárias.  
  
11. Na página **Concluir o Assistente** , confira o resumo das opções selecionadas. Clique em **Voltar** para alterar uma opção. Clique em **Concluir** para criar o banco de dados. Durante a transferência, a página **Executando operação** monitora informações de status sobre a execução do **Assistente para Copiar Banco de Dados**.  
  
     **Ação**  
     Lista cada ação que está sendo executada.  
  
     **Status**  
     Indica se a ação como um todo obteve êxito ou falhou.  
  
     **Mensagem**  
     Fornece qualquer mensagem que retornou de cada etapa.  
  
##  <a name="FollowUp"></a> Acompanhamento: Depois de atualizar um banco de dados do SQL Server  
 Após o uso do Assistente para Copiar Banco de Dados para atualizar um banco de dados de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados é disponibilizado imediatamente e é atualizado de forma automática. Se o banco de dados tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices dependendo da configuração da propriedade de servidor **Opção de Atualização de Texto Completo** . Se a opção de atualização for definida como **Importar** ou **Recriar**, os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação pode levar várias horas, e a recriação pode ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida como **Importar**, se não houver um catálogo de texto completo disponível, os índices de texto completo associados serão recompilados. Para obter informações sobre como exibir ou alterar a configuração da propriedade **Full-Text Upgrade Option** , veja [Gerenciar e monitorar a pesquisa de texto completo para uma instância de servidor](../search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
 Se o nível de compatibilidade de um banco de dados de usuário era 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização. Se o nível de compatibilidade era 90, no banco de dados atualizado, o nível de compatibilidade será definido como 100, que é o nível de compatibilidade mais baixo com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar um banco de dados usando Desanexar e Anexar &#40;Transact-SQL&#41;](upgrade-a-database-using-detach-and-attach-transact-sql.md)   
 [Criar um proxy do SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
  
