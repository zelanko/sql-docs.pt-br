---
title: "Notas de versão do SQL Server de 2017 | Microsoft Docs"
ms.custom: 
ms.date: 05/16/2017
ms.prod: sql-server-2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 67c1c0f3a9da6cc5d050da5db8a493f5da934c2a
ms.openlocfilehash: fa45fea4ebb378f035b4b4af2b1fa8a20bc152a5
ms.contentlocale: pt-br
ms.lasthandoff: 06/23/2017

---
# <a name="sql-server-2017-release-notes"></a>Notas de versão do SQL Server de 2017
Este tópico descreve as limitações e problemas com [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]. Para obter informações relacionadas, consulte o seguinte:

- [O que há de novo no SQL Server de 2017](../sql-server/what-s-new-in-sql-server-2017.md).
- [Notas de versão do Linux do SQL Server](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes).
- [Notas de versão do SQL Server Reporting Services](../reporting-services/reporting-services-release-notes.md).

 **Experimente:**    
   -   [![Baixar no Centro de Avaliação](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  Baixar o [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] no **[Centro de Avaliação](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="sql-server-2017-ctp-21-may--2017"></a>2017 CTP 2.1 (maio de 2017) do SQL Server
### <a name="documentation-ctp-21"></a>Documentação (CTP 2.1)
- **Problema e impacto sobre o cliente:** a documentação para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  O conteúdo em artigos que seja específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a**. 
- **Problema e impacto sobre o cliente:** nenhum conteúdo offline está disponível para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **Impacto do problema e o cliente:** se você tiver o SQL Server Reporting Services e Power BI servidor de relatório no mesmo computador e desinstale um deles, você não poderá se conectar ao servidor de relatório restantes com o Gerenciador de configuração de servidor de relatório.
- **Solução alternativa** para contornar esse problema, você deve executar as seguintes operações depois de desinstalar um dos servidores.

    1. Inicie um prompt de comando no modo de administrador.
    2. Vá para o diretório onde o servidor restante do relatório está instalado.

        *Local padrão para o servidor de relatório do Power BI: o servidor de relatório do C:\Program Files\Microsoft Power BI*

        *Local padrão para o SQL Server Reporting Services: C:\Program Files\Microsoft SQL Server Reporting Services*

    3. Em seguida, vá para a próxima pasta. Isso será *SSRS* ou *PBIRS* dependendo de qual é restantes.
    4. Vá para a pasta WMI.
    5. Execute o seguinte comando:

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        Você pode ignorar o erro a seguir, se você vê-lo.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi (CTP 2.1)

- **Impacto do problema e o cliente:** depois de instalar em um computador que tenha uma versão de 2016 do *TSqlLanguageService.msi* instalado (por meio da instalação do SQL ou autônomos redistribuível) as versões v13.* (SQL 2016) *Microsoft.SqlServer.Management.SqlParser.dll* e *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* são removidos. Os aplicativos que têm uma dependência nas versões 2016 desses assemblies, em seguida, deixará de funcionar, fornecendo um erro semelhante a: *erro: não foi possível carregar arquivo ou assembly ' Microsoft.SqlServer.Management.SqlParser, Version = 13.0.0.0, Culture = neutral, PublicKeyToken = 89845dcd8080cc91' ou uma de suas dependências. O sistema não pode localizar o arquivo especificado.*

   Além disso, tentar reinstalar uma versão de 2016 do TSqlLanguageService.msi irá falhar com a mensagem: *Falha na instalação do serviço Microsoft SQL Server 2016 T-SQL Language porque já existe uma versão mais recente no computador*.

- **Solução alternativa** para contornar esse problema e corrigir um aplicativo que depende de v13 versão dos assemblies siga estas etapas:

   1. Vá para **adicionar ou remover programas**
   1. Localizar *vNext do Microsoft SQL Server CTP 2.1 de serviço de linguagem T-SQL*, clique duas vezes e selecione **desinstalação**.
   1. Depois que o componente for removido, reparar o aplicativo que está quebrado (ou reinstalar a versão apropriada do *TSqlLanguageService.MSI*)

   Essa solução alternativa removerá a versão v14 esses assemblies, para que todos os aplicativos que dependem de versões v14 deixará de funcionar. Se esses assemblies são necessários, é necessária uma instalação separada sem qualquer instalação do 2016 lado a lado.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>2017 CTP 2.0 (abril de 2017) do SQL Server
### <a name="documentation-ctp-20"></a>Documentação (CTP 2.0)
- **Problema e impacto sobre o cliente:** a documentação para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  O conteúdo em artigos que seja específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a**. 
- **Problema e impacto sobre o cliente:** nenhum conteúdo offline está disponível para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="always-on-availability-groups"></a>Grupos de disponibilidade AlwaysOn

- **Impacto do problema e o cliente:** instância de um SQL Server que hospeda uma réplica secundária do grupo de disponibilidade falha se a versão principal do SQL Server é menor do que a instância que hospeda a réplica primária. Afeta as atualizações de todas as versões com suporte do SQL Server que hospeda grupos de disponibilidade para o SQL Server [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0. Isso acontece sob as etapas a seguir. 

> 1. Usuário atualiza a instância SQL Server hospedagem réplica secundária de acordo com [práticas recomendadas](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).
> 2. Após a atualização, ocorre um failover e recém-atualizado secundária se torna primária antes de concluir a atualização para todas as réplicas secundárias no grupo de disponibilidade. O antigo primário é agora um secundário que é uma versão inferior primário.
> 3. O grupo de disponibilidade está em uma configuração sem suporte e qualquer réplica secundária restante pode estar vulnerável à falha. 

- **Solução alternativa** conectar-se à instância do SQL Server que hospeda a nova réplica primária e remover a réplica secundária com falha da configuração.

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   Recupera a instância do SQL Server que hospeda a réplica secundária.


![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-14-march--2017"></a>O SQL Server de 2017 CTP 1.4 (março de 2017)

### <a name="documentation-ctp-14"></a>Documentação (CTP 1.4)
- **Problema e impacto sobre o cliente:** a documentação para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  O conteúdo em artigos que seja específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a**. 
- **Problema e impacto sobre o cliente:** nenhum conteúdo offline está disponível para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-13-february--2017"></a>O SQL Server de 2017 CTP 1.3 (fevereiro de 2017)
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

## <a name="sql-server-2017-ctp-12-january--2017"></a>O SQL Server de 2017 CTP 1.2 (janeiro de 2017)
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

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Entre em contato com a equipe de engenharia do SQL Server 
- [Stack Overflow (rótulo sql-server) – faça perguntas técnicas](http://stackoverflow.com/questions/tagged/sql-server)
- [Fóruns do MSDN – faça perguntas técnicas](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect – relatar bugs e solicitar recursos](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit – discussão geral sobre R](https://www.reddit.com/r/SQLServer/)


![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)


