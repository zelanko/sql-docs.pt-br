---
title: Fazer upgrade de pacotes do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, migrating
- migrating packages [Integration Services]
ms.assetid: 68dbdf81-032c-4a73-99f6-41420e053980
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 002ef268bbb858db961862c1a30479a3e8462237
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136056"
---
# <a name="upgrade-integration-services-packages"></a>Atualizar pacotes do Integration Services
  Quando você atualiza uma instância de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as existentes [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] pacotes não são atualizados automaticamente para o formato de pacote usado pela versão atual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa. Você terá que selecionar um método de atualização e atualizar os pacotes manualmente.  
  
 Quando você atualiza um pacote do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] migra os scripts existentes em qualquer tarefa Script e componente Script para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA). No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os scripts em tarefas Script ou em componentes Script usavam o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] for Applications (VSA). Para obter mais informações sobre as alterações que você possa ter de fazer nos scripts antes da migração e sobre falhas na conversão de scripts, consulte [Migrar scripts para o VSTA](../../sql-server/install/migrate-scripts-to-vsta.md).  
  
 Para obter informações sobre como atualizar pacotes quando você converte um projeto para o modelo de implantação de projetos, consulte [Deploy Projects to Integration Services Server](../deploy-projects-to-integration-services-server.md).  
  
## <a name="sql-server-2000-data-transformation-services-packages"></a>Pacotes do SQL Server 2000 Data Transformation Services  
 O suporte para a migração ou a execução de pacotes de DTS (Data Transformation Services) foram descontinuados na versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A seguinte funcionalidade do DTS foi descontinuada:  
  
-   Tempo de execução DTS  
  
-   API DTS  
  
-   O Assistente de Migração de Pacotes para migração de pacotes DTS para a próxima versão do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Suporte para manutenção de pacote DTS no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Tarefa Executar Pacote DTS 2000  
  
-   Exame de pacotes DTS do Supervisor de Atualização  
  
 As seguintes opções estão disponíveis para migrar pacotes do DTS.  
  
-   Migre os pacotes para o [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] ou [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]e, em seguida, atualize os pacotes para o [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)].  
  
     Para obter informações sobre migração de pacotes DTS para o [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] e o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)], consulte [Migrando pacotes DTS (Data Transformation Services)](http://go.microsoft.com/fwlink/?LinkId=251870) (2005) e [Migrando pacotes DTS (Data Transformation Services)](http://go.microsoft.com/fwlink/?LinkId=251871) (2008).  
  
-   Recrie os pacotes do DTS usando o [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)].  
  
     Para obter informações sobre os novos recursos do [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)], consulte [Novidades &#40;Integration Services&#41;](../what-s-new-in-integration-services-in-sql-server-2016.md). Para obter uma visão geral da estrutura dos pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Pacotes do Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md).  
  
## <a name="selecting-an-upgrade-method"></a>Selecionando um método de atualização  
 Você pode usar vários métodos para atualizar pacotes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] . Em alguns desses métodos, a atualização é apenas temporária. Em outros, a atualização é permanente. A tabela a seguir descreve cada um desses métodos e se a atualização é temporária ou permanente.  
  
> [!NOTE]  
>  Quando você executa um pacote do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] usando o utilitário **dtexec** (dtexec.exe) instalado com a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a atualização do pacote temporário aumenta o tempo de execução. A taxa de aumento em tempo de execução de pacote varia de acordo com o tamanho do pacote. Para evitar um aumento no tempo de execução, é recomendável que você atualize o pacote antes de executá-lo.  
  
|Método de atualização|Tipo de atualização|  
|--------------------|---------------------|  
|Use o utilitário **dtexec** (dtexec.exe) instalado com a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar um pacote do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> Para saber mais, veja [dtexec Utility](../packages/dtexec-utility.md).|A atualização do pacote é temporária. Para um pacote do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , a migração do script é temporária.<br /><br /> Não é possível salvar as alterações.|  
|Abra um arquivo de pacote do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|A atualização do pacote será permanente se você salvá-lo; se você não salvar o pacote, a atualização será temporária.<br /><br /> Para um pacote do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , a migração de script será permanente se você salvar o pacote; caso contrário, a atualização será temporária.|  
|Adicione um pacote do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a um projeto existente do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|A atualização do pacote é permanente. Para um pacote do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , a migração do script é permanente.|  
|Abra um arquivo de projeto do [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] ou [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]e use o Assistente de atualização de pacote do [!INCLUDE[ssIS](../../includes/ssis-md.md)] para atualizar vários pacotes do projeto.<br /><br /> Para obter mais informações, veja [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md) e [Ajuda F1 do Assistente de Atualização de Pacotes SSIS](../ssis-package-upgrade-wizard-f1-help.md).|A atualização do pacote é permanente. Para um pacote do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , a migração do script é permanente.|  
|Use o utilitário <xref:Microsoft.SqlServer.Dts.Runtime.Application.Upgrade%2A> para atualizar um ou mais pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|A atualização do pacote é permanente. Para um pacote do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , a migração do script é permanente.|  
  
## <a name="custom-applications-and-custom-components"></a>Aplicativos e componentes personalizados  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] não funcionarão com a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Você pode usar a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ferramentas para executar e gerenciar pacotes que incluem [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] componentes personalizados. Adicionamos quatro regras de redirecionamento de associação aos seguintes arquivos para facilitar o redirecionamento dos assemblies de tempo de execução da versão 10.0.0.0 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]) para a versão 11.0.0.0 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
-   DTExec.exe.config  
  
-   dtshost.exe.config  
  
-   DTSWizard.exe.config  
  
-   DTUtil.exe.config  
  
-   DTExecUI.exe.config  
  
 Para usar [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para criar pacotes que incluam [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] componentes personalizados, você precisa modificar o arquivo devenv que está localizado em  *\<unidade >*: \Program Files\ Microsoft Visual Studio 10.0\Common7\IDE.  
  
 Para usar esses pacotes com aplicativos de clientes compilados com o tempo de execução de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], inclua as regras de redirecionamento da seção de configuração do arquivo *.exe.config do executável. As regras redirecionam os assemblies de tempo de execução para a versão 11.0.0.0 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). Para obter mais informações sobre o redirecionamento de versão do assembly, veja [Elemento \<assemblyBinding> para \<runtime>](http://msdn.microsoft.com/library/twy1dw1e.aspx).  
  
### <a name="locating-the-assemblies"></a>Localizando os assemblies  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], os assemblies do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] foram atualizados para o .NET 4.0. Há um cache de assembly global separado para o .NET 4, localizado em  *\<drive >*: \windows\microsoft.net\assembly. Você pode localizar todos os assemblies do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nesse caminho, normalmente na pasta GAC_MSIL.  
  
 Assim como nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os principais arquivos .dll de extensibilidade do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também estão localizados em *\<unidade>*:\Arquivos de Programas\Microsoft SQL Server\100\SDK\Assemblies.  
  
## <a name="understanding-sql-server-package-upgrade-results"></a>Entendendo os resultados da atualização de pacote do SQL Server  
 No processo de atualização de pacotes, a maioria dos componentes e recursos dos pacotes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] são convertidos diretamente em seus respectivos equivalentes na versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No entanto, há vários componentes e recursos que não serão atualizados ou têm resultados de atualização dos quais você deve estar ciente. A tabela a seguir identifica esses componentes e recursos.  
  
> [!NOTE]  
>  Para identificar os pacotes que apresentam os problemas listados nesta tabela, execute o Supervisor de Atualização. Para obter mais informações, consulte [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
|Componente ou recurso|Resultados da atualização|  
|--------------------------|---------------------|  
|Cadeias de conexão|Para pacotes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , os nomes de determinados provedores foram alterados e requerem valores diferentes nas cadeias de conexão. Para atualizar as cadeias de conexão, use um dos seguintes procedimentos:<br /><br /> -Use o Assistente de Atualização de Pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] para atualizar o pacote e selecione a opção **Atualizar cadeias de caracteres de conexão para usar novos nomes de provedor**.<br /><br /> -No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], na página Geral da caixa de diálogo Opções, selecione a opção **Atualizar cadeias de caracteres de conexão para usar novos nomes de provedor** . Para obter mais informações sobre essa opção, consulte [General Page](../general-page-of-integration-services-designers-options.md).<br /><br /> -No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote e altere o texto da propriedade ConnectionString manualmente.<br /><br /> Observação: Você não pode usar os procedimentos anteriores para atualizar uma cadeia de conexão quando a cadeia de conexão é armazenada em um arquivo de configuração ou um arquivo de fonte de dados, ou quando uma expressão define o `ConnectionString` propriedade. Para atualizar a cadeia de conexão nesses casos, é necessário atualizar manualmente o arquivo ou a expressão.<br /><br /> Para obter mais informações sobre as fontes de dados disponíveis, veja [Fontes de Dados](../connection-manager/data-sources.md).|  
|transformação Pesquisa|Para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] pacotes, o processo de atualização atualiza automaticamente a transformação pesquisa para a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Porém, a versão atual deste componente tem alguns recursos adicionais dos quais você pode se beneficiar.<br /><br /> Para obter mais informações, consulte [Lookup Transformation](../data-flow/transformations/lookup-transformation.md).|  
|Tarefa Script e componente Script|Para pacotes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , o processo de atualização de pacotes migra automaticamente os scripts da tarefa Script e do componente Script do VSA para o VSTA.<br /><br /> Para obter mais informações sobre as alterações que você possa ter de fazer nos scripts antes da migração e sobre falhas na conversão de scripts, consulte [Migrar scripts para o VSTA](../../sql-server/install/migrate-scripts-to-vsta.md).|  
  
### <a name="scripts-that-depend-on-adodbdll"></a>Scripts que dependem do ADODB.dll  
 Os scripts Tarefa Script e Componente de Script que fazem referência explicitamente ao ADODB.dll podem não ser atualizados ou executados em computadores sem o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] instalado. Para atualizar esses scripts Tarefa Script ou Componente Script, é recomendável remover a dependência do ADODB.dll.  O Ado.Net é a alternativa indicada para código gerenciado, como scripts VB e C#.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Artigo técnico, [5 dicas para uma atualização suave do SSIS para o SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=235321), no msdn.microsoft.com.  
  
-   Entrada de blog, [Fazendo com que aplicativos e extensões de SSIS personalizados existentes funcionem no Denali](http://go.microsoft.com/fwlink/?LinkId=238157), em blogs.msdn.com.  
  
-   Webcast, [Atualizando pacotes SSIS para o SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=258674), em channel9.msdn.com.  
  
  
