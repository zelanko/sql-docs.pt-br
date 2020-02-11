---
title: Conectando-se ao Sybase ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: e1debb31cd70c73e3fecd569a58534377742a9a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948520"
---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>Conectar-se a ASE Sybase (SybaseToSQL)
Para migrar bancos de dados do Sybase Adaptive Server Enterprise (ASE) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o ou SQL Azure, você deve se conectar ao servidor adaptável que contém os bancos de dados que você deseja migrar. Quando você se conecta, o SSMA obtém metadados sobre todos os bancos de dados no servidor adaptável e exibe os metadados do banco de dados no painel Gerenciador de metadados Sybase. O SSMA armazena informações sobre o servidor de banco de dados, mas não armazena senhas.  
  
Sua conexão com o ASE permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao ASE se desejar uma conexão ativa com o servidor.  
  
Os metadados sobre o servidor adaptável não são atualizados automaticamente. Em vez disso, se desejar atualizar os metadados no Gerenciador de metadados do Sybase, você deverá atualizar manualmente os metadados, conforme descrito na seção "Atualizando metadados do ASE Sybase" mais adiante neste tópico.  
  
## <a name="required-ase-permissions"></a>Permissões do ASE necessárias  
A conta que é usada para conectar-se ao ASE deve ter pelo menos acesso **público** ao banco de dados mestre e a quaisquer bancos de dados de origem a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serem migrados para o ou SQL Azure. Além disso, para selecionar permissões em tabelas que estão sendo migradas, o usuário deve ter permissões SELECT nas seguintes tabelas do sistema:  
  
-   [source_db]. dbo. sysobjects  
  
-   [source_db]. dbo. syscolumns  
  
-   [source_db]. dbo. sysusers  
  
-   [source_db]. dbo. systypes  
  
-   [source_db]. dbo. sysconstraints  
  
-   [source_db]. dbo. syscomments  
  
-   [source_db]. dbo. sysindexes  
  
-   [source_db]. dbo. sysreferences  
  
-   Master. dbo. sysdatabases  
  
## <a name="establishing-a-connection-to-ase"></a>Estabelecendo uma conexão com o ASE  
Quando você se conecta a um servidor adaptável, o SSMA lê os metadados do banco de dados no servidor de banco de dados e, em seguida, adiciona esses metadados ao arquivo de projeto. Esses metadados são usados pelo SSMA quando convertem os objetos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure sintaxe e quando ele migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você pode procurar esses metadados no painel do Gerenciador de metadados do Sybase e examinar as propriedades de objetos de banco de dados individuais.  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao servidor de banco de dados, verifique se o servidor de banco de dados está em execução e pode aceitar conexões.  
  
**Para se conectar ao Sybase ASE**  
  
1.  No menu **arquivo** , selecione **conectar-se ao Sybase**.  
  
    Se você se conectou anteriormente ao Sybase, o nome do comando será **reconectado ao Sybase**.  
  
2.  Na caixa **provedor** , selecione qualquer um dos provedores instalados no computador para se conectar ao servidor Sybase.  
  
3.  Na caixa **modo** , selecione o modo **padrão** ou **avançado**.  
  
    Use o modo padrão para especificar o nome do servidor, a porta, o nome de usuário e a senha. Use o modo avançado para fornecer uma cadeia de conexão. Esse modo geralmente é usado apenas para solução de problemas ou trabalho com suporte técnico.  
  
4.  Se você selecionar **modo padrão**, forneça os seguintes valores:  
  
    1.  Na caixa **nome do servidor** , digite ou selecione o nome ou endereço IP do servidor de banco de dados.  
  
    2.  Se o servidor de banco de dados não estiver configurado para aceitar conexões na porta padrão (5000), insira o número da porta que é usado para conexões Sybase na caixa **porta do servidor** .  
  
    3.  Na caixa **nome de usuário** , insira uma conta do Sybase que tenha as permissões necessárias.  
  
    4.  Na caixa **senha** , digite a senha para o nome de usuário especificado.  
  
5.  Se você selecionar **modo avançado**, forneça uma cadeia de conexão na caixa **cadeia de conexão** .  
  
    Os exemplos de cadeias de conexão diferentes são os seguintes:  
  
    1.  **Cadeias de conexão para o provedor de OLE DB do Sybase:**  
  
        Para o ASE do Sybase OLE DB 12,5, um exemplo de cadeia de conexão é o seguinte:  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Para Sybase ASE OLE DB 15, um exemplo de cadeia de conexão é o seguinte:  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Cadeia de conexão para o provedor ODBC do Sybase:**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Cadeia de conexão para o provedor de ADO.NET do Sybase:**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    Para obter mais informações, consulte [conectar-se ao Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md).  
  
## <a name="reconnecting-to-sybase-ase"></a>Reconectando ao Sybase ASE  
A conexão com o servidor de banco de dados permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar se quiser uma conexão ativa com o servidor adaptável. Você pode trabalhar offline até que queira atualizar os metadados, carregar objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados no ou SQL Azure e migrar dados.  
  
## <a name="refreshing-sybase-ase-metadata"></a>Atualizando metadados do ASE do Sybase  
Os metadados sobre os bancos de dados ASE não são atualizados automaticamente. Os metadados no Gerenciador de metadados do Sybase são um instantâneo dos metadados quando você se conecta pela primeira vez ao servidor adaptável ou na última vez que você atualizou os metadados manualmente. Você pode atualizar manualmente os metadados de um único banco de dados, de um único esquema de banco de dados ou de todos os bancos.  
  
**Para atualizar metadados**  
  
1.  Certifique-se de que você está conectado ao servidor adaptável.  
  
2.  No Gerenciador de metadados do Sybase, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
3.  Clique com o botão direito do mouse em bancos de dados ou em um esquema de banco de dados individual ou em seu próprio e selecione **Atualizar do banco de**dados.  
  
4.  Se for solicitado que você verifique o objeto atual, clique em **Sim**.  
  
## <a name="next-step"></a>Próxima etapa  
  
-   A próxima etapa do processo de migração é [conectar-se a uma instância do SQL Server](connecting-to-sql-server-sybasetosql.md) / [se conectando a uma instância do SQL Azure](connecting-to-azure-sql-db-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Sybase ASE para o SQL Server-BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
