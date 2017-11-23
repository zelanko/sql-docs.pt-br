---
title: Atualizar pacotes do Integration Services | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Integration Services, migrating
- migrating packages [Integration Services]
ms.assetid: 68dbdf81-032c-4a73-99f6-41420e053980
caps.latest.revision: 54
author: MikeRayMSFT
ms.author: mikeray
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: a2e3655bedbb24f2174a62c8792cd168e7642592
ms.openlocfilehash: b04ba24fd90ec81e735933a45fed18294d77ceab
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="upgrade-integration-services-packages"></a>Atualizar pacotes do Integration Services
  Quando você atualiza uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os pacotes existentes do [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] não são atualizados automaticamente para o formato de pacote usado pela versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Você terá que selecionar um método de atualização e atualizar os pacotes manualmente.  
  
 Para obter informações sobre como atualizar pacotes quando você converte um projeto para o modelo de implantação de projeto, consulte [implantar Integration Services (SSIS) projetos e pacotes](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)
  
## <a name="selecting-an-upgrade-method"></a>Selecionando um método de atualização  
 Você pode usar vários métodos para atualizar pacotes do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] . Em alguns desses métodos, a atualização é apenas temporária. Em outros, a atualização é permanente. A tabela a seguir descreve cada um desses métodos e se a atualização é temporária ou permanente.  
  
> [!NOTE]  
>  Quando você executa um pacote do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] usando o utilitário **dtexec** (dtexec.exe) que é instalado com a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a atualização do pacote temporário aumenta o tempo de execução. A taxa de aumento em tempo de execução de pacote varia de acordo com o tamanho do pacote. Para evitar um aumento no tempo de execução, é recomendável que você atualize o pacote antes de executá-lo.  
  
|Método de atualização|Tipo de atualização|  
|--------------------|---------------------|  
|Use o utilitário **dtexec** (dtexec.exe) instalado com a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar um pacote do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .<br /><br /> Para saber mais, veja [dtexec Utility](../../integration-services/packages/dtexec-utility.md).|A atualização do pacote é temporária.<br /><br /> Não é possível salvar as alterações.|  
|Abra um arquivo do pacote do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|A atualização do pacote será permanente se você salvá-lo; se você não salvar o pacote, a atualização será temporária.|  
|Adicione um pacote do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a um projeto existente no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|A atualização do pacote é permanente.|  
|Abra um arquivo de projeto do [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] ou posterior no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]e use o Assistente de atualização de pacote do [!INCLUDE[ssIS](../../includes/ssis-md.md)] para atualizar vários pacotes do projeto.<br /><br /> Para obter mais informações, veja [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](../../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md) e [Ajuda F1 do Assistente de Atualização de Pacotes SSIS](../../integration-services/ssis-package-upgrade-wizard-f1-help.md).|A atualização do pacote é permanente.|  
|Use o utilitário <xref:Microsoft.SqlServer.Dts.Runtime.Application.Upgrade%2A> para atualizar um ou mais pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|A atualização do pacote é permanente.|  
  
## <a name="custom-applications-and-custom-components"></a>Aplicativos e componentes personalizados  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] não funcionarão com a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Você pode usar a versão atual de ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para executar e gerenciar pacotes que incluem componentes personalizados do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssIS](../../includes/ssis-md.md)] . Adicionamos quatro regras de redirecionamento de associação aos seguintes arquivos para facilitar o redirecionamento dos assemblies de tempo de execução da versão 10.0.0.0 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]), da versão 11.0.0.0 ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) ou da versão 12.0.0.0 ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) para a versão 13.0.0.0 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
-   DTExec.exe.config  
  
-   dtshost.exe.config  
  
-   DTSWizard.exe.config  
  
-   DTUtil.exe.config  
  
-   DTExecUI.exe.config  
  
 Para usar [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para criar pacotes que incluem [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] componentes personalizados, você precisa modificar o arquivo devenv.exe config está localizado em  *\<drive >*: \Program Files\Microsoft Visual Studio 10.0\Common7\IDE.  
  
 Para usar esses pacotes com aplicativos de clientes compilados com o tempo de execução de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], inclua as regras de redirecionamento da seção de configuração do arquivo *.exe.config do executável. As regras redirecionam os assemblies de tempo de execução para a versão 13.0.0.0 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). Para obter mais informações sobre o redirecionamento de versão do assembly, consulte [ \<assemblyBinding > elemento para \<tempo de execução >](http://msdn.microsoft.com/library/twy1dw1e.aspx).  
  
### <a name="locating-the-assemblies"></a>Localizando os assemblies  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], os assemblies do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] foram atualizados para o .NET 4.0. Há um cache de assembly global separado para o .NET 4, localizado em  *\<drive >*: \windows\microsoft.net\assembly.. Você pode localizar todos os assemblies do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nesse caminho, normalmente na pasta GAC_MSIL.  
  
 Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o núcleo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] arquivos. dll de extensibilidade também estão localizados em  *\<drive >*: \Program Files\Microsoft Server\130\SDK\Assemblies SQL.  
  
## <a name="understanding-sql-server-package-upgrade-results"></a>Entendendo os resultados da atualização de pacote do SQL Server  
 No processo de atualização de pacotes, a maioria dos componentes e recursos dos pacotes do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] são convertidos diretamente em seus respectivos equivalentes na versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No entanto, há vários componentes e recursos que não serão atualizados ou têm resultados de atualização dos quais você deve estar ciente. A tabela a seguir identifica esses componentes e recursos.  
  
> [!NOTE]  
>  Para identificar os pacotes que apresentam os problemas listados nesta tabela, execute o Supervisor de Atualização.  
  
|Componente ou recurso|Resultados da atualização|  
|--------------------------|---------------------|  
|Cadeias de conexão|Para pacotes do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , os nomes de determinados provedores foram alterados e requerem valores diferentes nas cadeias de conexão. Para atualizar as cadeias de conexão, use um dos seguintes procedimentos:<br /><br /> Use o Assistente de Atualização de Pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] para atualizar o pacote e selecione a opção **Atualizar cadeias de caracteres de conexão para usar novos nomes de provedor** .<br /><br /> No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], na página Geral da caixa de diálogo Opções, selecione a opção **Atualizar cadeias de caracteres de conexão para usar novos nomes de provedor** . Para obter mais informações sobre essa opção, consulte a página geral.<br /><br /> No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote e altere o texto da propriedade ConnectionString manualmente.<br /><br /> Observação: você não pode usar os procedimentos anteriores para atualizar uma cadeia de conexão quando ela está armazenada em um arquivo de configuração ou em um arquivo de fonte de dados, ou quando uma expressão define a propriedade **ConnectionString** . Para atualizar a cadeia de conexão nesses casos, é necessário atualizar manualmente o arquivo ou a expressão.<br /><br /> Para obter mais informações sobre as fontes de dados disponíveis, veja [Fontes de Dados](../../integration-services/connection-manager/data-sources.md).|  
  
### <a name="scripts-that-depend-on-adodbdll"></a>Scripts que dependem do ADODB.dll  
 Os scripts Tarefa Script e Componente de Script que fazem referência explicitamente ao ADODB.dll podem não ser atualizados ou executados em computadores sem o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] instalado. Para atualizar esses scripts Tarefa Script ou Componente Script, é recomendável remover a dependência do ADODB.dll.  O Ado.Net é a alternativa indicada para código gerenciado, como scripts VB e C#.  
  
  

