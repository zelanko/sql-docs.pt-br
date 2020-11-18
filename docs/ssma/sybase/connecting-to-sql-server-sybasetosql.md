---
description: Conectar-se ao SQL Server (SybaseToSQL)
title: Conectando-se ao SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 2988f57c5d0e3162c9b6dc54d8a7371efcf5da05
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870399"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>Conectar-se ao SQL Server (SybaseToSQL)

Para migrar bancos de dados do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, você deve se conectar à instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando você se conecta, o SSMA obtém metadados sobre todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibe os metadados do banco de dados no **SQL Server Gerenciador de metadados**. O SSMA armazena informações sobre a qual instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você está conectado, mas não armazena senhas.

Sua conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecerá ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados no e migrar.

Os metadados sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não são sincronizados automaticamente. Em vez disso, se você quiser atualizar os metadados no **SQL Server Gerenciador de metadados**, será necessário atualizar manualmente os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados, conforme descrito na seção "sincronizando metadados de SQL Server" mais adiante neste tópico.

## <a name="required-sql-server-permissions"></a>Permissões de SQL Server necessárias

A conta usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer permissões diferentes dependendo das ações que a conta executa:

- Para converter objetos do ASE em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, atualizar metadados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

- Para carregar objetos de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a conta deve ser membro da função de banco de dados **db_ddladmin** .

- Para migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, a conta deve ser:
  - Um membro da função de banco de dados **db_owner** , se estiver usando o mecanismo de migração de dado do lado do cliente.
  - Um membro da função de servidor **sysadmin** , se estiver usando o mecanismo de migração de dados do servidor. Isso é necessário para criar a `CmdExec` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] etapa de trabalho do Agent durante a migração de dados para executar a ferramenta de cópia em massa do SSMA.
    > [!NOTE]
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As contas proxy do agente não são suportadas pela migração de dados do lado do servidor.

- Para executar o código gerado pelo SSMA, a conta deve ter `EXECUTE` permissões para todas as funções definidas pelo usuário no esquema de **ssma_syb** do banco de dados de destino. Essas funções fornecem funcionalidade equivalente às funções do sistema ASE e são usadas por objetos convertidos.

## <a name="establishing-a-sql-server-connection"></a>Estabelecendo uma conexão SQL Server

Antes de converter objetos de banco de dados do ASE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe, você deve estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que você deseja migrar o banco de dados ase ou bancos.

Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível de esquema do ASE depois de se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [mapeando esquemas do ase do Sybase para esquemas de SQL Server &#40;&#41;SybaseToSQL ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).

> [!IMPORTANT]
> Antes de tentar se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verifique se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução e pode aceitar conexões.

Para conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:
  
1. No menu **arquivo** , selecione **conectar-se a SQL Server**.
   Se você se conectou anteriormente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o nome do comando será **reconectado a SQL Server**.

2. Na caixa de diálogo conexão, digite ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
   - Se você estiver se conectando à instância padrão no computador local, poderá inserir `localhost` ou um ponto ( `.` ).
   - Se você estiver se conectando à instância padrão em outro computador, insira o nome do computador.
   - Se você estiver se conectando a uma instância nomeada em outro computador, insira o nome do computador seguido por uma barra invertida e, em seguida, o nome da instância, como `MyServer\MyInstance` .

3. Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexões na caixa **porta do servidor** . Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador.

4. Na caixa **banco de dados** , digite o nome do banco de dados de destino.
   Essa opção não está disponível ao reconectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

5. Na caixa **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon, selecione **SQL Server autenticação** e, em seguida, forneça o nome de logon e a senha.

6. Para conexão segura, dois controles são adicionados, as caixas de seleção **criptografar conexão** e **TrustServerCertificate** . Somente quando a opção **criptografar conexão** está marcada, a caixa de seleção **TrustServerCertificate** está visível. Quando **criptografar conexão** está marcado (true) e **TrustServerCertificate** está desmarcado (false), ele validará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado SSL. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.

7. Clique em **Conectar**.

> [!IMPORTANT]
> Embora você possa se conectar a uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , em comparação com a versão escolhida quando o projeto de migração foi criado, a conversão dos objetos de banco de dados é determinada pela versão de destino do projeto e não pela versão do à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qual você está conectado.

## <a name="reconnecting-to-sql-server"></a>Reconectando ao SQL Server

Sua conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecerá ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até atualizar os metadados, carregar objetos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados em e migrar os mesmos.

O procedimento para reconectar-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o mesmo que o procedimento para estabelecer uma conexão.

## <a name="synchronizing-sql-server-metadata"></a>Sincronizando metadados de SQL Server

Os metadados sobre os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados não são atualizados automaticamente. Os metadados no **SQL Server Gerenciador de metadados** é um instantâneo dos metadados quando você se conecta pela primeira vez ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou da última atualização dos metadados. Você pode atualizar os metadados manualmente para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados individual. Para sincronizar metadados:

1. Certifique-se de que você está conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

2. No **SQL Server Gerenciador de metadados**, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.
   Por exemplo, para atualizar os metadados de todos os bancos de dados, selecione a caixa ao lado de **bancos de dados**.

3. Clique com o botão direito do mouse em **bancos** de dados ou em um esquema de banco de dados individual ou em seu próprio e selecione **sincronizar com Banco de dados**.

## <a name="next-step"></a>Próxima etapa

A próxima etapa na migração depende de suas necessidades de projeto:

- Se você quiser personalizar o mapeamento entre bancos de dados do ASE e esquemas e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados e esquemas, consulte [mapeando esquemas do ase do Sybase para esquemas de SQL Server &#40;&#41;SybaseToSQL ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).
- Se você quiser personalizar as opções de configuração para os projetos, consulte [definindo opções de projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).
- Se você quiser personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando os tipos de dados do Sybase ase e SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).
- Se você não precisar fazer nenhuma delas, poderá converter as definições de objeto de banco de dados do Sybase ASE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de objeto. Para obter mais informações, consulte [convertendo objetos de banco de dados do Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).

## <a name="see-also"></a>Consulte Também

[Migrando bancos de dados do Sybase ASE para o SQL Server-banco de SybaseToSQL SQL do Azure &#40;o&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)
