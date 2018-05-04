---
title: Use o SSMS para gerenciar o SQL Server no Linux | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 08/23/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.technology: database-engine
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.custom: sql-linux
ms.openlocfilehash: 7a09e44b80cdf80b3ce5e033210d0f55276a42b4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Use o SQL Server Management Studio no Windows para gerenciar o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo apresenta [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) e orienta você por algumas tarefas comuns. O SSMS é um aplicativo do Windows, então use SSMS, quando você tiver um computador Windows que pode se conectar a uma instância remota do SQL Server no Linux.

[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) faz parte de um conjunto de ferramentas do SQL que ofertas da Microsoft sem custo para suas necessidades de desenvolvimento e gerenciamento. O SSMS é um ambiente integrado para acessar, configurar, gerenciar, administrar e desenvolver todos os componentes do SQL Server em execução no local ou na nuvem, no Windows, Linux ou Docker no macOS e banco de dados do SQL Azure e o Azure SQL Data Warehouse. O SSMS combina um amplo grupo de ferramentas gráficas com um número de editores de script avançados para fornecer acesso ao SQL Server para desenvolvedores e administradores de todos os níveis.

SSMS oferece um amplo conjunto de recursos de desenvolvimento e gerenciamento para SQL Server, incluindo ferramentas para:

- configurar, monitorar e administrar única ou várias instâncias do SQL Server
- implantar, monitorar e atualizar os componentes da camada de dados, como bancos de dados e data warehouses
- backup e restauração de bancos de dados
- criar e executar scripts e consultas T-SQL e ver os resultados
- Gerar scripts do T-SQL para objetos de banco de dados
- Exibir e editar dados em bancos de dados
- criar visualmente consultas T-SQL e objetos de banco de dados como exibições, tabelas e procedimentos armazenados

Consulte [Use SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/ms174173.aspx) para obter mais informações.

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>Instalar a versão mais recente do SQL Server Management Studio (SSMS)

Ao trabalhar com o SQL Server, você deve usar sempre a versão mais recente do SQL Server Management Studio (SSMS). A versão mais recente do SSMS está sempre atualizada e otimizados e funciona atualmente com o SQL Server 2017 em Linux. Para baixar e instalar a versão mais recente, consulte [baixar o SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para se manter atualizado, a versão mais recente do SSMS avisa você quando há uma nova versão disponível para download. 

## <a name="before-you-begin"></a>Antes de começar
- Consulte [SSMS de uso no Windows para se conectar ao SQL Server no Linux](sql-server-linux-develop-use-ssms.md) como se conectar e consultar usando o SSMS
- Leitura de [problemas conhecidos](sql-server-linux-release-notes.md) para SQL Server 2017 no Linux

## <a name="create-and-manage-databases"></a>Criar e gerenciar bancos de dados
Durante a conexão com o *mestre* banco de dados, você pode criar bancos de dados no servidor e modificar ou remover bancos de dados existentes. As etapas a seguir descrevem como realizar várias tarefas de gerenciamento de banco de dados comum com o Management Studio. Para executar essas tarefas, verifique se você está conectado para o *mestre* banco de dados com o logon principal no nível de servidor que você criou ao configurar o SQL Server 2017 no Linux.

### <a name="create-a-new-database"></a>Criar um novo banco de dados

1. Inicie o SSMS e conectar-se ao seu servidor no SQL Server 2017 no Linux

2. No Pesquisador de objetos, clique duas vezes no *bancos de dados* pasta e depois clique em * novo banco de dados... "

3. No *novo banco de dados* caixa de diálogo, digite um nome para seu novo banco de dados e, em seguida, clique em *Okey*

O novo banco de dados é criado com êxito em seu servidor. Se você preferir criar um novo banco de dados usando o T-SQL, consulte [criar banco de dados (SQL Server Transact-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md).

### <a name="drop-a-database"></a>Remover um banco de dados

1. Inicie o SSMS e conectar-se ao seu servidor no SQL Server 2017 no Linux

2. No Pesquisador de objetos, expanda o *bancos de dados* pasta para ver uma lista de todos os banco de dados no servidor.

3. No Pesquisador de objetos, clique com botão direito no banco de dados que você deseja remover e, em seguida, clique em *excluir*

4. No *Excluir objeto* caixa de diálogo, seleção *fechar conexões existentes* e, em seguida, clique em *Okey*

O banco de dados é removido com êxito do servidor. Se você preferir descartar um banco de dados usando o T-SQL, consulte [DROP DATABASE (SQL Server Transact-SQL)](../t-sql/statements/drop-database-transact-sql.md).

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>Use o Monitor de atividade para obter informações sobre a atividade do SQL Server

O [Monitor de atividade](../relational-databases/performance-monitor/activity-monitor.md) ferramenta é interna no SQL Server Management Studio (SSMS) e exibe informações sobre processos do SQL Server e como esses processos afetam a instância atual do SQL Server.

1. Inicie o SSMS e conectar-se ao seu servidor no SQL Server 2017 no Linux

2. No Pesquisador de objetos, clique com botão direito do *servidor* nó e, em seguida, clique *Monitor de atividade*

Monitor de atividade mostra os painéis expansíveis e recolhíveis com informações sobre o seguinte:
- Visão geral
- Processos
- Esperas de recurso
- E/s de arquivo de dados
- Consultas caras recentes
- Consultas dispendiosas ativas

Quando um painel é expandido, o Monitor de atividade consulta a instância para obter informações. Quando um painel é recolhido, todas as atividades de consulta são interrompidas para esse painel. Você pode expandir um ou mais painéis ao mesmo tempo para exibir diferentes tipos de atividades na instância.

## <a name="see-also"></a>Consulte também
- [Usar o SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/ms174173.aspx)
- [Exportar e importar um banco de dados com o SSMS](sql-server-linux-migrate-ssms.md)
- [Tutorial: SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/bb934498.aspx)
- [Tutorial: Gravando instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)
- [Monitoramento de desempenho e atividade de servidor](../relational-databases/performance/server-performance-and-activity-monitoring.md)
