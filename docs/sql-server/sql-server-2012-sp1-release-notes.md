---
title: "Notas de Versão do SQL Server 2012 SP1 | Microsoft Docs"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 72171357-28de-4edd-bdfd-194f97225a6f
caps.latest.revision: "49"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d0e126678e921a47135ada143b1dba53a467df7d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-2012-sp1-release-notes"></a>SQL Server 2012 SP1 Release Notes
Este documento de Notas de Versão descreve problemas conhecidos sobre os quais você deve ler antes de instalar ou solucionar problemas do [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 1. Este documento de Notas de versão está disponível somente online, não em mídia de instalação, e é atualizado periodicamente.  
  
## <a name="bkmk_top"></a>Conteúdo  
[1.0 Antes da instalação](#bmk_Install)  
  
[2.0 Analysis Services e PowerPivot](#bkmk_AS)  
  
[3.0 Reporting Services](#bkmk_RS)  
  
[4.0 Data Quality Services](#bkmk_DQS)  
  
[5.0 SQL Server Express](#bkmk_Express)  
  
[6.0 Serviço Change Data Capture e Designer para Oracle da Attunity](#bkmk_CDC)  
  
[7.0 Estrutura de Aplicativo da Camada de Dados do SQL Server (DACFx)](#DACFx)  
  
[8.0 Problemas conhecidos corrigidos neste Service Pack](#bkmk_known_issues_fixed)  
  
## <a name="bmk_Install"></a>1.0 Antes da instalação  
Antes de instalar o SQL Server 2012 SP1, considere as seguintes informações.  
  
### <a name="11-reinstalling-an-instance-of-sql-server-failover-custer-fails-if-you-use-the-same-ip-address"></a>1.1 A reinstalação de uma instância do cluster de failover do SQL Server falhará se você usar o mesmo endereço IP  
**Problema:** se você especificar um endereço IP incorreto durante uma instalação da instância do cluster de failover do SQL Server, a instalação falhará. Depois que você desinstalar a instância com falha, e se tentar reinstalar a instância do cluster de failover do SQL Server com o mesmo nome de instância e o endereço de IP correto, a instalação falhará. A falha ocorre devido ao grupo de recursos duplicado por trás da instalação anterior.  
  
**Solução alternativa:** para resolver esse problema, use um nome de instância diferente durante a reinstalação, ou exclua manualmente o grupo de recursos antes de reinstalar. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server](http://msdn.microsoft.com/library/ms191545).  
  
### <a name="12-choose-the-correct-file-to-download-and-install"></a>1.2 Escolha o arquivo correto para baixar e instalar  
Use a tabela a seguir para determinar qual arquivo baixar e instalar. Verifique se você tem os requisitos de sistema corretos antes de instalar o service pack. Os requisitos de sistemas são fornecidos nas páginas de download vinculadas na tabela.  
  
|Se a versão instalada atual for...|E você quiser...|Baixar e instalar...|  
|-------------------------------------------|----------------------|---------------------------|  
|**Instalações de&32; bits:**|||  
|Uma versão de 32 bits de qualquer edição do SQL Server 2012|Atualizar para a versão de 32 bits do SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 32 Bits do SQL Server 2012 RTM Express|Atualizar para a versão de 32 bits do SQL Server 2012 Express SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 32 bits de somente ferramentas do cliente e de gerenciamento para SQL Server 2012 (incluindo SQL Server 2012 Management Studio)|Atualizar as ferramentas do cliente e de gerenciamento para a versão de 32 bits do SQL Server 2012 SP1|SQLManagementStudio_x86_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Uma versão de 32 bits do SQL Server 2012 Management Studio Express|Atualizar a versão de 32 bits do SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x86_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Uma versão de 32 bits de qualquer edição do SQL Server 2012 **e** uma versão de 32 bits do cliente e das ferramentas de gerenciamento (incluindo SQL Server 2012 RTM Management Studio)|Atualizar todos os produtos para a versão de 32 bits do SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 32 bits de uma ou mais ferramentas do [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/details.aspx?id=16978)|Atualizar as ferramentas para a versão de 32 bits do Microsoft SQL Server 2012 SP1 Feature Pack|Um ou mais arquivos do [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|  
|Nenhuma instalação de 32 bits do SQL Server 2012|Instalar a versão de 32 bits do SQL Server 2012 incluindo o SP1 (nova instância com SP1 pré-instalado)|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **e** SQLServer2012SP1-FullSlipstream-x86-ENU.box [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Nenhuma instalação de 32 bits do SQL Server 2012 Management Studio|Instalar a versão de 32 bits do SQL Server 2012 Management Studio incluindo SP1|SQLManagementStudio_x86_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|Nenhuma versão de 32 Bits do SQL Server 2012 RTM Express|Instalar a versão de 32 bits do SQL Server 2012 Express incluindo SP1|SQLEXPR32_x86_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|Uma instalação de 32 bits do **SQL Server 2008** ou do **SQL Server 2008 R2**|**Atualização in-loco** para a versão de 32 bits do SQL Server 2012 com SP1|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **e** SQLServer2012SP1-FullSlipstream-x86-ENU.box [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|**Instalações de&64; bits:**|||  
|Uma versão de 64 bits de qualquer edição do SQL Server 2012|Atualizar para a versão de 64 bits do SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 64 Bits do SQL Server 2012 RTM Express|Atualizar para a versão de 64 bits do SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 64 bits com somente o cliente e as ferramentas de gerenciamento para SQL Server 2012 SQL (incluindo SQL Server 2012 Management Studio)|Atualizar o cliente e as ferramentas de gerenciamento para a versão de 64 bits do SQL Server 2012 SP1|SQLManagementStudio_x64_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Uma versão de 64 bits do SQL Server 2012 Management Studio Express|Atualizar a versão de 64 bits do SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x64_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Uma versão de 64 bits de qualquer edição do SQL Server 2012 **e** uma versão de 64 bits do cliente e das ferramentas de gerenciamento (incluindo SQL Server 2012 RTM Management Studio)|Atualizar todos os produtos para a versão de 64 bits do SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 64 bits de uma ou mais ferramentas do [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/en/details.aspx?id=16978)|Atualizar as ferramentas para a versão de 64 bits do Microsoft SQL Server 2012 SP1 Feature Pack|Um ou mais arquivos do [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|  
|Nenhuma instalação de 64 bits do SQL Server 2012|Instalar a versão de 64 bits do SQL Server 2012 incluindo o SP1 (nova instância com SP1 pré-instalado)|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **e** SQLServer2012SP1-FullSlipstream-x64-ENU.box [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Nenhuma instalação de 64 bits do SQL Server 2012 Management Studio|Instalar a versão de 64 bits do SQL Server 2012 Management Studio incluindo SP1|SQLManagementStudio_x64_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Nenhuma versão de 64 Bits do SQL Server 2012 RTM Express|Instalar a versão de 64 bits do SQL Server 2012 Express incluindo SP1|SQLEXPR_x64_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Uma instalação de 64 bits do **SQL Server 2008** ou do **SQL Server 2008 R2**|**Atualização in-loco** para a versão de 64 bits do SQL Server 2012 com SP1|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **e** SQLServer2012SP1-FullSlipstream-x64-ENU.box [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
  
![Ícone de seta usado com o link Voltar ao Início](../sql-server/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início")[Conteúdo](#bkmk_top)  
  
## <a name="bkmk_AS"></a>2.0 Analysis Services e PowerPivot  
  
### <a name="21-powerpivot-configuration-tool-does-not-create-the-powerpivot-gallery"></a>2.1 A Ferramenta de Configuração do PowerPivot não cria a Galeria PowerPivot  
**Problema:** a Ferramenta de Configuração do PowerPivot provisiona um Site de Equipe e, portanto, a Galeria PowerPivot não é criada.  
  
**Solução alternativa:** crie um novo aplicativo (biblioteca).  
  
1.  Verifique se o recurso de coleção de sites **Integração de recursos do PowerPivot para coleções de sites** está ativo.  
  
2.  Na página **Conteúdo do site** de um site existente, clique em **adicionar aplicativo**.  
  
3.  Clique em **Galeria PowerPivot**.  
  
### <a name="22-to-use-powerpivot-for-excel-with-excel-2013-you-must-use-the-add-in-that-is-installed-with-excel"></a>2.2 Para usar o PowerPivot para Excel com o Excel 2013, você deverá usar o suplemento que está instalado com o Excel  
**Problema:** com o Office 2010, o PowerPivot para Excel é um suplemento independente baixado em [http://www.microsoft.com/bi/powerpivot.aspx](http://www.microsoft.com/bi/powerpivot.aspx). Ele também pode ser baixado no [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=29074). Observe que há duas versões do suplemento PowerPivot disponíveis como download: uma é fornecida com o SQL Server 2008 R2 e outra, com o SQL Server 2012. No entanto, para o Office 2013, o PowerPivot para Excel é fornecido com o Office e é instalado quando você instala o Excel. Embora as versões do SQL Server 2008 R2 e SQL Server 2012 do PowerPivot para Excel 2010 não sejam compatíveis com o Excel 2013, você ainda pode instalar o PowerPivot para Excel 2010 no computador cliente se quiser executar o Excel 2010 lado a lado com o Excel 2013. Em outras palavras, as duas versões do Excel podem coexistir, além dos suplementos correspondentes do PowerPivot.  
  
**Solução alternativa:** para usar o PowerPivot para Excel 2013, você deverá habilitar o suplemento do COM. No Excel 2013, selecione **Arquivo** | **Opções** | **Suplementos**. Na caixa suspensa **Gerenciar** , selecione **Suplementos do COM** e clique em **Ir**. Em **Suplementos do COM**, selecione **Microsoft Office PowerPivot para Excel 2013** e clique em **OK**.  
  
![Ícone de seta usado com o link Voltar ao Início](../sql-server/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início")[Conteúdo](#bkmk_top)  
  
## <a name="bkmk_RS"></a>3.0 Reporting Services  
  
### <a name="31-install-and-configure-sharepoint-server-2013-prior-to-installing-reporting-services"></a>3.1 Instalar e configurar o SharePoint Server 2013 antes de instalar o Reporting Services  
**Problema:** complete os seguintes requisitos **antes** de instalar o SQL Server Reporting Services (SSRS).  
  
1.  Execute a ferramenta de preparação dos produtos do SharePoint 2013.  
  
2.  Instale o SharePoint Server 2013.  
  
3.  Execute o Assistente de configuração de produto do SharePoint 2013 ou complete um conjunto equivalente de etapas de configuração para configurar o farm do SharePoint.  
  
**Solução alternativa:**  se você instalou o modo do SharePoint do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] antes de o farm do SharePoint ter sido configurado, a solução alternativa necessária dependerá de quais outros componentes estão instalados.  
  
### <a name="32-power-view-in-sharepoint-server-2013-requires-microsoftanalysisservicesspclientdll"></a>3.2 O Power View no SharePoint Server 2013 exige o Microsoft.AnalysisServices.SPClient.dll  
**Problema:**[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não instala um componente obrigatório, **Microsoft.AnalysisServices.SPClient.dll**. Se você instalar a Visualização do SharePoint Server 2013 e o [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo do SharePoint, mas não baixar e instalar o pacote do instalador do PowerPivot para SharePoint 2013, **spPowerPivot.msi** , o Power View não funcionará e exibirá os seguintes sintomas.  
  
**Sintomas:** quando você tenta criar um relatório do Power View, vê uma mensagem de erro semelhante à seguinte:  
  
-   "...Não é possível criar uma conexão com a fonte de dados...''  
  
Os detalhes de erro internos conterão uma mensagem semelhante à seguinte:  
  
-   "O valor 'SharePoint Principal' não tem suporte para a propriedade de cadeia de conexão 'Identidade do usuário'."  
  
**Solução alternativa:** instalar o pacote do instalador do PowerPivot para SharePoint 2013 (**spPowerPivot.msi**) no SharePoint Server 2013. O pacote do instalador está disponível como parte do feature pack do [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] . O feature pack pode ser baixado do centro de download [!INCLUDE[msCoName](../includes/msconame-md.md)] em [SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)  
  
### <a name="33-power-view-sheets-in-a-powerpivot-workbook-are-deleted-after-a-scheduled-data-refresh"></a>3.3 Planilhas do Power View em uma pasta de trabalho PowerPivot são excluídas depois de uma atualização de dados agendada  
**Problema**: no suplemento PowerPivot para SharePoint, o uso da **Atualização de Dados Agendada** em uma pasta de trabalho com o Power View irá excluir as planilhas do Power View.  
  
**Solução alternativa**: para usar a **Scheduled Data Refresh** com as pastas de trabalho do Power View, crie uma pasta de trabalho PowerPivot que seja apenas o modelo de dados. Crie uma pasta de trabalho separada com planilhas do Excel e do Power View que se vinculem à pasta de trabalho PowerPivot com o modelo de dados. Apenas a pasta de trabalho PowerPivot com o modelo de dados deve ser agendada para atualização.  
  
## <a name="bkmk_DQS"></a>4.0 Data Quality Services  
  
### <a name="41-dqs-available-in-the-incorrect-edition-of-sql-server-2012"></a>4.1 DQS disponível na edição incorreta do SQL Server 2012  
**Problema:** na versão RTM do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] , o recurso DQS (Data Quality Services) está disponível nas edições do SQL Server além das edições Enterprise, Business Intelligence e Developer. Depois de instalar o SQL Server 2012 SP1, o DQS não estará disponível em todas as edições exceto as edições Enterprise, Business Intelligence e Developer.  
  
**Solução alternativa**: se você estiver usando o DQS em uma edição sem suporte, atualize para uma edição com suporte ou remova a dependência desse recurso de seus aplicativos.  
  
![Ícone de seta usado com o link Voltar ao Início](../sql-server/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início")[Conteúdo](#bkmk_top)  
  
## <a name="bkmk_Express"></a>5.0 SQL Server Express  
  
### <a name="51-full-version-of-sql-server-management-studio-available-in-sql-server-2012-express-sp1"></a>5.1 Versão completa do SQL Server Management Studio disponível no SQL Server 2012 Express SP1  
A versão do SQL Server 2012 Express Service Pack 1 (SP1) inclui a versão completa do SQL Server 2012 Management Studio (que anteriormente estava disponível no DVD do SQL Server 2012) em vez do SQL Server 2012 Management Studio Express. Para baixar e instalar o SQL Server 2012 Express SP1, consulte [SQL Server 2012 Express Service Pack 1](http://go.microsoft.com/fwlink/p/?linkid=267905).  
  
![Ícone de seta usado com o link Voltar ao Início](../sql-server/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início")[Conteúdo](#bkmk_top)  
  
## <a name="bkmk_CDC"></a>6.0 Serviço Change Data Capture e Designer para Oracle da Attunity  
  
### <a name="61-upgrading-the-cdc-service-and-designer"></a>6.1 Atualizar o serviço CDC e Designer  
**Problema:** se o Change Data Capture Designer para Oracle e o Serviço Change Data Capture para Oracle da Attunity estiverem instalados no computador no momento em que você instalar o SQL Server 2012 SP1, esses componentes não serão atualizados instalando o SP1.  
  
**Solução alternativa:** atualizar os componentes CDC para a versão mais recente:  
  
1.  Baixar os arquivos .msi para o Serviço Change Data Capture para Oracle da Attunity na [página de download dos feature packs do SQL Server 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkID=268266).  
  
2.  Execute o arquivo .msi.  
  
![Ícone de seta usado com o link Voltar ao Início](../sql-server/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início")[Conteúdo](#bkmk_top)  
  
## <a name="DACFx"></a>7.0 Estrutura de Aplicativo da Camada de Dados do SQL Server (DACFx)  
**Suporte à atualização in-loco**  
  
Esta versão da Estrutura de Aplicativo da Camada de Dados (DACFx) fornece suporte à atualização in-loco de versões anteriores. Portanto, não é necessário remover as instalações anteriores da DACFx antes de atualizar para esta versão. Você poderá encontrar futuras versões da DACFx [aqui](https://msdn.microsoft.com/library/dn702988.aspx).  
  
**Suporte a índice XML seletivo**  
  
O SQL Server 2012 SP1 inclui suporte a [Índice XML seletivo (SXI)](http://msdn.microsoft.com/en-us/598ecdcd-084b-4032-81b2-eed6ae9f5d44), um novo recurso do SQL Server que fornece uma nova forma de indexar os dados da coluna XML com desempenho e eficiência crescentes.  
  
Agora a DACFx fornece suporte a índices SXI em todos os cenários DAC e a todas as ferramentas de cliente. O SXI é compatível apenas com a versão mais recente das SSDT. As SSDT RTM e as versões de setembro de 2012 não são compatíveis com o SXI.  
  
**Suporte para formato de dados BCP nativo**  
  
Anteriormente, o formato de dados usado para armazenar os dados da tabela dentro dos pacotes DACPAC e BACPAC era JSON. Com esta atualização, o BCP nativo agora é o formato de persistência de dados. Essa alteração apresenta a fidelidade aprimorada do tipo de dados do SQL Server à DACFx, incluindo suporte para tipos SQL_Variant, assim como desempenho aprimorado de implantação de dados para bancos de dados em grande escala.  
  
**A preservação do estado Restrição CHECK na criação/implantação do pacote**  
  
Anteriormente, a DACFx não preservava o estado (WITH CHECK/NOCHECK) das Restrições CHECK definidas nas tabelas no esquema de banco de dados nem armazenava essas informações dentro de DACPACs. Esse comportamento poderia levar a problemas potenciais na implantação do pacote quando há dados de tabela existente que violam as Restrições CHECK. Com esta atualização, a DACFx agora armazena o estado atual das Restrições CHECK dentro de DACPAC quando extraídas de um banco de dados e restaura apropriadamente esse estado na implantação do pacote.  
  
**Atualizações da SqlPackage.exe (ferramenta de linha de comando da DACFx)**  
  
-   Extrair DACPAC com dados – Cria um arquivo de instantâneo de banco de dados (.dacpac) de um banco de dados dinâmico SQL Server ou SQL do Windows Azure que contém dados de tabelas de usuário além do esquema de banco de dados. Esses pacotes podem ser publicados em um banco de dados SQL Server ou SQL do Windows Azure existente ou novo, usando a ação Publicar da SqlPackage.exe. Os dados contidos no pacote substituem os dados existentes no banco de dados de destino.  
  
-   Exportar BACPAC – Cria um arquivo de backup lógico (.bacpac) de um banco de dados dinâmico SQL Server ou SQL do Windows Azure que contém o esquema de banco de dados e dados de usuário que podem ser usados para migrar um banco de dados SQL Server ou SQL do Windows Azure no local. Os bancos de dados compatíveis com o Azure podem ser exportados e importados posteriormente entre versões com suporte do SQL Server.  
  
-   Importar BACPAC – Importa um arquivo .bacpac para popular um banco de dados vazio ou criar um novo banco de dados SQL Server ou SQL do Windows Azure.  
  
A documentação completa da SqlPackage.exe no MSDN pode ser encontrada [aqui](http://msdn.microsoft.com/library/hh550080%28v=vs.103%29.aspx).  
  
**Compatibilidade de pacote**  
  
Esta versão apresenta vários cenários de compatibilidade futura para os pacotes de DAC.  
  
-   Os pacotes de DAC criados por esta versão que não contêm dados de tabelas ou elementos SXI talvez possam ser utilizados por versões anteriores da DACFx (SQL Server 2012 RTM, SQL Server 2012 CU1 e DACFx de setembro de 2012).  
  
-   Todos os pacotes de DAC criados por versões anteriores da DACFx podem ser utilizados por esta versão.  
  
## <a name="bkmk_known_issues_fixed"></a>8.0 Problemas conhecidos corrigidos neste Service Pack  
Para obter uma lista completa de bugs e problemas conhecidos corrigidos neste service pack, consulte [este artigo mestre da Base de Dados de Conhecimento](http://support.microsoft.com/kb/2674319).  
  
[Conteúdo](#bkmk_top)  
  
## <a name="see-also"></a>Consulte também  
[Como determinar a versão e a edição do SQL Server](http://support.microsoft.com/kb/321185)  
[Recursos com suporte nas edições do SQL Server 2014](http://msdn.microsoft.com/en-us/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)  
  
