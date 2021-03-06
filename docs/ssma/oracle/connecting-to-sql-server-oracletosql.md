---
title: Conectando-se ao SQL Server (OracleToSQL) | Microsoft Docs
description: Saiba como se conectar ao SQL Server para migrar um banco de dados Oracle. O SSMA Obtém e exibe metadados para bancos de dados no SQL Server.
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server,Synchronizing SQL Server Metadata
ms.assetid: 1b2a8059-1829-4904-a82f-9c06de1e245f
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: a1bb675f00097bb86b56b6019a3b326b58302158
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870201"
---
# <a name="connecting-to-sql-server-oracletosql"></a>Conectar-se ao SQL Server (OracleToSQL)

Para migrar bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, você deve se conectar à instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando você se conecta, o SSMA obtém metadados sobre todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibe os metadados do banco de dados no **SQL Server Gerenciador de metadados**. O SSMA armazena informações sobre a qual instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você está conectado, mas não armazena senhas.

Sua conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecerá ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados no e migrar.

Os metadados sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não são sincronizados automaticamente. Em vez disso, para atualizar os metadados no **SQL Server Gerenciador de metadados**, você deve atualizar manualmente os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados. Para obter mais informações, consulte a seção "sincronizando metadados de SQL Server" mais adiante neste tópico.

## <a name="required-sql-server-permissions"></a>Permissões de SQL Server necessárias

A conta usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer permissões diferentes dependendo das ações que a conta executa:

- Para converter objetos Oracle em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, para atualizar metadados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou para salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

- Para carregar objetos de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a conta deve ser membro da função de banco de dados **db_ddladmin** .

- Para migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, a conta deve ser:
  - Um membro da função de banco de dados **db_owner** , se estiver usando o mecanismo de migração de dado do lado do cliente.
  - Um membro da função de servidor **sysadmin** , se estiver usando o mecanismo de migração de dados do servidor. Isso é necessário para criar a `CmdExec` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] etapa de trabalho do Agent durante a migração de dados para executar a ferramenta de cópia em massa do SSMA.
    > [!NOTE]
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As contas proxy do agente não são suportadas pela migração de dados do lado do servidor.

- Para executar o código gerado pelo SSMA, a conta deve ter `EXECUTE` permissões para todas as funções definidas pelo usuário no esquema de **ssma_oracle** do banco de dados de destino. Essas funções fornecem funcionalidade equivalente às funções do sistema Oracle e são usadas por objetos convertidos.

## <a name="establishing-a-sql-server-connection"></a>Estabelecendo uma conexão SQL Server

Antes de converter objetos de banco de dados Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe, você deve estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que você deseja migrar o banco de dados Oracle ou bancos.

Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível de esquema do Oracle depois de se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Mapping Oracle schemas to SQL Server schemas &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).

> [!IMPORTANT]
> Antes de tentar se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verifique se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução e pode aceitar conexões.

Para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :

1. No menu **arquivo** , selecione **conectar-se a SQL Server**.
   Se você se conectou anteriormente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o nome do comando será **reconectado a SQL Server**.

2. Na caixa de diálogo conexão, digite ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
   - Se você estiver se conectando à instância padrão no computador local, poderá inserir `localhost` ou um ponto ( `.` ).
   - Se você estiver se conectando à instância padrão em outro computador, insira o nome do computador.
   - Se você estiver se conectando a uma instância nomeada em outro computador, insira o nome do computador seguido por uma barra invertida e, em seguida, o nome da instância, como `MyServer\MyInstance` .

3. Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexões na caixa **porta do servidor** . Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador.

4. Na caixa **banco de dados** , digite o nome do banco de dados de destino.
   Essa opção não está disponível quando você se reconecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

5. Na caixa **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon, selecione **SQL Server autenticação** e forneça o nome de logon e a senha.

6. Para conexão segura, dois controles são adicionados, as caixas de seleção **criptografar conexão** e **TrustServerCertificate** . Somente quando a opção **criptografar conexão** está marcada, a caixa de seleção **TrustServerCertificate** está visível. Quando **criptografar conexão** está marcado (true) e **TrustServerCertificate** está desmarcado (false), ele validará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado SSL. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.

7. Clique em **Conectar**.

> [!IMPORTANT]
> Embora você possa se conectar a uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , em comparação com a versão escolhida quando o projeto de migração foi criado, a conversão dos objetos de banco de dados é determinada pela versão de destino do projeto e não pela versão do à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qual você está conectado.

## <a name="synchronizing-sql-server-metadata"></a>Sincronizando metadados de SQL Server

Metadados sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados não são atualizados automaticamente. Os metadados no **SQL Server Gerenciador de metadados** é um instantâneo dos metadados quando você se conecta pela primeira vez ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou da última atualização dos metadados. Você pode atualizar os metadados manualmente para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados individual. Para sincronizar os metadados:

1. Certifique-se de que você está conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

2. No **SQL Server Gerenciador de metadados**, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.
   Por exemplo, para atualizar os metadados de todos os bancos de dados, selecione a caixa ao lado de **bancos de dados**.

3. Clique com o botão direito do mouse em **bancos** de dados ou em um esquema ou banco de dados individual e selecione **sincronizar com Banco de dados**.
  
## <a name="next-step"></a>Próxima etapa

A próxima etapa na migração depende de suas necessidades de projeto:
  
- Para personalizar o mapeamento entre esquemas e bancos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados e esquemas Oracle, consulte [mapeando esquemas oracle para SQL Server esquemas &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).
- Para personalizar as opções de configuração para os projetos, consulte [definindo opções de projeto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md).
- Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando os tipos de dados Oracle e SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).
- Se você não precisar executar nenhuma dessas tarefas, poderá converter as definições de objeto do banco de dados Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de objeto. Para obter mais informações, consulte [convertendo esquemas Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).
  
## <a name="see-also"></a>Consulte Também

[Migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
