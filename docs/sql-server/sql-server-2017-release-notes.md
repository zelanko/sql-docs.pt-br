---
title: "Notas de Versão do SQL Server 2017 | Microsoft Docs"
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
ms.translationtype: HT
ms.sourcegitcommit: 6aa73e749d4f308265dfe27a160802c15a391a3e
ms.openlocfilehash: a2950b6aef0e12653efbb9eb26fd3f1ae6cb951e
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="sql-server-2017-release-notes"></a>Notas de Versão do SQL Server 2017
Este tópico descreve as limitações e problemas com [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]. Para obter informações relacionadas, consulte os artigos a seguir:

- [Novidades no SQL Server de 2017](../sql-server/what-s-new-in-sql-server-2017.md).
- [Notas de versão do SQL Server no Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes).
- [Notas de versão do SQL Server Reporting Services](../reporting-services/reporting-services-release-notes.md).

 **Experimente:**    
   -   [![Baixar no Centro de Avaliação](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  Baixar o [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] no **[Centro de Avaliação](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="sql-server-2017-release-candidate-rc1---july-2017"></a>SQL Server 2017 versão Release Candidate (RC1 – julho de 2017)

### <a name="sql-server-integration-services-ssis-rc1---july-2017"></a>SQL Server Integration Services (SSIS) (RC1 – julho de 2017)
- **Problema e impacto sobre o cliente:** o parâmetro *runincluster* do procedimento armazenado **[catalog].[create_execution]** foi renomeado como *runinscaleout*, a fim de obter consistência e legibilidade.
- **Solução alternativa:** se você tiver scripts existentes para executar pacotes no Scale Out, será necessário alterar o nome do parâmetro de *runincluster* para *runinscaleout* para que os scripts funcionem no RC1.

- **Problema e impacto sobre o cliente:** no SQL Server Management Studio (SSMS) 17.1 e versões anteriores, não é possível disparar a execução do pacote em Scale Out no RC1. A mensagem de erro é: "*@runincluster* não é um parâmetro para o procedimento **create_execution**." Esse problema é corrigido na próxima versão do SSMS, a versão 17.2. A versão 17.2 e posteriores do SSMS oferecem suporte ao novo nome de parâmetro e execução de execução em Scale Out. 
- **Solução alternativa:** até a versão 17.2 do SSMS ser disponibilizada, é possível usar a versão existente do SSMS para gerar o script de execução do pacote e, em seguida, alterar o nome do parâmetro *runincluster* para *runinscaleout* no script e executá-lo.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 2017 CTP 2.1 (maio de 2017)
### <a name="documentation-ctp-21"></a>Documentação (CTP 2.1)
- **Problema e impacto sobre o cliente:** a documentação para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  O conteúdo em artigos que seja específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a**. 
- **Problema e impacto sobre o cliente:** nenhum conteúdo offline está disponível para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **Impacto do problema e para o cliente:** se você tiver o SQL Server Reporting Services e o Servidor de Relatório do Power BI no mesmo computador e desinstalar um deles, não será possível se conectar ao outro servidor de relatório com o Report Server Configuration Manager.
- **Solução alternativa** Para contornar esse problema, você deve executar as seguintes operações depois de desinstalar um dos servidores.

    1. Abra um prompt de comando no modo de administrador.
    2. Vá para o diretório onde o servidor de relatório remanescente está instalado.

        *Local padrão para o Servidor de Relatório do Power BI: C:\Arquivos de Programas\Microsoft Power BI Report Server*

        *Local padrão para o SQL Server Reporting Services: C:\Arquivos de Programas\Microsoft SQL Server Reporting Services*

    3. Em seguida, vá para a próxima pasta. Ela será *SSRS* ou *PBIRS* dependendo de qual é o servidor remanescente.
    4. Vá para a pasta WMI.
    5. Execute o seguinte comando:

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        Você pode ignorar o erro a seguir, se ele aparecer.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi (CTP 2.1)

- **Impacto do problema e para o cliente:** depois de instalar em um computador que tenha uma versão de 2016 do *TSqlLanguageService.msi* instalado (por meio da Instalação do SQL ou redistribuível anônimo), as versões v13.* (SQL 2016) *Microsoft.SqlServer.Management.SqlParser.dll* e *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* são removidas. Os aplicativos que têm uma dependência nas versões 2016 desses assemblies deixarão de funcionar, mostrando um erro semelhante a: *Erro: não foi possível carregar o arquivo ou o assembly 'Microsoft.SqlServer.Management.SqlParser, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' ou uma de suas dependências. O sistema não pôde localizar o arquivo especificado.*

   Além disso, tentativas de reinstalar uma versão de 2016 do TSqlLanguageService.msi falharão com a mensagem: *Falha na instalação do Serviço de Linguagem T-SQL do Microsoft SQL Server 2016 porque já existe uma versão mais recente no computador*.

- **Solução alternativa** Para contornar esse problema e corrigir um aplicativo que depende da versão v13 dos assemblies, siga estas etapas:

   1. Vá para **Adicionar ou Remover Programas**
   1. Localize *Serviço de Linguagem T-SQL do Microsoft SQL Server vNext CTP2.1*, clique com o botão direito do mouse nele e selecione **Desinstalar**.
   1. Depois que o componente for removido, repare o aplicativo defeituoso (ou reinstale a versão apropriada do *TSqlLanguageService.MSI*)

   Essa solução alternativa removerá a versão v14 esses assemblies, de forma que todos os aplicativos que dependem de versões v14 deixarão de funcionar. Se esses assemblies forem necessários, será necessária uma instalação separada sem instalações 2016 lado a lado separadas.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 2017 CTP 2.0 (abril de 2017)
### <a name="documentation-ctp-20"></a>Documentação (CTP 2.0)
- **Problema e impacto sobre o cliente:** a documentação para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  O conteúdo em artigos que seja específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a**. 
- **Problema e impacto sobre o cliente:** nenhum conteúdo offline está disponível para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="always-on-availability-groups"></a>Grupos de disponibilidade AlwaysOn

- **Impacto do problema e para o cliente:** uma instância do SQL Server que hospeda uma réplica secundária do grupo de disponibilidade falhará se a versão principal do SQL Server for menor do que da instância que hospeda a réplica primária. Afeta os upgrades de todas as versões compatíveis do SQL Server que hospeda grupos de disponibilidade para o SQL Server [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0. Isso acontece conforme as etapas a seguir. 

> 1. O usuário faz upgrade da instância do SQL Server que hospeda a réplica secundária de acordo com as [práticas recomendadas](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).
> 2. Após o upgrade, ocorrerá um failover e a instância secundária recém-atualizada se torna a primária antes de concluir o upgrade para todas as réplicas secundárias no grupo de disponibilidade. A primária antiga agora será uma secundária de versão inferior à primária.
> 3. O grupo de disponibilidade está em uma configuração incompatível e as réplicas secundárias restantes pode estar vulnerável a falhas. 

- **Solução alternativa** Conecte-se à instância do SQL Server que hospeda a nova réplica primária e remova a réplica secundária com falha da configuração.

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   A instância do SQL Server que hospeda a réplica secundária é recuperada.

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Entre em contato com a equipe de engenharia do SQL Server 
- [Stack Overflow (rótulo sql-server) – faça perguntas técnicas](http://stackoverflow.com/questions/tagged/sql-server)
- [Fóruns do MSDN – faça perguntas técnicas](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect – relatar bugs e solicitar recursos](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit – discussão geral sobre R](https://www.reddit.com/r/SQLServer/)

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
