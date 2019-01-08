---
title: 'Lista de verificação de implantação: Reporting Services, Power View e PowerPivot para SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 9a2575c8-06fc-4ef4-9f24-c19e52b1bbcf
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2aa1133b9e23ea8f2174f73e9d8bf4a34ff0c824
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369098"
---
# <a name="deployment-checklist-reporting-services-power-view-and-powerpivot-for-sharepoint"></a>Lista de verificação de implantação: Reporting Services, Power View e PowerPivot para SharePoint
  Use a lista de verificação a seguir para instalar esses recursos de BI no mesmo farm do SharePoint: PowerPivot para SharePoint, construtor de relatórios e [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. Embora essa lista de verificação recomende uma ordem de instalação específica, na prática você pode instalar esses recursos em praticamente qualquer ordem. Essa lista de verificação presume a instalação dos seguintes produtos ou recursos:  
  
1.  SharePoint Server 2010 com Service Pack 1 (SP1)  
  
2.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Mecanismo de banco de dados  
  
3.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services e suplemento Reporting Services  
  
4.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot para SharePoint  
  
 Depois de instalar esses recursos, você poderá fazer o seguinte.  
  
-   Acessar as pastas de trabalho PowerPivot criadas no PowerPivot para Excel dos sites do SharePoint.  
  
-   Criar relatórios interativos do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] com base em pastas de trabalho PowerPivot no SharePoint.  
  
-   Criar relatórios do Construtor de Relatórios ao lançar o Construtor de Relatórios no SharePoint.  
  
> [!NOTE]  
>  O PowerPivot para SharePoint exige que você instale o SharePoint 2010 Service Pack 1 (SP1) no farm do SharePoint. Se você estiver instalando o software para fins de avaliação, comece com um servidor limpo para evitar a sobrecarga de uma etapa de atualização de farm. Atualizar um farm tem impacto em operações do SharePoint e geralmente exige planejamento cuidadoso. Se seu objetivo é instalar o PowerPivot para SharePoint o mais rápido possível, siga esta abordagem: instale o SharePoint 2010, instale o SharePoint 2010 SP1 e configure o farm em uma etapa posterior. A atualização é evitada porque o farm ainda não está configurado quando você instala o SharePoint 2010 SP1.  
>   
>  Nesta lista de verificação, a etapa de configuração do farm é presumida durante a configuração do PowerPivot para SharePoint, usando a Ferramenta de Configuração do PowerPivot. Como alternativa, você poderá usar o assistente de Configuração de Produto do SharePoint se preferir essa abordagem. Ambas as abordagem resultam em um farm operacional que dá suporte a PowerPivot para SharePoint.  
  
## <a name="prerequisites"></a>Prerequisites  
 Você deve ser um administrador local para executar a Instalação do SQL Server.  
  
 A edição SharePoint Server 2010 enterprise é necessária para o PowerPivot para SharePoint. Você também pode usar a edição evaluation enterprise.  
  
 O SharePoint Server 2010 SP1 deve ser instalado. Sem ele, você não poderá configurar o farm para usar os recursos do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] .  
  
 O computador deve ser unido a um domínio.  
  
 Você deve ter uma ou mais contas de usuário de domínio para provisionar os serviços. Você precisará de contas de usuário de domínio para os seguintes serviços: Serviços Web e serviços administrativos do SharePoint, Reporting Services, Analysis Services, Excel Services, Secure Store Services e Serviço de Sistema PowerPivot. Contas de domínio são necessárias pelo recurso de contas gerenciadas no SharePoint. O Mecanismo de Banco de Dados pode ser provisionado usando uma conta virtual, mas todos os outros serviços devem ser executados como um usuário de domínio.  
  
 O nome da instância do PowerPivot deve estar disponível. Você não pode ter uma instância nomeada existente do PowerPivot no computador em que está instalando o PowerPivot para SharePoint.  
  
 Se você estiver instalando o PowerPivot para SharePoint em um farm existente, deverá ter um ou mais aplicativos Web SharePoint configurados para a autenticação de modo clássico. O acesso a dados PowerPivot só funcionará se o aplicativo Web oferecer suporte à autenticação de modo clássica. Para obter mais informações sobre requisitos do modo clássico, consulte [PowerPivot Authentication and Authorization](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md).  
  
 Analise os tópicos adicionais a seguir para entender os requisitos de sistema e de versão:  
  
-   [Orientação para usar os recursos de BI do SQL Server em um farm do SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
## <a name="steps"></a>Etapas  
 As etapas a seguir pressupõem que um administrador esteja instalando e configurando o servidor. O usuário da instalação no SharePoint também é um administrador de farm e geralmente o administrador de sites primários da coleção de sites padrão. Se você estiver dividindo as etapas a seguir entre diversas pessoas, podem ser necessárias permissões adicionais para que as etapas a seguir funcionem.  
  
|Etapa|Link|  
|----------|----------|  
|Execute a ferramenta de preparação dos produtos do SharePoint 2010.|Você deve ter a mídia de instalação do SharePoint 2010. A ferramenta de preparação é o PrerequisiteInstaller.exe na mídia de instalação.|  
|Instale o SharePoint Server 2010 enterprise ou a edição enterprise evaluation.|Ao instalar o SharePoint, se você decidir configurar o farm posteriormente, não execute o Assistente de Configuração de Produtos do SharePoint 2010 depois que a Instalação for concluída. Aguardar para configurar o farm permitirá que você use um [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instância do mecanismo de banco de dados, que é instalada em uma etapa posterior, como o servidor de banco de dados do farm. Para configurar o farm, você usará a Ferramenta de Configuração do PowerPivot. Ela inclui ações para provisionar o farm se ele ainda não estiver configurado.|  
|Instale o SharePoint Server 2010 SP1.|Baixar o SP1 do [ https://support.microsoft.com/kb/2460045 ](https://go.microsoft.com/fwlink/p/?linkID=219697).|  
|Execute a instalação do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para instalar o Mecanismo de Banco de Dados e o PowerPivot para SharePoint.|[Instalar o PowerPivot para SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> A etapa 1 explica como instalar o PowerPivot para SharePoint. Nessa etapa, clique na caixa de seleção na página Função de Instalação que adiciona o Mecanismo de Banco de Dados à função. Isso adiciona o mecanismo de banco de dados à sua instalação para que você pode usá-lo como servidor de banco de dados do farm, quando você configurar o farm na próxima etapa. No entanto, se o farm já estiver configurado, essa etapa poderá ser ignorada.<br /><br /> A etapa 2 pede que você configure o servidor. Para essa etapa, escolha a ferramenta de Configuração do PowerPivot. Embora diversas abordagens estejam disponíveis, usar a ferramenta de configuração é a mais eficiente para uma instalação autônoma.<br /><br /> Se o SharePoint 2010 estiver instalado, mas não configurado, a ferramenta pré-selecionará ações que criarão o farm, um aplicativo Web padrão e uma coleção de sites raiz. Deixe essas opções selecionadas para que o farm seja criado. Se você já tiver configurado o farm, a ferramenta omitirá essas ações, e oferecerá apenas as ações necessárias para configurar o PowerPivot para SharePoint.<br /><br /> A etapa 3 pede que você instale a versão do SQL Server 2008 R2 do Provedor OLE DB do Analysis Services. Essa etapa é importante para dar suporte a versões de uma pasta de trabalho que foi criada na versão 2008 R2 do PowerPivot para Excel.|  
|Verifique se o farm está funcionando.|Primeiro, inicie a Administração Central e confirme se está disponível. Em seguida, abra o site de equipe inserindo http://localhost.  Você verá um site de equipe do SharePoint.|  
|Verifique se o PowerPivot para SharePoint está funcionando.|[Verificar uma instalação do PowerPivot para SharePoint](../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md)<br /><br /> Essa tarefa confirma o acesso a dados PowerPivot usando a pasta de trabalho que você carregou.|  
|Execute a Instalação do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para instalar e configurar o Reporting Services e o Suplemento Reporting Services.|[Instalar o Reporting Services no modo do SharePoint para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)<br /><br /> Como opção, enquanto estiver instalando o Reporting Services, você pode adicionar outra instância do Analysis Services à árvore de recursos de instalação se desejar um segundo recurso para hospedar dados tabulares. A instância adicional do Analysis Services será usada para hospedar bancos de dados modelo tabulares que você cria no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Bancos de dados tabulares são uma fonte de dados válida para relatórios do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].<br /><br /> [Instalar o Analysis Services em modo Tabular](../../analysis-services/instances/install-windows/install-analysis-services.md)|  
|Verifique se o Reporting Services está funcionando.|[Verificar uma instalação do Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)|  
|(Administradores de sites) Configurar permissões do SharePoint.|Permissões de colaboração são necessárias para adicionar, editar ou excluir itens em bibliotecas do SharePoint. O nível de permissão Exibição é suficiente para acesso somente leitura a relatórios e pastas de trabalho PowerPivot que apresentam dados inseridos.<br /><br /> As pastas de trabalho PowerPivot acessadas como fontes de dados externas (onde a URL da pasta de trabalho é uma cadeia de conexão em outra pasta de trabalho ou relatório) exigem permissões de Leitura, que é maior que as permissões de Exibição.<br /><br /> As conexões de modelo semântico BI também exigem permissões de Leitura. Você pode precisar criar novos níveis de permissão ou grupos do SharePoint para obter as permissões corretas necessárias.|  
|(Administradores do site) Estender bibliotecas de documentos|Estenda bibliotecas de documentos para usar tipos de conteúdo de BI: Conexões de modelo semântico BI, Fontes de Dados Compartilhadas do Reporting Services, relatórios do Construtor de Relatórios:<br /><br /> 1) <br />                    **Habilitar o gerenciamento de tipo de conteúdo**. Em documentos compartilhados ou outra biblioteca de documentos, na guia biblioteca, clique em **configurações de biblioteca**. Em configurações gerais, clique em **configurações avançadas**. Em tipos de conteúdo, selecione **Yes** para permitir o gerenciamento de tipos de conteúdo e, em seguida, clique em **Okey**.<br /><br /> 2) <br />                    **Selecione os tipos de conteúdo de BI**. Na guia biblioteca, clique em **configurações de biblioteca**. Em tipos de conteúdo, clique em **adicionar a partir de tipos de conteúdo de site existentes**. A partir do grupo de tipo de conteúdo de Business Intelligence, adicione **arquivo de Conexão de modelo semântico BI** e **fonte de dados de relatório**. Outra opção é adicionar outros tipos de conteúdo do Reporting Services, como Modelo de Relatório, para habilitar outros cenários de criação de relatórios.<br /><br /> <br /><br /> Para obter mais informações, consulte [adicionar um tipo BI Semantic modelo Conexão conteúdo em uma biblioteca do &#40;PowerPivot para SharePoint&#41; ](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md) e [Adicionar servidor de tipos de conteúdo relatório em uma biblioteca do &#40;Reporting Services no Modo integrado do SharePoint&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|(Administradores do site) Criar arquivos de conexão de dados que são usados para iniciar o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].|Você deve criar uma conexão de modelo semântico BI (.bism) ou uma fonte de dados compartilhados do Reporting Services (.rsds) como uma fonte de dados para o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. Depois de criar um arquivo de conexão de dados, você pode iniciar o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] usando a conexão de dados como sua fonte de dados.<br /><br /> [Criar uma conexão de modelo semântico de BI para uma pastas de trabalho PowerPivot](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)<br /><br /> [Criar uma conexão de modelo semântico de BI com um banco de dados de modelo de tabela](../../relational-databases/databases/model-database.md)<br /><br /> Observação: o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] está disponível porque você instalou a versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] do Reporting Services e configurou o servidor como um serviço compartilhado. Se você instalou o Reporting Services e o configurou para o nível de integração do SQL Server 2008, o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] não está disponível.|  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)  
  
  
