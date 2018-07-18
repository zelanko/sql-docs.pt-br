---
title: Conectando ao SQL Server (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- authentication
- instance of SQL Server
- metadata, refreshing
- ports
- refreshing metadata
- spaces in database names
- special characters
- SQL Server
- SQL Server, connecting
- SQL Server, connecting to
- SQL Server, reconnecting
ms.assetid: f84cf007-ddf1-4396-a07c-3e0729abc769
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 085d42cc6401f665269610c18f44516f5afe7a83
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38981618"
---
# <a name="connecting-to-sql-server-accesstosql"></a>Conectando ao SQL Server (AccessToSQL)
Migrar bancos de dados de acesso à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você deve se conectar à instância de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Quando você se conectar, o SSMA obtém metadados sobre os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e exibe metadados de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados. O SSMA armazena informações sobre qual instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que você está conectado ao, mas não armazena as senhas.  
  
Sua conexão ao SQL Server permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar ao SQL Server se você quiser que uma conexão ativa com o servidor. Você pode trabalhar offline até que você carregar objetos de banco de dados no SQL Server e migra os dados.  
  
Metadados sobre a instância do SQL Server não será sincronizado automaticamente. Em vez disso, para atualizar os metadados no Gerenciador de metadados do SQL Server, você deve atualizar manualmente os metadados do SQL Server. Para obter mais informações, consulte a seção "Sincronização de metadados do SQL Server", mais adiante neste tópico.  
  
## <a name="required-sql-server-permissions"></a>Permissões de servidor necessários do SQL  
A conta que é usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] exige permissões diferentes, dependendo das ações executadas por essa conta.  
  
-   Para converter objetos de acesso à [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxe, para atualizar os metadados da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], ou para salvar a sintaxe convertido em scripts, a conta deve ter permissão para fazer logon instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Carregar objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e a migração de dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o requisito mínimo de permissão é a associação à **db_owner** função de banco de dados no banco de dados de destino.  
  
## <a name="establishing-a-sql-server-connection"></a>Estabelecer uma Conexão de servidor SQL  
Antes de converter objetos de banco de dados de acesso à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe, você deve estabelecer uma conexão à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] onde você deseja migrar os bancos de dados do Access.  
  
Quando você define as propriedades de conexão, você também especificar o banco de dados onde objetos e dados serão migrados. Você pode personalizar esse mapeamento no nível de banco de dados de acesso depois que você se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter mais informações, consulte [bancos de dados de destino e origem do mapeamento](http://msdn.microsoft.com/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
> [!IMPORTANT]  
> Antes de você se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], verifique se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está em execução e pode aceitar conexões. Para obter mais informações, consulte "conectar-se para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mecanismo de banco de dados" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online do.  
  
**Para se conectar ao SQL Server**  
  
1.  Sobre o **arquivo** menu, selecione **conectar ao SQL Server**.  
  
    Se conectado anteriormente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o nome do comando será **reconectar-se ao SQL Server**.  
  
2.  No **nome do servidor** caixa, digite ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Se você estiver se conectando à instância padrão no computador local, você pode inserir **localhost** ou um ponto (**.**).  
  
    -   Se você estiver se conectando à instância padrão em outro computador, digite o nome do computador.  
  
    -   Se você estiver se conectando a uma instância nomeada, digite o nome do computador, uma barra invertida e o nome da instância. Por exemplo: MyServer\MyInstance.  
  
    -   Para se conectar a uma instância de usuário ativa do [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], se conectar usando pipes nomeados de protocolo e especificar o nome do pipe, por exemplo, \\ \\.\pipe\sql\query. Para obter mais informações, consulte a documentação do [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)].  
  
3.  Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está configurado para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] conexões na **porta do servidor** caixa. Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] serviço localizador.  
  
4.  No **banco de dados** , digite o nome do banco de dados de destino para migração de objeto e dados.  
  
    Essa opção não está disponível quando se reconectar à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    O nome do banco de dados de destino não pode conter espaços ou caracteres especiais. Por exemplo, você pode migrar bancos de dados do Access para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados denominado "abc". Mas você não pode migrar bancos de dados do Access para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados denominado "a b-c".  
  
    Você pode personalizar esse mapeamento por banco de dados depois de se conectar. Para obter mais informações, consulte [bancos de dados de destino e origem do mapeamento](http://msdn.microsoft.com/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
5.  No **autenticação** menu suspenso, selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] login, selecione **autenticação do SQL Server**e, em seguida, forneça um nome de usuário e senha.  
  
6.  Para uma conexão segura, dois controles são adicionados, **criptografar Conexão** caixa de seleção e **TrustServerCertificate** caixa de seleção. Somente quando **criptografar Conexão** caixa de seleção é marcada **TrustServerCertificate** caixa de seleção está visível. Quando **criptografar Conexão** é checked(true) e **TrustServerCertificate** é unchecked(false), validará o certificado SSL do SQL Server. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.  
  
7.  Clique em **Conectar**.  
  
**Maior compatibilidade de versão**  
  
Ele tem permissão para conectar-se/reconectar-se para versões superiores do SQL Server.  
  
1.  Você poderá se conectar ao SQL Server 2008 ou SQL Server 2012, quando o projeto criado é o SQL Server 2005.  
  
2.  Você será capaz de se conectar ao SQL Server 2012, quando o projeto criado é o SQL Server 2008, mas ele não tem permissão para se conectar a versões anteriores ou seja, o SQL Server 2005.  
  
3.  Você será capaz de se conectar a apenas o SQL Server 2012, quando o projeto criado é o SQL Server 2012.  
  
4.  Maior compatibilidade de versão não é válida para o SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**VERSÃO do servidor de destino do projeto tipo Vs**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 (versão: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 (versão: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 (Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 (Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 (Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|Sim|Sim|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||Sim|Sim|Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||Sim|Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||||Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016|||||Sim||
|SQL Azure||||||Sim|
  
> [!IMPORTANT]  
> Conversão dos objetos de banco de dados é realizada, de acordo com o tipo de projeto, mas não de acordo com a versão do SQL Server conectado ao. No caso de projeto do SQL Server 2005, conversão é executada de acordo com o SQL Server 2005 mesmo que você está conectado a uma versão posterior do SQL Server (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizando os metadados do SQL Server  
Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas alteram depois de se conectar, você pode sincronizar os metadados com o servidor.  
  
**Para sincronizar os metadados do SQL Server**  
  
-   Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados, o botão direito do mouse **bancos de dados**e, em seguida, selecione **sincronizar com o banco de dados**.  
  
## <a name="reconnecting-to-sql-server"></a>Reconectar-se ao SQL Server  
Sua conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se você quiser que uma conexão ativa com o servidor. Você pode trabalhar offline até que você carrega objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e migrar dados.  
  
O procedimento para reconectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é o mesmo que o procedimento para estabelecer uma conexão.  
  
## <a name="next-steps"></a>Próximas etapas  
Se você quiser personalizar o mapeamento entre bancos de dados de origem e destino, consulte [bancos de dados de destino e origem do mapeamento](http://msdn.microsoft.com/69bee937-7b2c-49ee-8866-7518c683fad4) caso contrário, a próxima etapa é converter objetos de banco de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando sintaxe [converter objetos de banco de dados](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
