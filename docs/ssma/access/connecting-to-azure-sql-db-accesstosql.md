---
title: Conectar-se ao banco de dados do SQL Azure (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-access
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
- instance of SQL Azure
- metadata, refreshing
- refreshing metadata
- SQL Azure
- SQL Azure, connecting
- SQL Azure, connecting to
- SQL Azure, reconnecting
- SQL Azure, synchronizing metadata
ms.assetid: 1ba0d113-dc05-4431-8689-e14a8821bafd
caps.latest.revision: 21
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 152a5cee9dbb7308772d0a2e21f263c873570171
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-azure-sql-db-accesstosql"></a>Conectar-se ao banco de dados do SQL Azure (AccessToSQL)
Para migrar bancos de dados do Access para o SQL Azure, você deve se conectar à instância de destino do SQL Azure. Quando você se conectar, o SSMA obtém metadados sobre todos os bancos de dados na instância do SQL Azure e exibe os metadados de banco de dados no Explorador de metadados do SQL Azure. O SSMA armazena informações sobre a instância do SQL Azure está conectado, mas não armazena as senhas.  
  
Sua conexão com o SQL Azure permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve reconectar ao SQL Azure se você quiser uma conexão ativa com o servidor. Você pode trabalhar offline até que você carregar objetos de banco de dados no SQL Azure e migra dados.  
  
Metadados sobre a instância do SQL Azure não será sincronizado automaticamente. Em vez disso, para atualizar os metadados no Gerenciador de metadados do SQL Azure, você deve atualizar manualmente os metadados do SQL Azure. Para obter mais informações, consulte a seção "Sincronizando o SQL Azure metadados" mais adiante neste tópico.  
  
## <a name="required-sql-azure-permissions"></a>Necessário SQL permissões do Azure  
A conta que é usada para se conectar ao SQL Azure requer permissões diferentes dependendo de ações que realiza a conta:  
  
-   Para converter objetos de acesso a [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxe, para atualizar os metadados do SQL Azure, ou salvar sintaxe convertido para scripts, a conta deve ter permissão para fazer logon na instância do SQL Azure.  
  
-   Para carregar os objetos de banco de dados no SQL Azure, o requisito mínimo de permissão é a associação de **db_owner** função de banco de dados no banco de dados de destino.  
  
## <a name="establishing-a-sql-azure-connection"></a>Estabelecendo um SQL Azure Conexão  
Antes de converter objetos de banco de dados do Access a sintaxe do SQL Azure, você deve estabelecer uma conexão com a instância do SQL Azure em que você deseja migrar o banco de dados ou bancos de dados.  
  
Quando você define as propriedades de conexão, você também especificar o banco de dados onde objetos e dados serão migrados. Depois de se conectar ao SQL Azure, você pode personalizar esse mapeamento no nível do esquema de acesso. Para obter mais informações, consulte [mapeamento de bancos de dados Access para esquemas SQL Server](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao SQL Azure, certifique-se de que a instância do SQL Azure está em execução e pode aceitar conexões.  
  
**Para se conectar ao SQL Azure**  
  
1.  Sobre o **arquivo** menu, selecione **conectar-se ao SQL Azure** (essa opção é habilitada após a criação de um projeto).  
  
    Se você se conectado anteriormente ao SQL Azure, o nome do comando será **reconectar-se ao SQL Azure**.  
  
2.  Na caixa de diálogo de conexão, digite ou selecione o nome do servidor do SQL Azure.  
  
3.  Insira, selecione ou **procurar** o nome do banco de dados.  
  
4.  Insira ou selecione **nome de usuário**.  
  
5.  Insira o **senha**.  
  
6.  O SSMA recomenda conexão criptografada para o SQL Azure.  
  
7.  Clique em **Conectar**.  
  
> [!IMPORTANT]  
> O SSMA para Access não dá suporte a conexão para **mestre** banco de dados no SQL Azure.  
  
Se não houver nenhum banco de dados na conta do SQL Azure, você pode criar o banco de dados usando a primeira **criar banco de dados do Azure** opção que aparece ao clicar de **procurar** botão.  
  
## <a name="synchronizing-sql-azure-metadata"></a>Sincronizando o SQL Azure metadados  
Metadados sobre bancos de dados do SQL Azure não são atualizados automaticamente. Os metadados no Gerenciador de metadados do SQL Azure são um instantâneo dos metadados quando conectado primeiro para o SQL Azure, ou a última vez que você manualmente atualizado metadados. Você pode atualizar manualmente os metadados para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados.  
  
**Para sincronizar os metadados**  
  
1.  Certifique-se de que você está conectado ao SQL Azure.  
  
2.  No Gerenciador de metadados do SQL Azure, selecione a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados para todos os bancos de dados, marque a caixa ao lado de bancos de dados.  
  
3.  Bancos de dados, ou o banco de dados individual ou o esquema de banco de dados e, em seguida, selecione **sincronizar com o banco de dados**.  
  
## <a name="refreshing-sql-azure-metadata"></a>Atualizando o SQL Azure metadados  
Se os esquemas do SQL Azure alteram depois de se conectar, você pode atualizar metadados do servidor.  
  
**Para atualizar os metadados do SQL Azure**  
  
-   No Gerenciador de metadados do SQL Azure, clique com botão direito **bancos de dados**e, em seguida, selecione **de atualização do banco de dados**.  
  
## <a name="reconnecting-to-sql-azure"></a>Reconectar-se ao SQL Azure  
Sua conexão com o SQL Azure permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve reconectar ao SQL Azure se você quiser uma conexão ativa com o servidor. Você pode trabalhar offline até que você carregar objetos de banco de dados no SQL Azure e migra dados.  
  
O procedimento para reconectar-se ao SQL Azure é o mesmo que o procedimento para estabelecer uma conexão.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre esquemas de acesso e esquemas de bancos de dados do SQL Azure, consulte [bancos de dados do mapeamento de acesso para esquemas SQL Server](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4).  
  
-   Para personalizar opções de configuração para os projetos, consulte [definindo opções de projeto](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167).  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [tipos de dados de destino e origem do mapeamento de](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).  
  
-   Se você não precisa executar qualquer uma dessas tarefas, você pode converter as definições de objeto de banco de dados do Access em definições de objeto do SQL Azure. Para obter mais informações, consulte [convertendo bancos de dados do Access](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
