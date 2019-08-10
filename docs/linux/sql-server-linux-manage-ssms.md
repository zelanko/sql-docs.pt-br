---
title: Usar o SSMS para gerenciar o SQL Server em Linux
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 05/21/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.openlocfilehash: 753845d41c946d955b80a927901f827ee4643567
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000096"
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Usar o SQL Server Management Studio no Windows para gerenciar o SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo apresenta o [SSMS (SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md) e descreverá algumas tarefas comuns. O SSMS é um aplicativo do Windows, portanto, use o SSMS quando você tiver um computador Windows que possa se conectar a uma Instância remota do SQL Server em Linux.

> [!TIP]
> Caso não tenha um computador Windows para executar o SSMS, considere o uso do novo [Azure Data Studio](../azure-data-studio/index.md). Ele fornece uma ferramenta gráfica para gerenciar o SQL Server e é executado no Linux e no Windows.

O [SSMS (SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md) faz parte de um conjunto de ferramentas do SQL que a Microsoft oferece gratuitamente para suas necessidades de desenvolvimento e gerenciamento. O SSMS é um ambiente integrado para acessar, configurar, gerenciar, administrar e desenvolver todos os componentes do SQL Server. Ele pode se conectar ao SQL Server em execução em qualquer plataforma local, em contêineres do Docker e na nuvem. Ele também se conecta ao Banco de Dados SQL do Azure e ao SQL Data Warehouse do Azure. O SSMS combina um amplo grupo de ferramentas gráficas com vários editores de script avançados para fornecer acesso ao SQL Server para desenvolvedores e administradores de todos os níveis de habilidades.

O SSMS oferece um amplo conjunto de funcionalidades de desenvolvimento e gerenciamento para o SQL Server, incluindo ferramentas para:

- Configurar, monitorar e administrar uma ou várias instâncias do SQL Server
- Implantar, monitorar e atualizar componentes da camada de dados, como bancos de dados e data warehouses
- Fazer backup e restauração de bancos de dados
- Criar e executar consultas e scripts T-SQL e ver os resultados
- Gerar scripts T-SQL para objetos de banco de dados
- Exibir e editar os dados em uma tabela
- Criar consultas T-SQL e objetos de banco de dados visualmente, como exibições, tabelas e procedimentos armazenados

Confira [O que é o SSMS?](../ssms/sql-server-management-studio-ssms.md) para obter mais informações sobre o SSMS.

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>Instale a última versão do SSMS (SQL Server Management Studio)

Ao trabalhar com o SQL Server, você sempre deverá usar a versão mais recente do SSMS (SQL Server Management Studio). A última versão do SSMS é continuamente atualizada e otimizada e, atualmente, funciona com o SQL Server em Linux. Para baixar e instalar a última versão, confira [Baixar o SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para que você se mantenha atualizado, a última versão do SSMS emite um prompt quando há uma nova versão disponível para download.

> [!NOTE]
> Antes de usar o SSMS para gerenciar o Linux, examine os [problemas conhecidos](sql-server-linux-release-notes.md) do SSMS no Linux.

## <a name="connect-to-sql-server-on-linux"></a>Conectar-se ao SQL Server em Linux

Use as seguintes etapas básicas para se conectar:

1. Inicie o SSMS digitando **Microsoft SQL Server Management Studio** na caixa de pesquisa do Windows e, em seguida, clique no aplicativo da área de trabalho.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png)

1. Na janela **Conectar ao Servidor**, insira as seguintes informações (se o SSMS já estiver em execução, clique em **Conectar > Mecanismo de Banco de Dados** para abrir a janela **Conectar ao Servidor**):

   | Configuração | Descrição |
   |-----|-----|
   | **Tipo de servidor** | O padrão é o mecanismo de banco de dados; não altere esse valor. |
   | **Nome do servidor** | Insira o nome do computador de destino do SQL Server em Linux ou seu endereço IP. |
   | **Autenticação** | Para o SQL Server em Linux, use **Autenticação do SQL Server**. |
   | **Logon** | Insira o nome de um usuário com acesso a um banco de dados no servidor (por exemplo, a conta **SA** padrão criada durante a instalação). |
   | **Senha** | Insira a senha do usuário especificado (para a **conta SA**, você criou isso durante a instalação). |

    ![SQL Server Management Studio: Conectar-se ao servidor do Banco de Dados SQL](./media/sql-server-linux-manage-ssms/connect.png)

1. Clique em **Conectar**.

    > [!TIP]
    > Se houver uma falha de conexão, primeiro, tente diagnosticar o problema da mensagem de erro. Em seguida, examine as [recomendações de solução de problemas de conexão](sql-server-linux-troubleshooting-guide.md#connection).
 
1. Depois que você se conectar com êxito ao SQL Server, o **Pesquisador de Objetos** será aberto e você poderá acessar seu banco de dados para executar tarefas administrativas ou consultar dados.

## <a name="run-transact-sql-queries"></a>Executar consultas Transact-SQL

Depois de se conectar ao servidor, você poderá se conectar a um banco de dados e executar consultas Transact-SQL. As consultas Transact-SQL podem ser usadas para quase todas as tarefas de banco de dados.

1. No **Pesquisador de Objetos**, navegue até o banco de dados de destino no servidor. Por exemplo, expanda **Bancos de Dados do Sistema** para trabalhar com o banco de dados **mestre**.

1. Clique com o botão direito do mouse no banco de dados e, em seguida, selecione **Nova Consulta**.

1. Na janela de consulta, escreva uma consulta Transact-SQL para escolher retornar os nomes de todos os bancos de dados no servidor.

   ```sql
   SELECT [Name]
   FROM sys.Databases
   ```

   Caso não esteja familiarizado com a escrita de consultas, confira [Como escrever instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md).

1. Clique no botão **Executar** para executar a consulta e ver os resultados.

   ![Sucesso. Conectar-se ao servidor do Banco de Dados SQL: SQL Server Management Studio](./media/sql-server-linux-manage-ssms/execute-query.png)

Embora seja possível fazer quase todas as tarefas de gerenciamento com consultas Transact-SQL, o SSMS é uma ferramenta gráfica que facilita o gerenciamento do SQL Server. As seções a seguir fornecem alguns exemplos de como usar a interface gráfica do usuário.

## <a name="create-and-manage-databases"></a>Criar e gerenciar bancos de dados

Enquanto estiver conectado ao banco de dados *mestre*, você poderá criar bancos de dados no servidor e modificar ou remover os bancos de dados existentes. As etapas a seguir descrevem como realizar várias tarefas comuns de gerenciamento de banco de dados por meio do Management Studio. Para executar essas tarefas, verifique se você está conectado ao banco de dados *mestre* com o logon de entidade de segurança no nível do servidor que você criou ao configurar o SQL Server em Linux.

### <a name="create-a-new-database"></a>Criar um novo banco de dados

1. Inicie o SSMS e conecte-se ao servidor no SQL Server em Linux

2. No Pesquisador de Objetos, clique com o botão direito do mouse na pasta *Bancos de Dados* e, em seguida, clique em *Novo Banco de Dados..."

3. Na caixa de diálogo *Novo Banco de Dados*, insira um nome para o novo banco de dados e, em seguida, clique em *OK*

O novo banco de dados será criado com êxito no servidor. Se preferir criar um banco de dados usando o T-SQL, confira [CREATE DATABASE (SQL Server Transact-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md).

### <a name="drop-a-database"></a>Remover um banco de dados

1. Inicie o SSMS e conecte-se ao servidor no SQL Server em Linux

2. No Pesquisador de Objetos, expanda a pasta *Bancos de Dados* para ver uma lista de todos os bancos de dados no servidor.

3. No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados que deseja remover e, em seguida, clique em *Excluir*

4. Na caixa de diálogo *Excluir Objeto*, marque *Fechar conexões existentes* e, em seguida, clique em *OK*

O banco de dados será removido com êxito do servidor. Se preferir remover um banco de dados usando o T-SQL, confira [DROP DATABASE (SQL Server Transact-SQL)](../t-sql/statements/drop-database-transact-sql.md).

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>Use o Monitor de Atividade para ver informações sobre as atividades do SQL Server

A ferramenta [Monitor de Atividade](../relational-databases/performance-monitor/activity-monitor.md) é interna do SSMS (SQL Server Management Studio) e exibe informações sobre os processos do SQL Server e como esses processos afetam a instância atual do SQL Server.

1. Inicie o SSMS e conecte-se ao servidor no SQL Server em Linux

1. No Pesquisador de Objetos, clique com o botão direito do mouse no nó de *servidor* e, em seguida, clique em *Monitor de Atividade*

O Monitor de Atividade mostra painéis expansíveis e recolhíveis com as seguintes informações:

- Visão geral
- Processos
- Esperas de recurso
- E/S de Arquivo de Dados
- Consultas Caras Recentes
- Consultas Caras Ativas

Quando um painel é expandido, o Monitor de Atividade consulta a instância em busca de informações. Quando um painel é recolhido, todas as atividades de consulta são interrompidas para esse painel. Você pode expandir um ou mais painéis ao mesmo tempo para exibir diferentes tipos de atividades na instância.

## <a name="see-also"></a>Confira também
- [O que é o SSMS?](../ssms/sql-server-management-studio-ssms.md)
- [Exportar e importar um banco de dados com o SSMS](sql-server-linux-migrate-ssms.md)
- [Tutorial: SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)
- [Tutorial: Gravando instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)
- [Monitoramento de desempenho e atividade de servidor](../relational-databases/performance/server-performance-and-activity-monitoring.md)
