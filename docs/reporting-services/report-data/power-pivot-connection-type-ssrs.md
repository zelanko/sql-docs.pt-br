---
title: Tipo de conexão do Power Pivot (SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: a104c3c7-f118-4d02-9a0f-6859f1469d11
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 21b727f60c0c60495c50e2e583b4cd776fd2e997
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571283"
---
# <a name="power-pivot-connection-type-ssrs"></a>Tipo de conexão Power Pivot (SSRS)
  É possível usar a extensão de processamento de dados do SQL Server Analysis Services para recuperar dados de uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] publicada em uma Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do SharePoint.  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 A fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] deve ser publicada em um Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um site do SharePoint.  
  
 Para dar suporte a conexões do Construtor de Relatórios a uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , o SQL Server 2008 R2 ADOMD.NET deve estar instalado no computador de sua estação de trabalho. Essa biblioteca de cliente é instalada com o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel, mas se você estiver usando um computador que não tenha esse aplicativo, deverá baixar e instalar o ADOMD.NET no [SQL Server 2008 R2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=192565).  
  
## <a name="data-source-type"></a>Tipo de fonte de dados  
 Use o tipo de fonte de dados de relatório **Microsoft SQL Server Analysis Services**.  
  
## <a name="connection-string"></a>Cadeia de Conexão  
 A cadeia de conexão é a URL para a pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] publicada no SharePoint na Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou em outra biblioteca, por exemplo, `https://contoso-srv/subsite/PowerPivotLibrary/ContosoSales.xlsx`.  
  
## <a name="credentials"></a>Credenciais  
 Especifique as credenciais que você precisa para acessar a pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e o site do SharePoint, por exemplo, Autenticação do Windows (Segurança Integrada). Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) ou [Especificar as credenciais no Construtor de Relatórios](https://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
## <a name="queries"></a>Consultas  
 Depois de se conectar à fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , use a consulta gráfica MDX para criar uma consulta por meio de procura e seleção nas estruturas de dados subjacentes. Depois de criar uma consulta, execute-a para ver os dados de exemplo no painel de resultados.  
  
 O designer de consulta analisa a consulta para determinar os campos do conjunto de dados. Você também pode editar manualmente a coleção de campos do conjunto de dados no painel **Dados do Relatório** . Para saber mais, confira [Adicionar, editar e atualizar campos no painel de dados do relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
## <a name="filters"></a>Filtros  
 No painel Filtros, especifique dimensões e membros a serem filtrados ou incluídos nos resultados da consulta.  
  
## <a name="parameters"></a>Parâmetros  
 No painel Filtros, selecione a opção **Parâmetros** de um filtro para criar automaticamente um parâmetro de relatório com os valores disponíveis correspondentes às seleções do filtro.  
  
## <a name="remarks"></a>Remarks  
 Se você abrir o Construtor de Relatórios na pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em uma Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , as Tabelas Dinâmicas, os Gráficos Dinâmicos, as segmentações de dados e outros recursos de layout e analíticos da pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não serão recriados no relatório. Em vez disso, o relatório em branco inclui uma fonte de dados pré-configurada que aponta para os dados na pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . A criação de relatórios com base em uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pode ser trabalhosa e demorada dependendo do número de segmentações de dados, filtros e tabelas ou gráficos que você deseja recriar no relatório. Uma abordagem melhor é prever a apresentação dos dados desejada em um relatório, independentemente do design do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Os dados em uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são altamente compactados. Os dados recuperados da pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para um relatório não são compactados. Use o designer de consulta para especificar filtros e parâmetros para limitar os dados para apenas o que é necessário no relatório.  
  
 Ao contrário da conexão a um cubo do Analysis Services, um modelo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não tem nenhuma hierarquia. Para fornecer funcionalidade semelhante a segmentações de dados na pasta de trabalho, você deve criar parâmetros em cascata no relatório. Para obter mais informações, consulte [Adicionar parâmetros em cascata a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md).  
  
 Em alguns casos, pode ser necessário ajustar expressões para acomodar os valores de dados subjacentes do modelo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Pode ser necessário modificar expressões para converter dados no tipo de dados correto ou adicionar ou remover uma função de agregação. Por exemplo, para converter o tipo de dados Cadeia de caracteres em Inteiro, use `=CInt`. Verifique sempre se o relatório exibe os valores esperados dos dados no modelo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] antes de publicá-lo.  
  
 Imagens de visualização de um relatório em uma Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] serão geradas apenas se as seguintes condições forem atendidas:  
  
-   O relatório e a pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que fornece os dados devem ser armazenados juntos na mesma Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   O relatório contém apenas dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de uma fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Interface do usuário do Designer de Consultas MDX do Analysis Services &#40;Construtor de Relatórios&#41;](https://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
