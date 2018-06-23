---
title: Topologias de licença de exemplo e custos para autoatendimento de Business Intelligence do SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 682b8711-407a-48d1-9807-415d4c24dad6
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 5939b834b50161e31cbbbf3290ab2342bcda59fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011057"
---
# <a name="example-license-topologies-and-costs--for-sql-server-2014-self-service-business-intelligence"></a>Topologias de licença de exemplo e custos para o autoatendimento de business intelligence do SQL Server 2014
  Este tópico ilustra considerações de alto nível para selecionar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edição Business Intelligence ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition. O tópico inclui diversas topologias locais de exemplo de Business Intelligence (BI) de autoatendimento da Microsoft. Os exemplos incluem as edições e licenças que você pode utilizar para otimizar o equilíbrio entre custo e desempenho. As topologias, o número de servidores e o custo de licenciamento são fornecidos **somente como exemplos**. O Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e o Microsoft SharePoint 2013 introduziram diversas alterações em licenciamento para oferecerem mais opções para você licenciar seus servidores, usuários e dispositivos. O licenciamento do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dá suporte aos mesmos cenários relacionados de Business Intelligence.  
  
-   O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] está disponível na edição Business Intelligence e oferece licenciamento por núcleo para algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O SharePoint 2013 simplificou o licenciamento do SharePoint Server para cenários de extranet e Internet, além de opções para o SharePoint Online.  
  
 Antes de adquirir, visite a seção "Como comprar" de cada produto e consulte seu representante ou revendedor local da Microsoft em relação a seus requisitos específicos de licenciamento. Para obter informações sobre os planos e custos de licenciamento mais recentes, consulte o seguinte:  
  
-   [Sobre o licenciamento – SQL Server 2014](http://www.microsoft.com/licensing/about-licensing/sql2014.aspx)  
  
-   [Licenciamento do SharePoint 2013](http://office.microsoft.com/sharepoint/sharepoint-licensing-overview-collaboration-software-FX103789438.aspx).  
  
 **Neste tópico:**  
  
-   [Componentes de Business Intelligence do SQL Server](#bkmk_bi_components)  
  
-   [Resumo do licenciamento do SQL Server 2014](#bkmk_sql_server_license)  
  
-   [Resumo do licenciamento do SharePoint 2013](#bkmk_sharepoint_license)  
  
-   [Topologia de camada 3 com servidores PowerPivot separados](#bkmk_3tier_powerpivot)  
  
-   [Topologia de 3 camadas](#bkmk_3tier)  
  
-   [Topologia de camada 2](#bkmk_2tier)  
  
-   [Conteúdo de referência e comunidade](#bkmk_reference)  
  
##  <a name="bkmk_bi_components"></a> Componentes de Business Intelligence do SQL Server  
 Este tópico se concentra nas tecnologias de servidor do SQL Server e do SharePoint. Os custos e os exemplos não ilustram especificamente componentes do Microsoft Windows Server ou do Microsoft Office necessários para uma solução completa de cliente e servidor. Os componentes do SQL Server Business Intelligence abordados neste tópico são o SQL Server Reporting Services executado no modo do SharePoint e o PowerPivot para SharePoint. Os componentes incluem os seguintes recursos:  
  
-   Pastas de trabalho PowerPivot interativas no navegador.  
  
-   Interativo [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] relatórios no SharePoint.  
  
-   Galeria [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], atualização de Dados da agenda, Painel de Gerenciamento.  
  
-   Reporting Services no modo do SharePoint, incluindo Alertas de Dados.  
  
 Para obter mais informações, consulte a tabela de recursos no [instalar recursos de BI do SQL Server com o SharePoint &#40;PowerPivot e Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md).  
  
## <a name="license-summary"></a>Resumo das licenças  
 Esta seção resume os requisitos de licenciamento para o SQL Server e o SharePoint. As informações são um resumo de alto nível e só abordam os cenários usados nos diagramas de topologia e nos exemplos de custo deste documento. Examine os links de conteúdo conforme indicado para obter mais detalhes sobre licenças. Os preços de exemplo baseiam-se nos preços do Microsoft Open License Program (MOLP).  
  
 Uma prática comum é usar o **Enterprise Edition** para servidores que executam o Mecanismo de Banco de Dados do SQL Server e o **Business Intelligence Edition** para servidores que executam o Reporting Services ou o PowerPivot para SharePoint. Entretanto, o **número de usuários** e o **número de núcleos de servidor** em sua implantação afetam o custo e sua decisão sobre qual edição usar.  
  
###  <a name="bkmk_sql_server_license"></a> Resumo do licenciamento do SQL Server 2014  
  
-   O SQL Server Enterprise Edition usa o licenciamento baseado em núcleo. As licenças baseadas em núcleo são vendidas em pacotes de **dois núcleos** .  
  
-   A edição SQL Server BI usa licenças de servidor e CALs (licenças de acesso para cliente).  
  
-   As licenças CAL se baseiam em cada usuário ou dispositivo conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independentemente do número de servidores a que eles estejam conectados.  
  
-   O licenciamento por núcleo exige que todos os núcleos do servidor sejam cobertos por uma licença. Há um mínimo de **quatro** licenças por núcleo necessárias para cada processador físico no servidor.  
  
 A tabela a seguir resume os detalhes da licença usados para design da implantação e estimativa de custo da licença. **OBSERVAÇÃO:**  Os preços mostrados são apenas para demonstração.  
  
|Edições do SQL Server|Licença do SQL Server + CAL|Licença baseada em núcleo do SQL Server|  
|-------------------------|---------------------------------------------------------|-----------------------------------|  
|Enterprise|Não aplicável|**(Sim)** $ 6874 X [nº de núcleos] X [fator de núcleo]|  
|Business Intelligence|**(Sim)** $ 8592 + $ 199 por CAL|Não aplicável|  
|Standard|**(Sim)**|**(Sim)**|  
  
 Para obter mais informações sobre o exemplo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] preços de licença, consulte:  
  
-   [Licenciamento para ambientes virtuais](http://www.microsoft.com/licensing/about-licensing/virtualization.aspx) (http://www.microsoft.com/licensing/about-licensing/virtualization.aspx).  
  
-   [SQL Server 2014 licenciamento folha de dados - Home Page da Microsoft](http://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf) (http://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf).  
  
-   [Licenciamento e edições do SQL server 2014](http://www.microsoft.com/licensing/about-licensing/sql2014.aspx#tab=2)  
  
1.  **Suposições sobre o SQL Server e mais informações de licenciamento:**  
  
2.  Os diagramas deste tópico usam o Enterprise Edition do SQL Server para servidores de banco de dados de forma que o conjunto completo de recursos de alta disponibilidade esteja disponível; por exemplo, os Grupos de Disponibilidade AlwaysOn. Para obter mais informações, consulte [Features Supported by the Editions of SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
3.  Os servidores deste exemplo são 2 processadores Intel Xeon de 6 núcleos, portanto há um **fator de núcleo do SQL Server** de **1** no cálculo de custos de licenciamento. Para obter mais informações sobre fatores de núcleo e custos de licenciamento, consulte [tabela de fator de núcleo do SQL Server](http://download.microsoft.com/download/9/B/F/9BF63163-D8F9-4339-90AA-EBC9AAFC49AD/SQL2012_CoreFactorTable_Mar2012.pdf) (http://download.microsoft.com/download/0/C/8/0C85665B-11EA-4FF5-B37C-8CC21CF95AC4/BizTalk%202013_CoreFactorTable_**3.19.2013**. v4.pdf).  
  
###  <a name="bkmk_sharepoint_license"></a> Resumo do licenciamento do SharePoint 2013  
 A lista a seguir resume os modelos de licença usados para design da implantação e estimativa de custo da licença. Os preços mostrados são apenas para demonstração.  
  
1.  Uma licença de servidor do SharePoint é necessária para cada instância do Microsoft SharePoint Server.  
  
2.  Para licenciar o SharePoint Enterprise, para cada usuário final ou dispositivo final, compre uma **licença CAL Standard** do Microsoft SharePoint Server 2013, além de uma **licença CAL Enterprise**do Microsoft SharePoint Server 2013.  
  
3.  As licenças CAL do SharePoint são compradas uma por usuário ou dispositivo que acesse servidores do SharePoint. Você não precisa comprar licenças CAL para cada servidor.  
  
 Por exemplo, se o seu ambiente consistir em 2 instâncias usadas por 100 usuários e seus custos cotados forem os seguintes:  
  
-   Licença CAL Standard do Microsoft SharePoint Server 2013: **$ 107,99**  
  
-   Licença CAL Enterprise do Microsoft SharePoint Server 2013: **$ 94,99**  
  
-   Licença do Microsoft SharePoint Server 2013: **$ 6.412,99**  
  
 O custo seria de: **$ 33.123,98**  
  
-   Licença CAL: ($ 107,99 + $ 94,99) X 100) =$ 20.298,00  
  
-   Licença de Servidor: ($ 6.412,99 X 2) = $ 12.825,98  
  
 **Pressuposições sobre o SharePoint e mais informações de licenciamento:**  
  
 As implantações de exemplo são todas ambientes de intranet e, portanto, o licenciamento CAL do SharePoint é necessário.  
  
-   [A lista completa do SharePoint de licenciamento do](http://technet.microsoft.com/en-in/library/jj819267.aspx#bkmk_FeaturesOnPremise) (http://technet.microsoft.com/en-in/library/jj819267.aspx#bkmk_FeaturesOnPremise).  
  
-   [Como comprar o SharePoint](http://sharepoint.microsoft.com/en-in/Pages/buy.aspx) (http://sharepoint.microsoft.com/en-in/Pages/buy.aspx).  
  
##  <a name="bkmk_3tier_powerpivot"></a> Topologia com separado de 3 camadas [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] servidores  
 Este exemplo ilustra que, com 800 usuários ou menos, é mais barato usar a edição SQL Server BI para os servidores de aplicativos do SharePoint e servidores [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Entretanto, quando houver 800 usuários ou mais, o SQL Server Enterprise Edition será mais barato. O licenciamento por núcleo independe do número de usuários e, portanto, há um ponto de limite de custo quando você compara custos de licença por núcleo e CAL e o número de usuários aumenta. Do ponto de limite para frente, o Enterprise Edition é a solução mais barata de todas. Para determinar o limite de custo, compare custos com base no número de núcleos a serem licenciados versus o número de CALs de usuário final ou de dispositivo final a serem licenciadas.  
  
-   Este exemplo é uma implantação de intranet; portanto, o licenciamento CAL do SharePoint aplica-se ao SharePoint 2013.  
  
-   A função Aplicativo (2) inclui SQL Server Reporting Services instalados no modo do SharePoint.  
  
     Os bancos de dados de aplicativo de serviço do SharePoint são executados em servidores de função de banco de dados (4).  
  
-   O [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint é executado em servidores separados (3). [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2013 é executado fora do farm do SharePoint e pode ser instalado em servidores que não incluem uma instalação do SharePoint, melhorando o desempenho.  
  
-   A função de Banco de Dados (4) usa o SQL Server Enterprise de forma que o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Grupos de Disponibilidade AlwaysOn, esteja disponível.  
  
 ![bi_license_3tiers_and_ASseparate](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseparate.gif "bi_license_3tiers_and_ASseparate")  
  
 Com 100 usuários, a edição SQL Server BI é a mais barata.  
  
 ![bi_license_3tiers_and_ASseperate_calcs](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseperate-calcs.gif "bi_license_3tiers_and_ASseperate_calcs")  
  
 Entretanto, com 300 usuários, usar o SQL Server Enterprise Edition será mais barato.  
  
 ![bi_license_3tiers_and_ASseperate_calcs2](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseperate-calcs2.gif "bi_license_3tiers_and_ASseperate_calcs2")  
  
##  <a name="bkmk_3tier"></a> Topologia de 3 camadas  
 Este exemplo ilustra que, com 100 ou menos usuários, é mais barato usar a edição SQL Server BI para os servidores que executem a funcionalidade do SQL Server BI. Entretanto, quando houver 500 usuários ou mais, o SQL Server Enterprise Edition será mais barato.  
  
-   Este exemplo é uma implantação de intranet; portanto, o licenciamento CAL do SharePoint aplica-se ao SharePoint 2013.  
  
-   Analysis Services no modo PowerPivot (2) é executado fora do farm, mas PowerPivot estiver **no mesmo físico** servidores na função de aplicativo.  
  
-   A função de banco de dados (3) usa o SQL Server Enterprise para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recurso, grupos de disponibilidade AlwaysOn estão disponíveis.  
  
 ![bi_license_3tiers](../../../2014/sql-server/install/media/bi-license-3tiers.gif "bi_license_3tiers")  
  
 Com 100 usuários, a edição SQL Server BI é a mais barata.  
  
 ![bi_license_3tiers_calcs1](../../../2014/sql-server/install/media/bi-license-3tiers-calcs1.gif "bi_license_3tiers_calcs1")  
  
 Entretanto, com 500 usuários, o SQL Server Enterprise Edition será mais barato.  
  
 ![bi_license_3tiers_calcs3](../../../2014/sql-server/install/media/bi-license-3tiers-calcs3.gif "bi_license_3tiers_calcs3")  
  
##  <a name="bkmk_2tier"></a> Topologia de camada 2  
 Com apenas duas camadas, o SQL Server Enterprise Edition é usado de forma que o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Grupos de Disponibilidade AlwaysOn, esteja disponível para o Mecanismo de Banco de Dados do SQL Server. Portanto, não há diferenças de custo para se fazer uma comparação entre edições do SQL Server. A única variável é o preço da CAL do SharePoint com base no número de usuários.  
  
-   Este exemplo é uma implantação de intranet; portanto, o licenciamento CAL do SharePoint aplica-se ao SharePoint 2013.  
  
-   O Analysis Services no modo PowerPivot é executado fora do farm, mas o PowerPivot está sendo executado nos mesmos servidores físicos (2) do Mecanismo de Banco de Dados do SQL Server.  
  
 ![bi_license_2tiers](../../../2014/sql-server/install/media/bi-license-2tiers.gif "bi_license_2tiers")  
  
 ![bi_license_2tiers_calcs1](../../../2014/sql-server/install/media/bi-license-2tiers-calcs1.gif "bi_license_2tiers_calcs1")  
  
##  <a name="bkmk_reference"></a> Conteúdo de referência e comunidade  
  
### <a name="license-tools"></a>Ferramentas de licenciamento  
  
-   [Supervisor de licenças da Microsoft](http://mla.microsoft.com/default.aspx) (http://mla.microsoft.com/default.aspx).  
  
-   [Licença de acesso para cliente (CAL) decisão ferramenta](http://www.microsoft.com/licensing/CalTool/) (http://www.microsoft.com/licensing/CalTool/).  
  
-   [Microsoft Business Hub: Como comprar](http://www.microsoftbusinesshub.com/How_To_Buy#) (http://www.microsoftbusinesshub.com/How_To_Buy#).  
  
### <a name="microsoft-license-information"></a>Informações sobre licença da Microsoft  
  
-   [Sobre licenciamento: Licenças de acesso para cliente e gerenciamento de licenças](http://www.microsoft.com/licensing/about-licensing/client-access-license.aspx) (http://www.microsoft.com/licensing/about-licensing/client-access-license.aspx).  
  
-   [Sobre licenciamento: Produto pesquisa de licenciamento](http://www.microsoftvolumelicensing.com/default.aspx) (http://www.microsoftvolumelicensing.com/default.aspx).  
  
-   [Licenciamento por volume: preços e como comprar](http://www.microsoft.com/licensing/how-to-buy/how-to-buy.aspx) (http://www.microsoft.com/licensing/how-to-buy/how-to-buy.aspx).  
  
### <a name="community-content"></a>Conteúdo da Comunidade  
  
-   [Licenciamento do SQL Server 2014 Developer Edition](http://sqlmag.com/sql-server-2014/sql-server-2014-developer-edition-licensing).  
  
-   [Alterações no licenciamento do SQL Server 2014](http://www.brentozar.com/archive/2014/04/sql-server-2014-licensing-changes)(http://www.brentozar.com/archive/2014/04/sql-server-2014-licensing-changes).  
  
-   [Alterações no licenciamento do SQL Server 2014](https://www.directionsonmicrosoft.com/sites/default/files/PDFs/Licensing_Changes_for_SQL_Server_2014.pdf)(https://www.directionsonmicrosoft.com/sites/default/files/PDFs/Licensing_Changes_for_SQL_Server_2014.pdf).  
  
-   [Estimar os custos de licenciamento do SharePoint 2013](http://www.degdigital.com/blog/sharepoint-2013-licensing-for-dummies/) (http://www.degdigital.com/blog/sharepoint-2013-licensing-for-dummies/).  
  
-   [Comunidade de clientes de licenciamento por Volume da Microsoft](http://www.microsoft.com/licensing/existing-customers/community.aspx) (http://www.microsoft.com/licensing/existing-customers/community.aspx).  
  
  