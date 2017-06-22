---
title: "Segurança (construtor de relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ed38291a-6afe-449f-9f32-3ae04502bd6f
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7e6f09ff050246777e307f73280c764dd6da3ad7
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="security-report-builder"></a>Segurança (Construtor de Relatórios)
  O Construtor de Relatórios é um aplicativo cliente de criação de relatórios projetado para funcionar com um servidor de relatório do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . O servidor de relatório pode ser configurado para funcionar em modo nativo como um servidor autônomo ou em modo integrado do SharePoint para oferecer suporte a relatórios em um site do SharePoint.  
  
 No Construtor de Relatórios, você pode criar relatórios, conjuntos de dados compartilhados e partes de relatório reutilizáveis. A partir de um servidor de relatório ou um site do SharePoint, você pode editar relatórios e adicionar fontes de dados compartilhadas, conjunto de dados compartilhados e partes de relatório compartilhadas.  
  
 Para criar, publicar e usar relatórios e itens relacionados a relatórios, você precisa compreender como os recursos de segurança se relacionam às áreas a seguir:  
  
-   **O servidor de relatório ou site do SharePoint onde você publica relatórios** Estes recursos são gerenciados pelo administrador de servidor de relatório ou pelo administrador de site do SharePoint.  
  
-   **Relatórios publicados e itens relacionados a relatórios** Os itens relacionados a relatórios incluem fontes de dados compartilhadas e inseridas e suas credenciais, conjuntos de dados compartilhados, parâmetros, partes de relatório e modelos de relatório. Os recursos de segurança que se aplicam a estes itens são gerenciados pelo autor do relatório. Permissões suficientes devem ser concedidas para o autor do relatório, por meio do administrador de servidor de relatório ou do administrador de site do SharePoint, para publicar e compartilhar os itens.  
  
-   **Fontes de dados externas usadas por um relatório** Estes recursos são gerenciados pelo proprietário da fonte de dados externa.  
  
-   **Modelos de relatório com base em fontes de dados externas** Estes recursos são gerenciados pelo criador do modelo.  
  
-   **Recursos de relatório interativos como parâmetros** Esses recursos são gerenciados pelo autor do relatório.  
  
 Revise as informações neste tópico para compreender melhor como usar recursos de segurança para ajudar a gerenciar e proteger relatórios e itens relacionados a relatórios.  
  
##  <a name="ReportServers"></a> Compreensão da segurança para servidores de relatórios  
 A publicação e a exibição de relatórios são operações privilegiadas. Um administrador de servidor de relatório concede permissões para garantir que apenas usuários autorizados possam publicar e exibir relatórios em um dos seguintes tipos de servidores de relatórios:  
  
-   Servidor de relatório configurado em modo nativo  
  
     Para conectar-se a ou navegar até um servidor de relatório, você deve ter uma URL válida e permissões suficientes para acessar o servidor.  
  
     Para exibir ou publicar itens em um servidor de relatório, são organizados conjuntos de permissões, que se aplicam a itens relacionados a relatório, e operações em funções. Um administrador de servidor de relatório atribui você a uma ou mais funções. Por exemplo, o Navegador de função predefinido permite que você exiba relatórios, pastas, modelos e recursos.  
  
     Se você não puder se conectar a ou navegar até um servidor de relatório, entre em contato com o administrador de servidor de relatório. Para obter mais informações, consulte [Segurança e proteção do Reporting Services](../../reporting-services/security/reporting-services-security-and-protection.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]](http://go.microsoft.com/fwlink/?linkid=121312).  
  
-   Servidor de relatório configurado no modo integrado do SharePoint  
  
     Para conectar-se a um site do SharePoint, integrado com um servidor de relatório, você deve ter uma URL válida para site do SharePoint ou subsite e deve ter permissões suficientes para o acesso.  
  
     A permissão para acessar operações e itens relacionados a relatórios é concedida por meio das políticas de segurança do SharePoint que mapeiam uma conta de usuário ou grupo com um nível de permissão, em relação a um item.  
  
     Se você não puder se conectar ou navegar até um site do SharePoint ou subsite, entre em contato com o administrador de site do SharePoint.  
  
  
##  <a name="Reports"></a> Compreensão da segurança para relatórios publicados e itens relacionados a relatórios  
 A segurança para relatórios e itens relacionados a relatórios é gerenciada pelo administrador de servidor de relatório. Itens relacionados a relatório incluem fontes de dados inseridas e compartilhadas, inclusive credenciais, conjuntos de dados compartilhados, parâmetros, partes de relatório e modelos.  
  
 Em um servidor de relatório ou site do SharePoint, os relatórios, itens relacionados a relatórios e operações são independentemente protegidos. A permissão para acessar itens e operações é concedida por meio das políticas de segurança que mapeiam uma conta de usuário ou grupo com um nível de permissão, em relação a um item. Para reduzir a complexidade e sobrecarga de manter um grande número de políticas, as permissões em um contêiner, como uma pasta, são herdadas através de itens no contêiner. Por exemplo, se um usuário tiver a permissão de Relatórios de Exibição específica em uma pasta, ele terá permissão de Relatórios de Exibição nos itens da pasta.  
  
 As permissões podem sobrepor itens ou pastas, usando a segurança no nível do item. Quando segurança a segurança no nível do item for aplicada, a herança da permissão do contêiner pai não se aplicará mais aos itens. Se a segurança no nível de item for aplicada a uma pasta, as pastas aninhadas herdarão as mesmas permissões.  
  
 Se não puder navegar e localizar itens que outra pessoa publicou para você, talvez seja um problema de permissões no item ou na pasta.  
  
 Para permitir que outras pessoas naveguem e publiquem itens que você publicou para ser compartilhado, trabalhe com o administrador de servidor de relatório para configurar uma organização de pastas que forneça acesso a seus usuários. O acesso deve estar disponível para criar relatórios e executar relatórios publicados.  
  
 Para obter mais informações, consulte os seguintes tópicos da documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [do](http://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [Funções e permissões &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)  
  
-   [Gerenciar conjuntos de dados compartilhados](../../reporting-services/report-data/manage-shared-datasets.md)  
  
### <a name="update-notifications-for-report-parts"></a>Atualize notificações para partes de relatório  
 As partes de relatório são publicadas em um servidor de relatório para que outras pessoas possam compartilhá-las. Através de design, você especifica o local no qual as partes de relatório serão publicadas.  
  
 Os usuários que incluem partes de relatório em seus relatórios podem habilitar o recurso de atualização. Quando este recurso for habilitado, os usuários receberão notificações assim que as partes de relatório forem alteradas no servidor de relatório.  
  
 Se as partes de relatório forem movidas do local original, o aviso de atualização incluirá o local atual e o local anterior da parte de relatório. Aceite atualizações somente de locais confiáveis.  
  
 Para obter mais informações, consulte [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
  
##  <a name="Data"></a> Compreensão da segurança para dados de relatório e fontes de dados externas  
 Para acessar dados de cada fonte de dados externa em um relatório, crie uma fonte de dados inserida, adicione uma referência a uma fonte de dados compartilhada ou compartilhe o conjunto de dados em seu relatório.  
  
 Para cada fonte de dados externa, forneça credenciais suficientes para acessar a origem e os dados subjacentes. O proprietário de fonte de dados especifica o tipo de credenciais que fornece este acesso.  
  
 As credenciais não são salvas na definição de relatório. Elas são gerenciadas independentemente do relatório no servidor de relatório, ou site do SharePoint, e no cliente de criação de relatório.  
  
 No momento do design do relatório, as credenciais são usadas para executar consultas de conjunto de dados e visualizar o relatório. No momento do design, as credenciais são usadas para executar consultas de relatório e consultas de cache. Você também pode armazenar em cache os resultados de consulta de conjunto de dados compartilhados independentemente. O tempo de design e o tempo de execução de credenciais podem ser diferentes. Para obter mais informações, consulte [Especificar as credenciais no Construtor de Relatórios](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
 Para obter mais informações sobre dados de segurança, consulte os seguintes tópicos da documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 Para obter mais informações sobre fontes de dados, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
  
##  <a name="Models"></a> Compreensão de modelos e filtros de segurança  
 Quando os dados são recuperados de um modelo de relatório com base em dados externos, você pode aplicar filtros de segurança no modelo. Essa é uma boa maneira de proteger dados, de forma que cada usuário que executar um relatório poderá consultar somente os dados que eles tiverem permissões.  
  
 Os parâmetros de relatório não são usados para segurança no nível de linha; eles não evitam que usuários ou grupos de usuários vejam linhas específicas de dados. Para aplicar segurança aos dados exibidos em um relatório, use filtros de segurança ou segurança do item de modelo.  
  
  
##  <a name="Interactive"></a> Compreensão da segurança para criação de relatórios para recursos interativos  
 Frequentemente, os relatórios usam parâmetros para permitir que um usuário personalize a exibição de um relatório interativamente. Use as dicas a seguir para criar relatórios que seguem as práticas recomendadas:  
  
-   Não use parâmetros com base em parâmetros de consulta que são do tipo **Texto** , a menos que você forneça valores válidos. Uma lista de valores disponível ajuda um usuário a escolher apenas valores válidos. Sem uma lista de valores disponível, não é possível restringir quais valores um usuário pode inserir.  
  
-   Não use o [&UserID] global para proteger dados privados. Como um parâmetro de relatório, esse valor pode ser especificado em uma URL de relatório, usando a sintaxe de acesso da URL. O uso deste valor em uma expressão em um conjunto de dados compartilhado impede que o conjunto de dados seja armazenado em cache. Para obter mais informações, consulte [Referência do parâmetro de acesso à URL](../../reporting-services/url-access-parameter-reference.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]](http://go.microsoft.com/fwlink/?linkid=121312).  
  
 Depois que os itens são publicados em um servidor de relatório, o administrador de servidor de relatório pode ajudar a protegê-los, atribuindo segurança com base em função ou segurança no nível do item ou da pasta. Para obter mais informações, consulte [Proteger relatórios e recursos](../../reporting-services/security/secure-reports-and-resources.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]](http://go.microsoft.com/fwlink/?linkid=121312).  
  
  
## <a name="see-also"></a>Consulte também  
 [Instalar e desinstalar o Construtor de Relatórios](http://msdn.microsoft.com/library/2c9a5814-17bf-4947-8fb3-6269e7caa416)   
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
