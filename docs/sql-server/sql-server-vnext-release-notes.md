---
title: "Notas de versão do SQL Server vNext | Microsoft Docs"
ms.custom: 
ms.date: 03/12/2017
ms.prod: sql-vnext
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
caps.latest.revision: 41
author: craigg-msft
ms.author: craigg
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 93d6640c3842f36f1da10b035ae32b1f0dfc027b
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-vnext-release-notes"></a>Notas de versão do SQL Server vNext
Este tópico descreve as limitações e problemas com [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

- Para ler o que há de novo nesta versão, consulte [O que há de novo no SQL Server vNext](../sql-server/what-s-new-in-sql-server-vnext.md).
- As[Notas de versão do SQL Server no Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes) estão publicadas em nossa de nova e crescente plataforma de documentação.
- [Notas de versão do SQL Server Reporting Services](../reporting-services/reporting-services-release-notes.md) são publicadas na seção Reporting Services.

 **Experimente:**    
   -   [![Baixar no Centro de Avaliação](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  Baixar o [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] no **[Centro de Avaliação](http://go.microsoft.com/fwlink/?LinkID=829477)**


## <a name="sql-server-vnext-ctp-14-march--2017"></a>SQL Server vNext CTP 1.4 (março de 2017)
### <a name="supported-installation-scenarios-ctp-14"></a>Cenários de instalação com suporte (CTP 1.4)

### <a name="documentation-ctp-14"></a>Documentação (CTP 1.4)
- **Problema e impacto sobre o cliente:** a documentação para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  O conteúdo em artigos que seja específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a**. 
- **Problema e impacto sobre o cliente:** nenhum conteúdo offline está disponível para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-13-february--2017"></a>SQL Server vNext CTP 1.3 (fevereiro de 2017)
### <a name="supported-installation-scenarios-ctp-13"></a>Cenários de instalação com suporte (CTP 1.3)
O[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] destina-se a ser usado apenas como uma versão de teste.  Não há suporte para implantações de produção. É recomentado que você instale e teste [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] em uma máquina virtual.

### <a name="documentation-ctp-13"></a>Documentação (CTP 1.3)
- **Problema e impacto sobre o cliente:** a documentação para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  O conteúdo em artigos que seja específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a**. 
- **Problema e impacto sobre o cliente:** nenhum conteúdo offline está disponível para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-integration-services-ssis-ctp-13"></a>SQL Server Integration Services (SSIS) (CTP 1.3)
#### <a name="cdc-components-not-supported-in-this-ctp-release"></a>Não há suporte para componentes do CDC nesta versão CTP
-   **Problema e impacto sobre o cliente**: não há suporte para o CDC Control Task, CDC Source e CDC Splitter nesta versão CTP.
-   **Solução alternativa**: não há solução alternativa.


![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-12-january--2017"></a>SQL Server vNext CTP 1.2 (janeiro de 2017)
### <a name="supported-installation-scenarios-ctp-12"></a>Cenários de instalação com suporte (CTP 1.2)
O[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] destina-se a ser usado apenas como uma versão de teste.  Não há suporte para implantações de produção. É recomentado que você instale e teste [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] em uma máquina virtual.

### <a name="sql-server-database-engine-ctp-12"></a>Mecanismo de Banco de Dados do SQL Server (CTP 1.2)
- **Problema e impacto sobre o cliente:** em alguns casos, o serviço MSSQLSERVER travará no estado "Iniciando".
- **Solução alternativa:** para contornar este problema:
  -  Crie uma dependência entre o serviço do `mssqlserver` e o serviço do `keyiso` . Uma maneira de fazer isso é executar o comando a seguir em um Prompt de Comando elevado: `sc config mssqlserver depend= keyiso`
  - Reinicialize o computador.

### <a name="documentation-ctp-12"></a>Documentação (CTP 1.2)
- **Problema e impacto sobre o cliente:** a documentação para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  O conteúdo em artigos que seja específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a:**. 
- **Problema e impacto sobre o cliente:** nenhum conteúdo offline está disponível para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
 
### <a name="sql-server-integration-services-ssis-ctp-12"></a>SQL Server Integration Services (SSIS) (CTP 1.2)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>A exclusão do Catálogo do SSIS poderá falhar quando a Expansão do SSIS estiver instalada
**Problema e impacto sobre o cliente**: quando o recurso Expansão do SSIS estiver instalado em um computador, a exclusão do banco de dados do catálogo do SSISDB poderá falhar com o seguinte erro: “Não foi possível remover o logon *'login'* pois o usuário fez logon”.
   
**Solução alternativa**:
-   Em um computador com o Mestre de Expansão, execute o comando “services.msc” para abrir a janela Serviços. Interrompa o serviço Mestre de Cluster do SQL Server Integration Services.
-   Nos computadores de Trabalho de Expansão que se conectam ao mestre, execute o comando “services.msc” para abrir a janela Serviços. Interrompa o serviço Trabalho de Cluster do SQL Server Integration Services.

Agora você poderá excluir o banco de dados do catálogo do SSISDB.

### <a name="sql-server-master-data-services-ctp-12"></a>SQL Server Master Data Services (CTP 1.2)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>A transação pode não funcionar quando o tipo de log de transação de entidade é definido como atributo
**Problema e impacto sobre o cliente:** quando o tipo de log de transação de entidade é definido como **Atributo** em [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] (o valor padrão é **Membro**), os seguintes cenários de falham:

* As transações de alterações de entidade não são exibidas no site.
* Não é possível abrir a página **Transações** no site e reverter uma transação.
* Não é possível atualizar uma entidade com uma anotação de transação no site.

**Solução alternativa**: não há solução alternativa.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>Copiar a versão pode não funcionar quando **Copiar somente versão confirmada** for definido como falso
-  **Problema e impacto sobre o cliente:** quando a configuração **Copiar somente versão confirmada** for definida como **Não** (o valor padrão é **Sim**), a operação de cópia de versão pode falhar. Não há nenhuma mensagem de erro.
-  **Solução alternativa**: não há solução alternativa.

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-11-december--2016"></a>SQL Server vNext CTP 1.1 (dezembro de 2016)
### <a name="supported-installation-scenarios-ctp-11"></a>Cenários de instalação com suporte (CTP 1.1)
O[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] destina-se a ser usado apenas como uma versão de teste.  Não há suporte para implantações de produção. É recomentado que você instale e teste [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] em uma máquina virtual.

Especificamente, embora os cenários a seguir podem funcionar para você, eles não foram minuciosamente testados e **não** têm suporte em [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]:
- Desinstalação do CTP 1.1.
- Instalação lado a lado com qualquer outra versão do SQL Server.
- Atualização de todas as versões anteriores do SQL Server.
- Não há componentes do feature pack do SQL Server disponíveis como parte da instalação [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] .

### <a name="documentation-ctp-11"></a>Documentação (CTP 1.1)
- **Problema e impacto sobre o cliente:** a documentação para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  O conteúdo em artigos que seja específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a:**. 
- **Problema e impacto sobre o cliente:** nenhum conteúdo offline está disponível para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-master-data-services-ctp-11"></a>SQL Server Master Data Services (CTP 1.1)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>A transação pode não funcionar quando o tipo de log de transação de entidade é definido como atributo
**Problema e impacto sobre o cliente:** quando o tipo de log de transação de entidade é definido como **Atributo** em [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] (o valor padrão é **Membro**), os seguintes cenários de falham:

* As transações de alterações de entidade não são exibidas no site.
* Não é possível abrir a página **Transações** no site e reverter uma transação.
* Não é possível atualizar uma entidade com uma anotação de transação no site.

**Solução alternativa**: não há solução alternativa.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>Copiar a versão pode não funcionar quando **Copiar somente versão confirmada** for definido como falso
-  **Problema e impacto sobre o cliente:** quando a configuração **Copiar somente versão confirmada** for definida como **Não** (o valor padrão é **Sim**), a operação de cópia de versão pode falhar. Não há nenhuma mensagem de erro.
-  **Solução alternativa**: não há solução alternativa.

### <a name="sql-server-integration-services-ssis-ctp-11"></a>SQL Server Integration Services (SSIS) (CTP 1.1)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>A exclusão do Catálogo do SSIS poderá falhar quando a Expansão do SSIS estiver instalada
**Problema e impacto sobre o cliente**: quando o recurso Expansão do SSIS estiver instalado em um computador, a exclusão do banco de dados do catálogo do SSISDB poderá falhar com o seguinte erro: “Não foi possível remover o logon *'login'* pois o usuário fez logon”.
   
**Solução alternativa**:
-   Em um computador com o Mestre de Expansão, execute o comando “services.msc” para abrir a janela Serviços. Interrompa o serviço Mestre de Cluster do SQL Server Integration Services.
-   Nos computadores de Trabalho de Expansão que se conectam ao mestre, execute o comando “services.msc” para abrir a janela Serviços. Interrompa o serviço Trabalho de Cluster do SQL Server Integration Services.

Agora você poderá excluir o banco de dados do catálogo do SSISDB.

#### <a name="odbc-components-are-not-supported-in-this-ctp-release"></a>Não há suporte para componentes do ODBC nesta versão CTP
**Problema e impacto sobre o cliente**: não há suporte para o Gerenciador de Conexões ODBC, a Origem nem para o Destino nesta versão CTP.

**Solução alternativa**: não há solução alternativa.

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-10-november-2016"></a>SQL Server vNext CTP 1.0 (novembro de 2016)
### <a name="supported-installation-scenarios-ctp10"></a>Cenários de instalação com suporte (CTP1.0)
O[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] destina-se a ser usado apenas como uma versão de teste.  Não há suporte para implantações de produção. É recomentado que você instale e teste [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] em uma máquina virtual.

Especificamente, embora os cenários a seguir podem funcionar para você, eles não foram minuciosamente testados e **não** têm suporte em [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]:
- Desinstalação do CTP 1.0.
- Instalação lado a lado com qualquer outra versão do SQL Server.
- Atualização de todas as versões anteriores do SQL Server.
- Não há componentes do feature pack do SQL Server disponíveis como parte da instalação [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] .

### <a name="documentation-ctp-10"></a>Documentação (CTP 1.0)
- **Problema e impacto sobre o cliente:** a documentação para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  O conteúdo em artigos que seja específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a:**. 
- **Problema e impacto sobre o cliente:** nenhum conteúdo offline está disponível para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-database-engine-ctp-10"></a>Mecanismo de Banco de Dados do SQL Server (CTP 1.0)
-  **Problema e impacto sobre o cliente:** a função `STRING_AGG` no CTP1 retorna um tipo LOB como resultado (por exemplo, `NVARCHAR(MAX)`). Em uma versão futura do CTP, esse comportamento poderá mudar e `STRING_AGG` poderá retornar `NVARCHAR(4000)` se os valores de entrada não forem tipos LOB. Um erro de estouro poderá ser gerado se os resultados concatenados não couberem em `NVARCHAR(4000)`.

-  **Problema e impacto sobre o cliente:** evitar o uso de palavras-chave não reservadas, tais como `WITHIN`, como um alias para expressões `STRING_AGG`. (Por exemplo, `SELECT Company.Name, STRING_AGG(Product.Name, ',') AS WITHIN FROM TableA;`.) Em uma versão futura do CTP, o token `WITHIN` após a chamada `STRING_AGG` poderá ser usado como parte da função `STRING_AGG`.

-  **Solução alternativa:** evitar usar o alias `WITHIN` ou adicionar `AS WITHIN` como uma especificação de alias para evitar colisões com alterações futuras que poderão ser adicionadas na função `STRING_AGG`.


### <a name="sql-server-integration-services-ctp-10"></a>SQL Server Integration Services (CTP 1.0)
#### <a name="stop-operation-in-ssis-catalog-may-fail"></a>A Operação de interrupção no Catálogo do SSIS pode falhar
**Problema e impacto sobre o cliente:** a interrupção de uma operação em [!INCLUDE[ssIS_md](../includes/ssis-md.md)] usando [!INCLUDE[ssManStudio_md](../includes/ssmanstudio-md.md)] ou o procedimento armazenado catalog.stop_operation pode falhar com o seguinte erro: "Ocorreu um erro do .NET Framework durante a execução da rotina definida pelo usuário ou da 'stop_operation_internal' agregada".

-  **Solução alternativa:** Abrir o Gerenciador de tarefas do Windows. Na guia **Processos** , localize o processo nomeado **ISServerExec** e clique em **Finalizar tarefa** para finalizar o processo.

#### <a name="create-dump-of-ssis-pacakge-execution-may-fail"></a>Criar despejo da Execução de Pacote SSIS pode falhar
**Problema e impacto sobre o cliente:** a criação de um despejo para a execução de um pacote, usando o procedimento armazenado catalog.create_execution_dump, pode falhar com o seguinte erro: "Ocorreu um erro do .NET Framework durante a execução da rotina definida pelo usuário ou da 'create_execution_dump_internal' agregada".

-  **Solução alternativa:** Abrir o Gerenciador de tarefas do Windows. Na guia **processos** , localize o processo nomeado **ISServerExec**, clique com botão direito do mouse no processo e, em seguida, clique em **Criar arquivo de despejo**.

#### <a name="get-perf-counter-of-ssis-package-execution-may-fail"></a>A obtenção do Contador de desempenho da Execução de pacote SSIS pode falhar
**Problema e impacto sobre o cliente:** a consulta dos contadores de desempenho [!INCLUDE[ssIS_md](../includes/ssis-md.md)] , usando a função com valor de tabela catalog.dm_execution_performance_counters, pode falhar com o seguinte erro: "Ocorreu um erro do .NET Framework durante a execução da rotina definida pelo usuário ou da 'get_execution_perf_counters' agregada".

-  **Solução alternativa**: usar o Monitor de desempenho do Windows para monitorar diretamente os valores dos contadores de desempenho. Não há nenhuma solução alternativa para os contadores de desempenho que são para uma execução de pacote específica.

#### <a name="deleting-catalog-may-fail-when-ssis-scale-out-master-is-installed"></a>A Exclusão do catálogo pode falhar quando o Mestre de Expansão do SSIS estiver instalado
**Problema e impacto sobre o cliente:** quando o recurso Expansão [!INCLUDE[ssIS_md](../includes/ssis-md.md)] está instalado em um computador, a exclusão do catálogo **SSISDB** pode falhar com o seguinte erro: "não foi possível removerr o logon '...' pois o usuário fez logon”. 

**Solução alternativa**: 
* Em um computador Mestre de Expansão, execute o comando "services.msc" para abrir a janela **Serviços** e interrompa o serviço **SQL Server Integration Services Cluster Master** . 

* Em computadores Trabalho de Expansão que se conectam ao mestre, execute o comando "services.msc" para abrir a janela **Serviços** . Interrompa o serviço **SQL Server Integration Services Cluster Worker** . 

Agora é possível excluir o catálogo **SSISDB** .

#### <a name="odbc-connector-in-ssis-is-not-supported"></a>Não há suporte para o conector ODBC no SSIS
-  **Problema e impacto sobre o cliente:** não há suporte para o conector ODBC no [!INCLUDE[ssIS_md](../includes/ssis-md.md)] .
-  **Solução alternativa:** não há.

### <a name="sql-server-reporting-services-ctp-10"></a>SQL Server Reporting Services (CTP 1.0)

O SQL Server Reporting Services não está lançando nenhum recurso novo para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-master-data-services-ctp-10"></a>SQL Server Master Data Services (CTP 1.0)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>A transação pode não funcionar quando o tipo de log de transação de entidade é definido como atributo
**Problema e impacto sobre o cliente:** quando o tipo de log de transação de entidade é definido como **Atributo** em [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] (o valor padrão é **Membro**), os seguintes cenários de falham:

* As transações de alterações de entidade não são exibidas no site.
* Não é possível abrir a página **Transações** no site e reverter uma transação.
* Não é possível atualizar uma entidade com uma anotação de transação no site.

**Solução alternativa**: não há solução alternativa.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>Copiar a versão pode não funcionar quando **Copiar somente versão confirmada** for definido como falso
**Problema e impacto sobre o cliente:** quando a configuração **Copiar somente versão confirmada** for definida como **Não** (o valor padrão é **Sim**), a operação de cópia de versão pode falhar. Não há nenhuma mensagem de erro.

**Solução alternativa**: não há solução alternativa.
 
### <a name="sql-server-management-studio-ssms-ctp-10"></a>SSMS (SQL Server Management Studio) (CTP 1.0)
O SQL Server Management Studio é um download separado.  Para obter as informações mais recentes, consulte [SQL Server Management Studio – Notas de Versão](https://msdn.microsoft.com/library/mt238486.aspx).

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Entre em contato com a equipe de engenharia do SQL Server 
- [Stack Overflow (rótulo sql-server) – faça perguntas técnicas](http://stackoverflow.com/questions/tagged/sql-server)
- [Fóruns do MSDN – faça perguntas técnicas](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect – relatar bugs e solicitar recursos](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit – discussão geral sobre R](https://www.reddit.com/r/SQLServer/)


![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)


