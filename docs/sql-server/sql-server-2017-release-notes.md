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
ms.translationtype: HT
ms.sourcegitcommit: 6aa73e749d4f308265dfe27a160802c15a391a3e
ms.openlocfilehash: a2950b6aef0e12653efbb9eb26fd3f1ae6cb951e
ms.contentlocale: pt-br
ms.lasthandoff: 07/17/2017

---
# <a name="sql-server-2017-release-notes"></a>Notas de versão do SQL Server de 2017
Este tópico descreve as limitações e problemas com [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]. Para obter informações relacionadas, consulte os artigos a seguir:

- [O que há de novo no SQL Server de 2017](../sql-server/what-s-new-in-sql-server-2017.md).
- [Notas de versão do Linux do SQL Server](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes).
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

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Entre em contato com a equipe de engenharia do SQL Server 
- [Stack Overflow (rótulo sql-server) – faça perguntas técnicas](http://stackoverflow.com/questions/tagged/sql-server)
- [Fóruns do MSDN – faça perguntas técnicas](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect – relatar bugs e solicitar recursos](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit – discussão geral sobre R](https://www.reddit.com/r/SQLServer/)

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
