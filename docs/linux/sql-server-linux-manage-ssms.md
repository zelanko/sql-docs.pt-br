---
title: Usar o SSMS para gerenciar o SQL Server no Linux | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/21/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.custom: sql-linux
ms.openlocfilehash: 2b6293e7c0d80eb1ebe02d6cd03f17626d793c05
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001658"
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Use o SQL Server Management Studio no Windows para gerenciar o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo apresenta [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) e orienta você por algumas tarefas comuns. O SSMS é um aplicativo do Windows, portanto, use o SSMS quando você tiver um computador Windows que pode se conectar a uma instância remota do SQL Server no Linux.

> [!TIP]
> Se você não tiver uma máquina do Windows para executar o SSMS, considere o novo [SQL Server Operations Studio](../sql-operations-studio/index.md). Ele fornece uma ferramenta gráfica para gerenciar o SQL Server e é executado no Linux e Windows.

[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) faz parte de um conjunto de ferramentas do SQL que a Microsoft oferece gratuitamente para suas necessidades de desenvolvimento e gerenciamento. O SSMS é um ambiente integrado para acessar, configurar, gerenciar, administrar e desenvolver todos os componentes do SQL Server. Ele pode se conectar ao SQL Server em execução em qualquer plataforma no local, em contêineres do Docker e na nuvem. Ele também se conecta ao banco de dados SQL e Azure SQL Data Warehouse. SSMS combina um amplo grupo de ferramentas gráficas com um número de editores de script avançados para fornecer acesso ao SQL Server para desenvolvedores e administradores de todos os níveis de habilidade.

SSMS oferece um amplo conjunto de recursos de desenvolvimento e gerenciamento para SQL Server, incluindo ferramentas para:

- Configurar, monitorar e administrar única ou várias instâncias do SQL Server
- Implantar, monitorar e atualizar os componentes de camada de dados, como bancos de dados e data warehouses
- Backup e restauração de bancos de dados
- Criar e executar scripts e consultas T-SQL e ver os resultados
- Gerar scripts T-SQL para objetos de banco de dados
- Exibir e editar dados em bancos de dados
- Criar visualmente consultas T-SQL e objetos de banco de dados, como exibições, tabelas e procedimentos armazenados

Ver [o que é o SSMS?](../ssms/sql-server-management-studio-ssms.md) para obter mais informações sobre o SSMS.

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>Instalar a versão mais recente do SQL Server Management Studio (SSMS)

Ao trabalhar com o SQL Server, você deve usar sempre a versão mais recente do SQL Server Management Studio (SSMS). A versão mais recente do SSMS é atualizada continuamente e otimizada e atualmente trabalha com o SQL Server 2017 no Linux. Para baixar e instalar a versão mais recente, consulte [baixar o SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para se manter atualizado, a versão mais recente do SSMS avisará quando há uma nova versão disponível para download.

> [!NOTE]
> Antes de usar o SSMS para gerenciar o Linux, examine os [problemas conhecidos](sql-server-linux-release-notes.md) SSMS no Linux.

## <a name="connect-to-sql-server-on-linux"></a>Conectar-se ao SQL Server no Linux

Use as seguintes etapas básicas para se conectar:

1. Inicie o SSMS ao digitar **Microsoft SQL Server Management Studio** caixa de pesquisa no Windows e, em seguida, clique no aplicativo de área de trabalho.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png)

1. No **conectar ao servidor** janela, insira as informações a seguir (se o SSMS já está em execução, clique em **conectar > mecanismo de banco de dados** para abrir o **conectar ao servidor** janela):

   | Configuração | Description |
   |-----|-----|
   | **Tipo de servidor** | O padrão é o mecanismo de banco de dados; Não altere esse valor. |
   | **Nome do servidor** | Insira o nome do computador do Linux do SQL Server de destino ou seu endereço IP. |
   | **Autenticação** | Para o SQL Server 2017 no Linux, use **autenticação do SQL Server**. |
   | **Logon** | Insira o nome de um usuário com acesso a um banco de dados no servidor (por exemplo, o padrão **SA** conta criada durante a instalação). |
   | **Senha** | Insira a senha para o usuário especificado (para o **SA** conta, você criou esse durante a instalação). |

    ![SQL Server Management Studio: Conectar-se ao servidor de banco de dados SQL](./media/sql-server-linux-manage-ssms/connect.png)

1. Clique em **Conectar**.

    > [!TIP]
    > Se houver uma falha de conexão, primeiro, tente diagnosticar o problema da mensagem de erro. Em seguida, examine as [recomendações de solução de problemas de conexão](sql-server-linux-troubleshooting-guide.md#connection).
 
1. Depois de se conectar ao SQL Server, **Pesquisador de objetos** é aberto e você agora pode acessar seu banco de dados para executar tarefas administrativas ou consultar dados.

## <a name="run-transact-sql-queries"></a>Executar consultas Transact-SQL

Depois de se conectar ao seu servidor, você pode se conectar a um banco de dados e executar consultas Transact-SQL. Consultas Transact-SQL podem ser usadas em quase qualquer tarefa de banco de dados.

1. Na **Pesquisador de objetos**, navegue até o banco de dados de destino no servidor. Por exemplo, expanda **bancos de dados do sistema** para trabalhar com o **mestre** banco de dados.

1. O banco de dados com o botão direito e, em seguida, selecione **nova consulta**.

1. Na janela de consulta, escreva uma consulta de Transact-SQL para selecionar a retornar os nomes de todos os bancos de dados em seu servidor.

   ```sql
   SELECT [Name]
   FROM sys.Databases
   ```

   Se você for inexperiente na gravação de consultas, consulte [escrevendo instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md).

1. Clique o **Execute** botão para executar a consulta e ver os resultados.

   ![Sucesso. Conectar-se ao servidor de banco de dados SQL: SQL Server Management Studio](./media/sql-server-linux-manage-ssms/execute-query.png)

Embora seja possível fazer quase qualquer tarefa de gerenciamento com consultas Transact-SQL, o SSMS é uma ferramenta gráfica que faz é mais fácil de gerenciar o SQL Server. As seções a seguir fornecem alguns exemplos de como usar a interface gráfica do usuário.

## <a name="create-and-manage-databases"></a>Criar e gerenciar bancos de dados

Enquanto estiver conectado para o *mestre* banco de dados, você pode criar bancos de dados no servidor e modificar ou soltar bancos de dados existentes. As etapas a seguir descrevem como realizar várias tarefas de gerenciamento de banco de dados comum por meio do Management Studio. Para executar essas tarefas, verifique se você está conectado para o *mestre* banco de dados com o logon principal no nível de servidor que você criou ao configurar o SQL Server 2017 no Linux.

### <a name="create-a-new-database"></a>Criar um novo banco de dados

1. Inicie o SSMS e conecte-se ao seu servidor no SQL Server 2017 no Linux

2. No Pesquisador de objetos, clique com botão direito no *bancos de dados* pasta e depois clique em * novo banco de dados... "

3. No *novo banco de dados* caixa de diálogo, insira um nome para seu novo banco de dados e, em seguida, clique em *Okey*

O novo banco de dados é criado com êxito em seu servidor. Se você preferir criar um novo banco de dados usando o T-SQL, consulte [criar banco de dados (SQL Server Transact-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md).

### <a name="drop-a-database"></a>Remover um banco de dados

1. Inicie o SSMS e conecte-se ao seu servidor no SQL Server 2017 no Linux

2. No Pesquisador de objetos, expanda o *bancos de dados* pasta para ver uma lista de todos os banco de dados no servidor.

3. No Pesquisador de objetos, clique com botão direito no banco de dados que você deseja remover e, em seguida, clique em *excluir*

4. No *Excluir objeto* caixa de diálogo, verifique *fechar conexões existentes* e, em seguida, clique em *Okey*

O banco de dados é descartado com êxito de seu servidor. Se você preferir descartar um banco de dados usando o T-SQL, consulte [DROP DATABASE (SQL Server Transact-SQL)](../t-sql/statements/drop-database-transact-sql.md).

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>Use o Monitor de atividade para ver informações sobre a atividade do SQL Server

O [Monitor de atividade](../relational-databases/performance-monitor/activity-monitor.md) ferramenta baseia-se ao SQL Server Management Studio (SSMS) e exibe informações sobre processos do SQL Server e como esses processos afetam a instância atual do SQL Server.

1. Inicie o SSMS e conecte-se ao seu servidor no SQL Server 2017 no Linux

1. No Pesquisador de objetos, clique com botão direito do *server* nó e, em seguida, clique *Monitor de atividade*

Monitor de atividade mostra os painéis expansíveis e recolhíveis com as seguintes informações:

- Visão geral
- Processos
- Esperas de recurso
- Arquivo de dados de e/s
- Consultas caras recentes
- Consultas dispendiosas ativas

Quando um painel é expandido, o Monitor de atividade consulta a instância para obter informações. Quando um painel é recolhido, todas as atividades de consulta são interrompidas para esse painel. Você pode expandir um ou mais painéis ao mesmo tempo para exibir diferentes tipos de atividades na instância.

## <a name="see-also"></a>Confira também
- [O que é o SSMS?](../ssms/sql-server-management-studio-ssms.md)
- [Exportar e importar um banco de dados com o SSMS](sql-server-linux-migrate-ssms.md)
- [Tutorial: SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)
- [Tutorial: Gravando instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)
- [Monitoramento de desempenho e atividade de servidor](../relational-databases/performance/server-performance-and-activity-monitoring.md)
