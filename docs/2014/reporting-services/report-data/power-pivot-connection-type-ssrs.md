---
title: Tipo de Conexão PowerPivot (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a104c3c7-f118-4d02-9a0f-6859f1469d11
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bce7d17a2edb004f662d5229ea929d89c6d66d4f
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53350486"
---
# <a name="powerpivot-connection-type-ssrs"></a>Tipo de conexão PowerPivot (SSRS)
  É possível usar a extensão de processamento de dados do SQL Server Analysis Services para recuperar dados de uma pasta de trabalho PowerPivot publicada em uma Galeria PowerPivot do SharePoint.  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;construtor de relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 A fonte de dados PowerPivot deve ser publicada em um Galeria PowerPivot em um site do SharePoint.  
  
 Para dar suporte a conexões do Construtor de Relatórios a uma pasta de trabalho PowerPivot, o SQL Server 2008 R2 ADOMD.NET deve estar instalado no computador de sua estação de trabalho. Essa biblioteca de cliente é instalada com o PowerPivot para Excel, mas se você estiver usando um computador que não tenha esse aplicativo, deverá baixar e instalar o ADOMD.NET no site [SQL Server 2008 R2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=192565).  
  
## <a name="data-source-type"></a>Tipo de fonte de dados  
 Use o tipo de fonte de dados de relatório **Microsoft SQL Server Analysis Services**.  
  
## <a name="connection-string"></a>Cadeia de Conexão  
 A cadeia de caracteres de conexão é a URL para a pasta de trabalho PowerPivot publicada no SharePoint na Galeria PowerPivot ou em outra biblioteca, por exemplo, http://contoso-srv/subsite/PowerPivotLibrary/ContosoSales.xlsx.  
  
## <a name="credentials"></a>Credenciais  
 Especifique as credenciais que você precisa para acessar a pasta de trabalho PowerPivot e o site do SharePoint, por exemplo, Autenticação do Windows (Segurança Integrada). Para obter mais informações, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) ou [especificar as credenciais no construtor de relatórios](../specify-credentials-in-report-builder.md).  
  
## <a name="queries"></a>Consultas  
 Depois de conectar-se à fonte de dados PowerPivot, use a consulta gráfica MDX para criar uma consulta por meio de procura e seleção nas estruturas de dados subjacentes. Depois de criar uma consulta, execute-a para ver os dados de exemplo no painel de resultados.  
  
 O designer de consulta analisa a consulta para determinar os campos do conjunto de dados. Você também pode editar manualmente a coleção de campos do conjunto de dados no painel **Dados do Relatório** . Para saber mais, confira [Adicionar, editar e atualizar campos no painel de dados do relatório &#40;Construtor de Relatórios e SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
## <a name="filters"></a>Filtros  
 No painel Filtros, especifique dimensões e membros a serem filtrados ou incluídos nos resultados da consulta.  
  
## <a name="parameters"></a>Parâmetros  
 No painel Filtros, selecione a opção **Parâmetros** de um filtro para criar automaticamente um parâmetro de relatório com os valores disponíveis correspondentes às seleções do filtro.  
  
## <a name="remarks"></a>Comentários  
 Se você abrir o Construtor de Relatórios na pasta de trabalho PowerPivot em uma Galeria PowerPivot, as Tabelas Dinâmicas, os Gráficos Dinâmicos, as segmentações de dados e outros recursos de layout e analíticos da pasta de trabalho PowerPivot não serão recriados no relatório. Em vez disso, o relatório em branco inclui uma fonte de dados pré-configurada que aponta para os dados na pasta de trabalho PowerPivot. A criação de relatórios com base em uma pasta de trabalho PowerPivot pode ser trabalhosa e demorada dependendo do número de segmentações de dados, filtros e tabelas ou gráficos que você deseja recriar no relatório. Uma abordagem melhor é prever a apresentação dos dados desejada em um relatório, independentemente do design do PowerPivot.  
  
 Os dados em uma pasta de trabalho PowerPivot são altamente compactados. Os dados recuperados da pasta de trabalho PowerPivot para um relatório não são compactados. Use o designer de consulta para especificar filtros e parâmetros para limitar os dados para apenas o que é necessário no relatório.  
  
 Ao contrário da conexão a um cubo do Analysis Services, um modelo PowerPivot não tem nenhuma hierarquia. Para fornecer funcionalidade semelhante a segmentações de dados na pasta de trabalho, você deve criar parâmetros em cascata no relatório. Para obter mais informações, consulte [Adicionar parâmetros em cascata a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md).  
  
 Em alguns casos, pode ser necessário ajustar expressões para acomodar os valores de dados subjacentes do modelo PowerPivot. Pode ser necessário modificar expressões para converter dados no tipo de dados correto ou adicionar ou remover uma função de agregação. Por exemplo, para converter o tipo de dados Cadeia de caracteres em Inteiro, use `=CInt`. Verifique sempre se o relatório exibe os valores esperados dos dados no modelo PowerPivot antes de publicá-lo.  
  
 Imagens de visualização de um relatório em uma Galeria PowerPivot serão geradas apenas se as seguintes condições forem atendidas:  
  
-   O relatório e a pasta de trabalho PowerPivot que fornece os dados devem ser armazenados juntos na mesma Galeria PowerPivot.  
  
-   O relatório contém apenas dados PowerPivot de uma fonte de dados PowerPivot.  
  
## <a name="see-also"></a>Consulte também  
 [Interface do usuário do Designer de Consultas MDX do Analysis Services &#40;Construtor de Relatórios&#41;](../analysis-services-mdx-query-designer-user-interface-report-builder.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
