---
title: Notas de Versão do SQL Server 2017 | Microsoft Docs
description: Este artigo descreve as limitações e problemas com o SQL Server 2017 e fornece links para informações relacionadas.
ms.custom: ''
ms.date: 11/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-2017
ms.openlocfilehash: 83829530014c83279bcde7dc8aa4be17496bdf50
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97409482"
---
# <a name="sql-server-2017-release-notes"></a>Notas de Versão do SQL Server 2017
[!INCLUDE[SQL Server 2017](../includes/applies-to-version/sqlserver2017.md)]
Este tópico descreve as limitações e os problemas com o SQL Server 2017. Para obter informações relacionadas. consulte:
- [Novidades no SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)
- [Notas de versão do SQL Server no Linux](../linux/sql-server-linux-release-notes.md)
- [Atualizações cumulativas do SQL Server 2017](https://aka.ms/sql2017cu) para obter informações sobre a última versão de atualização cumulativa

**Experimente o SQL Server!**
- [![Baixar da Central de Avaliação](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=829477) [Baixar o SQL Server 2017](https://go.microsoft.com/fwlink/?LinkID=829477)
- [![Criar máquina virtual](../includes/media/azure-vm.png)](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) [Configurar uma máquina virtual com o SQL Server 2017](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)

> [!NOTE]
> Agora a versão prévia do SQL Server 2019 está disponível. Para obter mais informações, consulte [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15).

## <a name="sql-server-2017---general-availability-release-october-2017"></a>SQL Server 2017 – versão de disponibilidade geral (outubro de 2017)
### <a name="database-engine"></a>Mecanismo de Banco de Dados

- **Problema e impacto ao cliente:** após a atualização, o compartilhamento de rede existente do FILESTREAM pode não estar mais disponível.

- **Solução alternativa:** primeiro, reinicialize o computador e verifique se o compartilhamento de rede do FILESTREAM está disponível. Se o compartilhamento ainda não estiver disponível, conclua as seguintes etapas:

    1. No SQL Server Configuration Manager, clique com o botão direito do mouse na instância do SQL Server e clique em **Propriedades**. 
    2. Na guia **FILESTREAM**, desmarque **Habilitar FILESTREAM para acesso de fluxo de E/S de arquivo** e, em seguida, clique em **Aplicar**.
    3. Marque **Habilitar FILESTREAM para acesso de fluxo de E/S de arquivo** novamente com o nome original do compartilhamento e clique em **Aplicar**.

### <a name="master-data-services-mds"></a>Master Data Services (MDS)
- **Problema e impacto ao cliente:**  na página de permissões do usuário, ao conceder permissão para o nível raiz no modo de exibição de árvore da entidade, você pode ver o seguinte erro: `"The model permission cannot be saved. The object guid is not valid"`

- **Solução alternativa:** 
  - Conceder permissão aos sub-nós no modo de exibição de árvore, em vez do nível raiz.

### <a name="analysis-services"></a>Serviços de análise
- **Problema e impacto ao cliente:** os conectores de dados das fontes a seguir ainda não estão disponíveis para modelos de tabela no nível de compatibilidade 1400.
  - Amazon Redshift
  - IBM Netezza
  - Impala
- **Solução alternativa:** Nenhum.   

- **Problema e impacto ao cliente:** modelos de consulta direta no nível de compatibilidade 1400 com perspectivas podem falhar em consultas ou descoberta de metadados.
- **Solução alternativa:** remova as perspectivas e implante-as novamente.

### <a name="tools"></a>Ferramentas
- **Problema e impacto ao cliente:** Falha na execução de *DReplay* com a seguinte mensagem: “Ocorreu um erro inesperado em DReplay!”.
- **Solução alternativa:** Nenhum.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-release-candidate-rc2---august-2017"></a>SQL Server 2017 versão Release Candidate (RC2 – agosto de 2017)
Não há nenhuma nota de versão do SQL Server no Windows relacionada a essa versão. Consulte [Notas de versão do SQL Server no Linux](../linux/sql-server-linux-release-notes.md).


![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-release-candidate-rc1---july-2017"></a>SQL Server 2017 versão Release Candidate (RC1 – julho de 2017)
### <a name="sql-server-integration-services-ssis-rc1---july-2017"></a>SQL Server Integration Services (SSIS) (RC1 – julho de 2017)
- **Problema e impacto ao cliente:** O parâmetro *runincluster* do procedimento armazenado **[catalog].[create_execution]** foi renomeado como *runinscaleout*, a fim de obter consistência e legibilidade.
- **Solução alternativa:** Se você tiver scripts existentes para executar pacotes no Scale Out, precisará alterar o nome do parâmetro de *runincluster* para *runinscaleout* para que os scripts funcionem no RC1.

- **Problema e impacto ao cliente:** O SSMS (SQL Server Management Studio) 17.1 e versões anteriores não pode disparar a execução de pacote no Scale Out no RC1. A mensagem de erro é: " *\@runincluster* não é parâmetro para o procedimento **create_execution**". Esse problema é corrigido na próxima versão do SSMS, a versão 17.2. A versão 17.2 e posteriores do SSMS oferecem suporte ao novo nome de parâmetro e execução de execução em Scale Out. 
- **Solução alternativa:** até a versão 17.2 do SSMS estar disponível:
  1. Use sua versão existente do SSMS para gerar o script de execução do pacote.
  2. Altere o nome do parâmetro *runincluster* para *runinscaleout* no script.
  3. Execute o script.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 2017 CTP 2.1 (maio de 2017)
### <a name="documentation-ctp-21"></a>Documentação (CTP 2.1)
- **Problema e impacto ao cliente:** A documentação do [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada, e o conteúdo está incluído no conjunto de documentação do [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)].  O conteúdo em artigos que for específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a**. 
- **Problema e impacto ao cliente:** Nenhum conteúdo offline está disponível para o [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **Problema e impacto ao cliente:** se você tiver o SQL Server Reporting Services e o Servidor de Relatórios do Power BI no mesmo computador e desinstalar um deles, não poderá se conectar ao outro servidor de relatório com o Gerenciador de Configurações do Servidor de Relatório.
- **Solução alternativa** Para contornar esse problema, você deve executar as seguintes operações depois de desinstalar um dos servidores.

    1. Abra um prompt de comando no modo de administrador.
    2. Vá para o diretório onde o servidor de relatório remanescente está instalado.

        *Local padrão do Servidor de Relatórios do Power BI: C:\Arquivos de Programas\Servidor de Relatórios do Microsoft Power BI*

        *Local padrão do SQL Server Reporting Services: C:\Arquivos de Programas\Microsoft SQL Server Reporting Services*

    3. Em seguida, vá para a próxima pasta, que pode ser *SSRS* ou *PBIRS*, dependendo de qual restou.
    4. Vá para a pasta WMI.
    5. Execute o comando a seguir:

        ```console
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        Se você vir o erro a seguir, ignore-o.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi (CTP 2.1)

- **Problema e impacto ao cliente:** depois de instalar em um computador que tenha uma versão de 2016 do *TSqlLanguageService.msi* instalado (por meio da Instalação do SQL ou como um redistribuível anônimo), as versões v13.* (SQL 2016) *Microsoft.SqlServer.Management.SqlParser.dll* e *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* são removidas. Qualquer aplicativo que tem uma dependência nas versões de 2016 desses assemblies param de funcionar e geram um erro semelhante a este: *erro: Não foi possível carregar o arquivo ou o assembly “Microsoft.SqlServer.Management.SqlParser, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91” ou uma de suas dependências. O sistema não pôde localizar o arquivo especificado.*

   Além disso, tentativas de reinstalar uma versão de 2016 do TSqlLanguageService.msi falham com a mensagem: *Falha na instalação do Serviço de Linguagem T-SQL do Microsoft SQL Server 2016 porque já existe uma versão mais recente no computador*.

- **Solução alternativa** Para contornar esse problema e corrigir um aplicativo que depende da versão v13 dos assemblies, siga estas etapas:

   1. Vá para **Adicionar ou Remover Programas**
   2. Localize *Serviço de Linguagem T-SQL do Microsoft SQL Server 2019 CTP2.1*, clique com o botão direito do mouse nele e selecione **Desinstalar**.
   3. Depois da remoção do componente, repare o aplicativo defeituoso ou reinstale a versão apropriada do *TSqlLanguageService.MSI*.

   Essa solução alternativa remove a versão v14 desses assemblies, assim, todos os aplicativos que dependem de versões v14 deixam de funcionar. Se esses assemblies forem necessários, será necessária uma instalação separada sem instalações 2016 lado a lado separadas.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 2017 CTP 2.0 (abril de 2017)
### <a name="documentation-ctp-20"></a>Documentação (CTP 2.0)
- **Problema e impacto ao cliente:** A documentação do [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] é limitada, e o conteúdo está incluído no conjunto de documentação do [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)].  O conteúdo em artigos que for específico a [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] será anotado com **Aplica-se a**. 
- **Problema e impacto ao cliente:** Nenhum conteúdo offline está disponível para o [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="always-on-availability-groups"></a>Grupos de disponibilidade AlwaysOn

- **Problema e impacto ao cliente:** uma instância do SQL Server que hospeda uma réplica secundária do grupo de disponibilidade falhará se a versão principal do SQL Server for menor do que da instância que hospeda a réplica primária. Afeta os upgrades de todas as versões compatíveis do SQL Server que hospeda grupos de disponibilidade para o SQL Server [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0. O problema ocorre nas condições descritas a seguir. 

> 1. O usuário faz upgrade da instância do SQL Server que hospeda a réplica secundária de acordo com as [práticas recomendadas](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).
> 2. Após o upgrade, ocorre um failover e uma instância secundária recém-atualizada se torna a primária antes de concluir o upgrade para todas as réplicas secundárias no grupo de disponibilidade. A primária antiga agora será uma secundária com versão inferior à primária.
> 3. O grupo de disponibilidade está em uma configuração incompatível e as réplicas secundárias restantes pode estar vulnerável a falhas. 

- **Solução alternativa** Conecte-se à instância do SQL Server que hospeda a nova réplica primária e remova a réplica secundária com falha da configuração.

   ```sql
   ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName;
   ```

   A instância do SQL Server que hospeda a réplica secundária é recuperada.

## <a name="more-information"></a>Mais informações
- [Notas de versão do SQL Server Reporting Services](../reporting-services/release-notes-reporting-services.md).
- [Problemas Conhecidos de Serviços de Machine Learning](../machine-learning/troubleshooting/known-issues-for-sql-server-machine-learning-services.md)
- [Centro de atualização do SQL Server – links e informações para todas as versões com suporte](../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)