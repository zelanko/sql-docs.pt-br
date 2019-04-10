---
title: Requisitos de hardware e Software para servidor do Analysis Services no modo do SharePoint (SQL Server 2014) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: fb86ca0a-518c-4c61-ae78-7680c57fae1f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 72888a9896502c09480ae682981e4031ea01751c
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241584"
---
# <a name="hardware-and-software-requirements-for-analysis-services-server-in-sharepoint-mode-sql-server-2014"></a>Requisitos de hardware e software para servidor do Analysis Services no modo do SharePoint (SQL Server 2014)
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] dá suporte ao SharePoint 2010 e SharePoint 2013. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 é executado fora do farm do SharePoint, embora ele pode ser instalado nos servidores do SharePoint. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 é executado em servidores de aplicativos em um farm do SharePoint 2010 e usa recursos do SharePoint e a infraestrutura para dar suporte a operações de servidor. Para instalar o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] para uma versão do SharePoint, use o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Após a instalação, siga estas etapas:  
  
-   Execute a versão apropriada da ferramenta de configuração do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] para a versão do SharePoint.  
  
-   Para SharePoint 2013, instale o [instalar ou desinstalar o PowerPivot para SharePoint Add-in &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  

  
##  <a name="bkmk_sqleditions"></a> Requisitos de edição do SQL Server  
 Os recursos de business intelligence não estão disponíveis em todas as edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter detalhes, consulte [recursos compatíveis com as edições do SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md) e [edições e componentes do SQL Server 2014](../editions-and-components-of-sql-server-2016.md).  
  
 Notas de versão atuais podem ser encontradas em [notas de versão do Microsoft SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
  

  
##  <a name="bkmk_sqllicense"></a> Licenciamento do SQL Server  
 Para obter mais informações sobre o licenciamento do SQL Server, consulte:  
  
-   [Folha de dados do SQL Server 2014 licenciamento](https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf) (https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf).  
  
-   [Como comprar: Suporte a modelos de licenciamento do SQL Server](https://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2) (https://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2).  
  

  
##  <a name="bkmk_ssas__sharepoint_2013"></a> Analysis Services instalado no SharePoint 2013  
 Se você instalar o servidor do Analysis Services no modo do SharePoint em um servidor sozinho, os requisitos mínimos do sistema serão baseados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em vez de nos requisitos do SharePoint Server.  
  
 [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint é melhor executado em servidores comerciais de nova geração que oferecem limites de RAM mais altos e mais capacidade de processamento. Grandes quantidades de RAM são usadas para armazenar dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] na memória. A RAM dá suporte à capacidade de adaptação a alterações estruturais. Processadores adicionais dão suporte a exames de dados brutos não agregados de longa execução. Os dados supõem sua estrutura em um ambiente dinâmico, em resposta à análise de dados controlada pelo usuário iniciada diretamente de um cliente Excel ou interface front-end.  
  
> [!TIP]  
>  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint utiliza caches L2 e L3. Para melhorar o desempenho, é recomendável o uso de processadores com caches L2 e L3 maiores.  
  
 A seguinte tabela descreve as configurações de hardware mínima e recomendada para um servidor autônomo do [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] que não faça parte do farm do SharePoint:  
  
|Componente|Mínimo|Recomendado|  
|---------------|-------------|-----------------|  
|Processador|Processador de núcleo duplo de 64 bits, 3 gigahertz.|16 núcleos|  
|RAM|8 gigabytes de RAM|64 gigabytes de RAM|  
|Armazenamento|80 gigabytes de armazenamento|80 gigabytes ou mais|  
  
 Se você instalar o servidor do Analysis Services no modo do SharePoint em um servidor do farm do SharePoint, analise os requisitos mínimos do sistema para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e o SharePoint Server nos seguintes links:  
  
-   [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [Requisitos de hardware e software para SharePoint 2013](https://technet.microsoft.com/library/cc262485\(office.15\).aspx).  
  
 As recomendações padrão de hardware e software do SharePoint 2013 são para uma solução de gerenciamento de documentos baseada na Web para um grupo de trabalho ou equipe. Como o processamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] faz uso intenso de dados, a recomendação padrão é suficiente se a carga de trabalho geral é pequena; por exemplo, menos de 100 usuários ou pastas de trabalho. Uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] maior exige capacidade adicional de computação.  
  

  
##  <a name="bkmk_ssas__sharepoint_2010"></a> Analysis Services instalado em um servidor do SharePoint 2010  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 é executado em servidores de aplicativos em um farm do SharePoint 2010 e usa recursos do SharePoint e a infraestrutura para dar suporte a operações de servidor. A seguinte tabela resume os requisitos relacionados às implantações do SharePoint 2010:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Versão do SharePoint|SharePoint 2010 Enterprise, com Serviços do Excel, Serviço de Repositório Seguro e o Claims to Windows Token Service configurados no mesmo farm de servidores.<br /><br /> O SharePoint deve ser instalado utilizando a opção Farm de Servidores na Instalação do SharePoint (a opção de instalação Autônoma do SharePoint não é permitida). [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] requer acesso a dados e infraestrutura de farm de servidor para dar suporte administrativo. A instalação autônoma não fornece estes serviços.<br /><br /> A edição de desenvolvedor, executada no Windows 7 ou no Windows Vista, não tem suporte em instalações de servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|  
|Service Packs|O SharePoint Server 2010 Service Pack 1 (SP1) é necessário.<br /><br /> O SharePoint 2010 Service Pack 1 é necessário para os recursos do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].<br /><br /> A atualização cumulativa de agosto de 2010 do SharePoint 2010, ou posterior, é necessária para atualizar uma versão anterior do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. A atualização cumulativa do agosto de 2010, ou posterior, deve ser instalada depois de instalar o SharePoint Service Pack 1. Uma nova instalação do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] não requer a atualização cumulativa. Para obter mais informações, consulte [agosto de 2010 atualização cumulativa para o SharePoint foi lançada](http://blogs.technet.com/b/stefan_gossner/archive/2010/09/02/august-2010-cumulative-update-for-sharepoint-has-been-released.aspx).|  
|Aplicativo Web do SharePoint|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] somente para o SharePoint 2010 dá suporte a aplicativos web do SharePoint que estão configurados para autenticação de modo clássico. Se estiver adicionando o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint a um farm existente, verifique se o aplicativo Web que você pretende usar com ele está configurado para a autenticação de modo clássico. Para obter instruções sobre como verificar o modo de autenticação, consulte a seção "verificar se o aplicativo Web usa a autenticação de modo clássico" em [implantar soluções do PowerPivot para SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md).|  
|Os provedores de dados necessários à atualização de dados do servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|A atualização de dados do servidor repete as mesmas etapas de recuperação de dados usadas para importar os dados originalmente. Isso significa que os provedores de dados usados para importar os dados em uma estação de trabalho cliente também devem estar presentes no servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.<br /><br /> Além disso, o uso de feeds de dados em um servidor SharePoint requer que você tenha o ADO.NET Data Services. O programa do Instalador de Pré-requisitos do SharePoint não instala esse software para você. O software a seguir deve ser instalado manualmente.<br /><br /> Os assemblies de tempo de execução do ADO.NET Data Services 3.5 SP1, usados para exportar uma lista do SharePoint como um feed de dados. Baixe e instale a versão que corresponde a seu sistema operacional:<br /><br /> Para o Windows Server 2008 R2, use [ADO.NET Data Services Update para .NET Framework 3.5 SP1 para Windows 7 e windows Server 2008 R2 (https://go.microsoft.com/fwlink/?LinkId=182557)](https://go.microsoft.com/fwlink/?LinkId=182557). Windows Server 2008 R2 **SP1** já contém o provedor atualizado.<br /><br /> Para o Windows Server 2008, use [atualização do ADO.NET Data Services para .NET Framework 3.5 SP1 para Windows 2000, Windows Server 2003, Windows XP, Windows Vista e Windows Server 2008 (https://go.microsoft.com/fwlink/?LinkId=158125)](https://go.microsoft.com/fwlink/?LinkId=158125).|  
  
 [Determinar o Hardware e Software (de requisitos (SharePoint 2010)https://go.microsoft.com/fwlink/?LinkId=169734)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
 
  
## <a name="additional-information"></a>Informações adicionais  
 Para obter informações sobre as alterações do SharePoint, consulte [alterações do SharePoint 2010 para SharePoint 2013](https://technet.microsoft.com/library/ff607742\(office.15\).aspx) (https://technet.microsoft.com/library/ff607742(office.15).aspx).  
  

  
  
