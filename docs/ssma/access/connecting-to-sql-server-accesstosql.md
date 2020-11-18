---
title: Conectando-se ao SQL Server (AccessToSQL) | Microsoft Docs
description: Saiba como se conectar a uma instância de destino do banco de dados SQL para migrar bancos de dados do Access. O SSMA Obtém os metadados sobre os bancos de dados no SQL Database.
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1bd54d3fdf90447dbbf8b35a96c6b454ca6c4e56
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869535"
---
# <a name="connecting-to-sql-server-accesstosql"></a>Conectando-se ao SQL Server (AccessToSQL)

Para migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, você deve se conectar à instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando você se conecta, o SSMA obtém metadados sobre os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibe metadados de banco de dados no **SQL Server Gerenciador de metadados**. O SSMA armazena informações sobre a instância do à qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você está conectado, mas não armazena senhas.

Sua conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecerá ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados no e migrar.

Os metadados sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não são sincronizados automaticamente. Em vez disso, para atualizar os metadados no SQL Server Gerenciador de metadados, você deve atualizar manualmente os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados. Para obter mais informações, consulte a seção "sincronizando metadados de SQL Server" mais adiante neste tópico.

## <a name="required-sql-server-permissions"></a>Permissões de SQL Server necessárias

A conta usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer permissões diferentes dependendo das ações que a conta executa:

- Para converter objetos do Access em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, atualizar metadados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

- Para carregar objetos de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a conta deve ser membro da função de banco de dados **db_ddladmin** .

- Para migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, a conta deve ser um membro da função de banco de dado **db_owner** .

## <a name="establishing-a-sql-server-connection"></a>Estabelecendo uma conexão SQL Server

Antes de converter objetos de banco de dados do Access em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe, você deve estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde você deseja migrar os bancos de dados do Access.

Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível do banco de dados do Access depois de se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [mapeando bancos de dados de origem e de destino](mapping-source-and-target-databases-accesstosql.md).

> [!IMPORTANT]
> Antes de se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verifique se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução e pode aceitar conexões.

Para conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:

1. No menu **arquivo** , selecione **conectar-se a SQL Server**.
   Se você se conectou anteriormente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o nome do comando será **reconectado a SQL Server**.

2. Na caixa **nome do servidor** , digite ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
   - Se você estiver se conectando à instância padrão no computador local, poderá inserir `localhost` ou um ponto ( `.` ).
   - Se você estiver se conectando à instância padrão em outro computador, insira o nome do computador.
   - Se você estiver se conectando a uma instância nomeada, insira o nome do computador, uma barra invertida e o nome da instância. Por exemplo: `MyServer\MyInstance`.
   - Para se conectar a uma instância de usuário ativa do [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] , conecte-se usando o protocolo de pipes nomeados e especificando o nome do pipe, como `\\.\pipe\sql\query` . Para obter mais informações, consulte a documentação do [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)].

3. Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexões na caixa **porta do servidor** . Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador.

4. Na caixa **de dados,** digite o nome do banco de dados de destino para a migração de objeto e data.
   Essa opção não está disponível ao reconectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
   O nome do banco de dados de destino não pode conter espaços ou caracteres especiais. Por exemplo, você pode migrar bancos de dados do Access para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados denominado `abc` . Mas você não pode migrar os bancos de dados do Access para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database denominado `a b-c` .
   Você pode personalizar esse mapeamento por banco de dados depois de se conectar. Para obter mais informações, consulte [mapeando bancos de dados de origem e de destino](mapping-source-and-target-databases-accesstosql.md)

5. No menu suspenso **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon, selecione **SQL Server autenticação** e, em seguida, forneça um nome de usuário e uma senha.

6. Para conexão segura, dois controles são adicionados, caixa de seleção **criptografar conexão** e caixa de seleção **TrustServerCertificate** . Somente quando a caixa de seleção **criptografar conexão** está marcada, a caixa de seleção **TrustServerCertificate** está visível. Quando **criptografar conexão** está marcado (true) e **TrustServerCertificate** está desmarcado (false), o validará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado SSL. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.

7. Clique em **Conectar**.

> [!IMPORTANT]
> Embora você possa se conectar a uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , em comparação com a versão escolhida quando o projeto de migração foi criado, a conversão dos objetos de banco de dados é determinada pela versão de destino do projeto e não pela versão do à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qual você está conectado.

## <a name="synchronizing-sql-server-metadata"></a>Sincronizando metadados de SQL Server

Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os esquemas forem alterados após a conexão, você poderá sincronizar os metadados com o servidor.

Para sincronizar SQL Server metadados, **SQL Server Gerenciador de metadados**, clique com o botão direito do mouse em **bancos** de dados e, em seguida, selecione **sincronizar com Database**.

## <a name="reconnecting-to-sql-server"></a>Reconectando ao SQL Server

Sua conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecerá ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados no e migrar.

O procedimento para reconectar-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o mesmo que o procedimento para estabelecer uma conexão.

## <a name="next-steps"></a>Próximas etapas

Se você quiser personalizar o mapeamento entre os bancos de dados de origem e de destino, consulte [mapeando bancos](mapping-source-and-target-databases-accesstosql.md) de dados de origem e de destino de outra forma, a próxima etapa é converter objetos de Database em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe usando [converter objetos de banco de dados](converting-access-database-objects-accesstosql.md).

## <a name="see-also"></a>Consulte Também

[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)
