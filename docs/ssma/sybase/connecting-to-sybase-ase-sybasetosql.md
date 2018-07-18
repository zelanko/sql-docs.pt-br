---
title: Conectar-se a ASE Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0fe501e639b5896eb0f83391e6be40b8f8961ba9
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980088"
---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>Conectar-se a ASE Sybase (SybaseToSQL)
Migrar bancos de dados do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você deve se conectar ao servidor adaptável que contém os bancos de dados que você deseja migrar. Quando você se conectar, o SSMA obtém os metadados sobre todos os bancos de dados no servidor adaptável e exibe metadados de banco de dados no painel Gerenciador de metadados do Sybase. O SSMA armazena informações sobre o servidor de banco de dados, mas não armazena as senhas.  
  
Sua conexão para o ASE permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar ao ASE se você quiser que uma conexão ativa com o servidor.  
  
Metadados sobre o servidor adaptável não é atualizado automaticamente. Em vez disso, se você quiser atualizar os metadados no Gerenciador de metadados do Sybase, você deve atualizar manualmente os metadados, conforme descrito na seção "Atualizando Sybase ASE metadados" neste tópico.  
  
## <a name="required-ase-permissions"></a>Permissões necessárias do ASE  
A conta que é usada para se conectar ao ASE deve ter pelo menos **pública** acesso ao banco de dados mestre e a qualquer banco de dados de origem sejam migrados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure. Além disso, para selecionar permissões nas tabelas que estão sendo migradas, o usuário deve ter permissões SELECT nas tabelas do sistema a seguir:  
  
-   [source_db].dbo.sysobjects  
  
-   [source_db].dbo.syscolumns  
  
-   [source_db].dbo.sysusers  
  
-   [source_db].dbo.systypes  
  
-   [source_db].dbo.sysconstraints  
  
-   [source_db].dbo.syscomments  
  
-   [source_db].dbo.sysindexes  
  
-   [source_db].dbo.sysreferences  
  
-   master.dbo.sysdatabases  
  
## <a name="establishing-a-connection-to-ase"></a>Estabelecer uma Conexão para o ASE  
Quando você se conecta a um servidor adaptável, o SSMA lê os metadados do banco de dados no servidor de banco de dados e, em seguida, adiciona esses metadados ao arquivo de projeto. Esses metadados são usados pelo SSMA quando ele converte os objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou a sintaxe do SQL Azure, e quando ele migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure. Você pode procurar esses metadados no painel Gerenciador de metadados do Sybase e examine as propriedades dos objetos de banco de dados individuais.  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao servidor de banco de dados, certifique-se de que o servidor de banco de dados está em execução e pode aceitar conexões.  
  
**Para conectar-se ao Sybase ASE**  
  
1.  Sobre o **arquivo** menu, selecione **conectar-se ao Sybase**.  
  
    Se você conectado anteriormente ao Sybase, será o nome do comando **reconectar-se ao Sybase**.  
  
2.  No **provedor** , selecione qualquer um dos provedores instalados no computador para se conectar ao servidor do Sybase.  
  
3.  No **modo** , selecione qualquer uma **modo padrão** ou **modo avançado**.  
  
    Use o modo padrão para especificar o nome do servidor, porta, nome de usuário e senha. Use o modo avançado para fornecer uma cadeia de caracteres de conexão. Esse modo geralmente é usado somente para solução de problemas ou trabalhar com o suporte técnico.  
  
4.  Se você selecionar **o modo padrão**, forneça os seguintes valores:  
  
    1.  No **nome do servidor** caixa, digite ou selecione o nome ou endereço IP do servidor de banco de dados.  
  
    2.  Se o servidor de banco de dados não estiver configurado para aceitar conexões no padrão da porta (5000), insira o número da porta que é usado para conexões do Sybase na **porta do servidor** caixa.  
  
    3.  No **nome de usuário** , digite uma conta do Sybase que tem as permissões necessárias.  
  
    4.  No **senha** , digite a senha para o nome de usuário especificado.  
  
5.  Se você selecionar **modo avançado**, forneça uma cadeia de conexão na **cadeia de caracteres de Conexão** caixa.  
  
    Exemplos de cadeias de caracteres de conexão diferentes são da seguinte maneira:  
  
    1.  **Cadeias de caracteres de Conexão do Sybase OLE DB Provider:**  
  
        Para Sybase ASE OLE DB 12,5, uma cadeia de caracteres de conexão de exemplo é o seguinte:  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Para Sybase ASE OLE DB 15, um exemplo de cadeia de conexão é da seguinte maneira:  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Cadeia de caracteres de Conexão para o provedor do Sybase ODBC:**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Cadeia de caracteres de Conexão para o provedor de ADO.NET Sybase:**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    Para obter mais informações, consulte [conectar-se ao Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md).  
  
## <a name="reconnecting-to-sybase-ase"></a>Reconectar-se ao Sybase ASE  
Sua conexão com o servidor de banco de dados permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar se você quiser que uma conexão ativa com o servidor adaptável. Você pode trabalhar offline até que você deseja atualizar os metadados, carregar objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, e migrar dados.  
  
## <a name="refreshing-sybase-ase-metadata"></a>Atualizar metadados de ASE do Sybase  
Metadados sobre os bancos de dados do ASE não é atualizado automaticamente. Os metadados no Gerenciador de metadados do Sybase são um instantâneo dos metadados quando você primeiro conectado ao servidor adaptável, ou a última vez que você atualizou metadados manualmente. Você pode atualizar manualmente os metadados para um banco de dados, um esquema de banco de dados individual ou todos os bancos de dados.  
  
**Para atualizar os metadados**  
  
1.  Certifique-se de que você está conectado ao servidor adaptável.  
  
2.  No Gerenciador de metadados do Sybase, selecione a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
3.  Bancos de dados ou o banco de dados individual ou o esquema de banco de dados e, em seguida, selecione **Refresh do banco de dados**.  
  
4.  Se você for solicitado a verificar o objeto atual, clique em **Sim**.  
  
## <a name="next-step"></a>Próxima etapa  
  
-   É a próxima etapa no processo de migração [conectar-se a uma instância do SQL Server](http://msdn.microsoft.com/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) / [se conectar a uma instância do SQL Azure](http://msdn.microsoft.com/9e77e4b0-40c0-455c-8431-ca5d43849aa7)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Sybase ASE para o SQL Server – BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
