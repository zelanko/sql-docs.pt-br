---
title: Criar servidores vinculados (Mecanismo de Banco de Dados do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: linked-servers
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.linkedserver.properties.general.f1
- sql13.swb.linkedserver.properties.security.f1
- sql13.swb.linkedserver.properties.provider.f1
- sql13.swb.linkedserver.properties.options.f1
helpviewer_keywords:
- linked servers [SQL Server], creating
ms.assetid: 3228065d-de8f-4ece-a9b1-e06d3dca9310
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bed6a93030c854c89ec32658ed086d6b0092a8c9
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984478"
---
# <a name="create-linked-servers-sql-server-database-engine"></a>Criar servidores vinculados (Mecanismo de Banco de Dados do SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Para ver o conteúdo relacionado a versões anteriores do SQL Server, consulte [Criar servidores vinculados (Mecanismo de Banco de Dados do SQL Server)](https://msdn.microsoft.com/library/ff772782(SQL.120).aspx).

  Este tópico mostra como criar um servidor vinculado e acessar dados de outro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Criar um servidor vinculado permite trabalhar com dados de várias origens. O servidor vinculado não precisa ser outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas esse é um cenário comum.  
  
##  <a name="Background"></a> Plano de fundo  
 Um servidor vinculado permite acesso a consultas distribuídas e heterogêneas em fontes de dados OLE DB. Depois que um servidor vinculado é criado, as consultas distribuídas podem ser executadas nesse servidor, e as consultas podem unir tabelas de mais de uma fonte de dados. Se o servidor vinculado estiver definido como uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], poderão ser executados procedimentos armazenados remotos.  
  
 Os recursos e argumentos necessários do servidor vinculado podem variar significativamente. Os exemplos neste tópico fornecem um exemplo típico, mas nem todas as opções são descritas. Para obter mais informações, consulte [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
##  <a name="Security"></a> Segurança  
  
### <a name="permissions"></a>Permissões  
 Ao usar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , exija a permissão **ALTER ANY LINKED SERVER** no servidor ou associação na função de servidor fixa **setupadmin** . Ao usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , requer a permissão **CONTROL SERVER** ou associação na função de servidor fixa **sysadmin** .  
  
##  <a name="Procedures"></a> Como criar um servidor vinculado  
 Você pode usar qualquer um dos itens a seguir:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-sql-server-management-studio"></a>Para criar um servidor vinculado para outra instância do SQL Server usando o SQL Server Management Studio  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o Pesquisador de Objetos, expanda **Objetos de Servidor**, clique com o botão direito do mouse em **Servidores Vinculados**e clique em **Novo Servidor Vinculado**.  
  
2.  Na página **Geral** , na caixa **Servidor vinculado** , digite o nome da instância do **SQL Server** à qual você está se vinculando.  
  
     **SQL Server**  
     Identifique o servidor vinculado como uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você usar esse método de definição de um servidor vinculado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o nome especificado em **Servidor vinculado** deverá ser o nome de rede do servidor. Da mesma forma, todas as tabelas recuperadas do servidor provêm do banco de dados padrão definido para logon no servidor vinculado.  
  
     **Outra fonte de dados**  
     Especifique um tipo de servidor OLE DB diferente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Clicar nessa opção ativa as opções abaixo dela.  
  
     **Provedor**  
     Selecione uma fonte de dados OLE DB na caixa de listagem. O provedor OLE DB é registrado com o PROGID fornecido no registro.  
  
     **Nome do produto**  
     Digite o nome do produto da fonte de dados OLE DB para adicionar como servidor vinculado.  
  
     **Fonte de dados**  
     Digite o nome da fonte de dados conforme interpretada pelo provedor OLE DB. Se estiver se conectando a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça o nome da instância.  
  
     **Cadeia de caracteres do provedor**  
     Digite o identificador programático exclusivo (PROGID) do provedor OLE DB que corresponde à fonte de dados. Para obter exemplos de cadeias de caracteres de provedor válidas, consulte [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
     **Local**  
     Digite o nome do local do banco de dados conforme interpretado pelo provedor OLE DB.  
  
     **Catálogo**  
     Digite o nome do catálogo para usar ao fazer conexão com o provedor OLE DB.  
  
     Para testar a capacidade de conexão com um servidor vinculado, no Pesquisador de Objetos, clique com o botão direito do mouse no servidor vinculado e, em seguida, clique em **Testar Conexão**.  
  
    > [!NOTE]  
    >  Se a instância do **SQL Server** for a instância padrão, digite o nome do computador que hospeda a instância do **SQL Server**. Se o **SQL Server** for uma instância nomeada, digite o nome do computador e o nome da instância, como **Accounting\SQLExpress**.  
  
3.  Na área **Tipo de servidor** , selecione **SQL Server** para indicar que o servidor vinculado é outra instância do **SQL Server**.  
  
4.  Na página **Segurança** , especifique o contexto de segurança que será usado quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] original se conectar ao servidor vinculado. Em um ambiente de domínio onde os usuários se conectam usando seus logons de domínio, a melhor opção é geralmente selecionar **Serão feitas usando o contexto de segurança atual do logon** . Quando os usuários se conectam ao **SQL Server** original com um logon do **SQL Server** , a melhor opção geralmente é selecionar **Usando este contexto de segurança**e fornecer as credenciais necessárias para autenticação no servidor vinculado.  
  
     **Logon local**  
     Especifique o logon local que pode se conectar ao servidor vinculado. O logon local pode ser um logon que usa a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um logon de Autenticação do Windows. Use essa lista para restringir a conexão a logons específicos ou permitir alguns logons para serem conectados como um logon diferente.  
  
     **Impersonate**  
     Passe o nome de usuário e senha do logon local para o servidor vinculado. Para a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , um logon com exatamente o mesmo nome e senha deve existir no servidor remoto. Para logons de Windows, o logon deve ser um logon válido no servidor vinculado.  
  
     Para usar representação, a configuração deve satisfazer o requisito para delegação.  
  
     **Usuário Remoto**  
     Use o usuário remoto para mapear usuários não definidos em **Logon local**. O **Usuário Remoto** deve ser um logon de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor remoto.  
  
     **Senha Remota**  
     Especifique a senha do Usuário Remoto.  
  
     **Adicionar**  
     Adicione um novo logon local.  
  
     **Remover**  
     Remova um logon local existente.  
  
     **Não serão feitas**  
     Especifique que uma conexão não será feita para logons não definidos na lista.  
  
     **Serão feitas sem usar um contexto de segurança**  
     Especifique que uma conexão será feita sem usar um contexto de segurança para logons não definidos na lista.  
  
     **Serão feitas usando um contexto de segurança atual do logon**  
     Especifique que uma conexão será feita usando o contexto de segurança atual do logon para logons não definidos na lista. Se conectado ao servidor local que usa Autenticação do Windows, suas credenciais do Windows serão usadas para conectar-se ao servidor remoto. Se conectado ao servidor local que usa a Autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , nome de logon e senha serão usados para conectar-se ao servidor remoto. Nesse caso um logon com exatamente o mesmo nome e senha deve existir no servidor remoto.  
  
     **Serão feitas usando este contexto de segurança**  
     Especifique que uma conexão será feita usando o logon e senha especificados nas caixas **Logon Remoto** e **Com senha** para logons não definidos na lista. O usuário remoto deve ser um logon de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor remoto.  
  
5.  Opcionalmente, para exibir ou especificar opções de servidor, clique na página **Opções de Servidor**  .  
  
     **Compatível com Agrupamento**  
     Afeta a execução da Consulta Distribuída nos servidores vinculados. Se essa opção estiver definida como true, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presumirá que todos os caracteres no servidor vinculado são compatíveis com o servidor local, no que diz respeito ao conjunto de caracteres e à sequência do agrupamento (ou ordem de classificação). Isso permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envie comparações sobre colunas de caracteres ao provedor. Se essa opção não estiver definida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre avaliará comparações sobre colunas de caracteres localmente.  
  
     Essa opção deve ser definida somente se você tiver certeza de que a fonte de dados correspondente ao servidor vinculado tem o mesmo conjunto de caracteres e ordem de classificação do servidor local.  
  
     **Acesso aos Dados**  
     Habilita e desabilita um servidor vinculado para o acesso às consultas distribuídas.  
  
     **RPC**  
     Habilita o RPC a partir do servidor especificado.  
  
     **RPC Out**  
     Habilita o RPC para o servidor especificado.  
  
     **Usar Agrupamento Remoto**  
     Determina se o agrupamento de uma coluna remota ou de um servidor local será usado.  
  
     Se verdadeiro, o agrupamento de colunas remotas será usado para as fontes dos dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o agrupamento especificado no nome será usado para fontes de dados não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Se falso, as consultas distribuídas usarão sempre o agrupamento padrão do servidor local, enquanto que o nome do agrupamento e o agrupamento de colunas remotas serão ignorados. O padrão é falso.  
  
     **Nome do Agrupamento**  
     Especifica o nome do agrupamento usado pela fonte de dados remotos se o uso do agrupamento remoto for verdadeiro e a fonte de dados não for uma fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O nome deve ser um dos agrupamentos que têm suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Use essa opção ao acessar uma origem de dados OLE DB diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas cujo agrupamento coincide com um dos agrupamentos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     O servidor vinculado deve fornecer suporte a um único agrupamento a ser usado para todas as colunas naquele servidor. Não defina essa opção se o servidor vinculado fornecer suporte a vários agrupamentos dentro de uma única fonte de dados ou se o agrupamento do servidor vinculado não puder ser determinado para corresponder a um dos agrupamentos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Tempo-limite da conexão**  
     O valor do tempo limite em segundos para conexão a um servidor vinculado.  
  
     Se 0, use o valor **sp_configure** padrão da opção [remote login timeout](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md) .  
  
     **Tempo-limite da consulta**  
     O valor do tempo limite em segundos para as consultas em um servidor vinculado.  
  
     Se 0, use o valor **sp_configure** padrão da opção [remote query timeout](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md) .  
  
     **Habilitar Promoção de Transações Distribuídas**  
     Use esta opção para proteger as ações de um procedimento servidor a servidor por meio de uma transação do MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ). Quando esta opção for TRUE, chamar um procedimento remoto armazenado irá iniciar uma transação distribuída e inscrever a transação com o MS DTC. Para obter mais informações, consulte [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md).  
  
6.  Clique em **OK**.  
  
##### <a name="to-view-the-provider-options"></a>Para exibir as opções de provedor  
  
-   Para exibir as opções que o provedor torna disponível, clique na página **Opções de Provedores** .  
  
     Todos os provedores não têm as mesmas opções disponíveis. Por exemplo, alguns tipos de dados têm índices disponíveis e outros talvez não tenham. Use essa caixa de diálogo para ajudar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a entender os recursos do provedor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala alguns provedores de dados comuns; porém, quando o produto que fornece os dados muda, o provedor instalado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode não oferecer suporte a todos os recursos mais novos. A melhor fonte de informações sobre os recursos do produto que fornece os dados é a documentação desse produto:  
  
     **Parâmetro dinâmico**  
     Indica que o provedor permite a sintaxe de marcador de parâmetro '?' para consultas parametrizadas. Defina essa opção apenas se o provedor der suporte à interface **ICommandWithParameters** e a um '?' como o marcador de parâmetro. Definir essa opção permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execute consultas com parâmetros em relação ao provedor. A capacidade de executar consultas parametrizadas em relação ao provedor pode resultar em um melhor desempenho para determinadas consultas.  
  
     **Consultas aninhadas**  
     Indica que o provedor permite instruções aninhadas `SELECT` na cláusula FROM. Definir essa opção permite ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] delegar determinadas consultas ao provedor que requer instruções aninhadas SELECT na cláusula FROM.  
  
     **Somente nível zero**  
     Somente as interfaces OLE DB de nível 0 são invocadas em relação ao provedor.  
  
     **Permitir inprocess**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que seja criada uma instância do servidor como um servidor em processo. Quando essa opção não é definida, o comportamento padrão é criar uma instância no provedor fora do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Criando uma instância no provedor fora do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] protege o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de erros no provedor. Quando a instância é criada do provedor fora do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não são permitidas atualizações ou inserções de colunas longas de referência (**text**, **ntext**ou **image**).  
  
     **Atualizações não transacionadas**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite atualizações, até mesmo se a **ITransactionLocal** não estiver disponível. Se essa opção estiver habilitada, atualizações em relação ao provedor não serão recuperáveis porque o provedor não possui suporte para transações.  
  
     **Índice como caminho de acesso**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta usar índices do provedor para buscar dados. Por padrão, os índices são usados apenas para metadados e não são abertos  
  
     **Proibir acesso ad hoc**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite acesso ad hoc pelas funções OPENROWSET e OPENDATASOURCE ao provedor OLE DB. Quando essa opção não é definida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também não permite acesso ad hoc.  
  
     **Oferece suporte ao operador 'Like'**  
     Indica que o provedor oferece suporte a consultas que usam a palavra-chave LIKE.  
  
###  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Para criar um servidor vinculado usando [!INCLUDE[tsql](../../includes/tsql-md.md)], use as instruções [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)[CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md) e [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md).  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-transact-sql"></a>Para criar um servidor vinculado para outra instância do SQL Server usando Transact-SQL  
  
1.  No Editor de Consultas, digite o comando [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir para vincular a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada `SRVR002\ACCTG`:  
  
    ```sql  
    USE [master]  
    GO  
    EXEC master.dbo.sp_addlinkedserver   
        @server = N'SRVR002\ACCTG',   
        @srvproduct=N'SQL Server' ;  
    GO  
  
    ```  
  
2.  Execute o código a seguir para configurar o servidor vinculado para usar as credenciais de domínio do logon que está usando o servidor vinculado.  
  
    ```sql  
    EXEC master.dbo.sp_addlinkedsrvlogin   
        @rmtsrvname = N'SRVR002\ACCTG',   
        @locallogin = NULL ,   
        @useself = N'True' ;  
    GO  
  
    ```  
  
##  <a name="FollowUp"></a> Acompanhamento: tarefas a serem executadas após a criação de um servidor vinculado  
  
#### <a name="to-test-the-linked-server"></a>Para testar o servidor vinculado  
  
-   Execute o código a seguir para testar a conexão com o servidor vinculado. Este exemplo retorna os nomes dos bancos de dados no servidor vinculado.  
  
    ```sql  
    SELECT name FROM [SRVR002\ACCTG].master.sys.databases ;  
    GO  
  
    ```  
  
#### <a name="writing-a-query-that-joins-tables-from-a-linked-server"></a>Gravando uma consulta que une tabelas de um servidor vinculado  
  
-   Use nomes de quatro partes para referir-se a um objeto em um servidor vinculado. Execute o código a seguir para retornar uma lista de todos os logons no servidor local e seus logons correspondentes no servidor vinculado.  
  
    ```sql  
    SELECT local.name AS LocalLogins, linked.name AS LinkedLogins  
    FROM master.sys.server_principals AS local  
    LEFT JOIN [SRVR002\ACCTG].master.sys.server_principals AS linked  
        ON local.name = linked.name ;  
    GO  
    ```  
  
     Quando NULL é retornado para o logon do servidor vinculado, ele indica que o logon não existe no servidor vinculado. Esses logons não poderão usar o servidor vinculado, a menos que o servidor vinculado seja configurado para passar um contexto de segurança diferente ou o servidor vinculado aceite conexões anônimas.  
  
## <a name="see-also"></a>Consulte Também  
 [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  
