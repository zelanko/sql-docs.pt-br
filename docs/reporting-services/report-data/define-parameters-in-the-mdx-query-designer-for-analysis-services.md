---
title: "Definir parâmetros no Designer de Consultas MDX do Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [Reporting Services], MDX
- Multidimensional Expressions [Reporting Services]
- Data Mining Prediction [Reporting Services]
- MDX [Reporting Services], defining parameters
- DMX [Reporting Services]
ms.assetid: 4ad1e5bc-f510-4752-b4f6-589e55317a90
caps.latest.revision: "37"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 728bbc3b0e39d7818460795144c09f56a15500d9
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="define-parameters-in-the-mdx-query-designer-for-analysis-services"></a>Definir parâmetros no Designer de Consulta MDX do Analysis Services
  Para parametrizar uma consulta MDX referente a uma fonte de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , é necessário adicionar um parâmetro de consulta à consulta. No designer de consulta MDX, você pode adicionar um parâmetro de consulta nos modos de Design e de Consulta especificando um filtro. Depois de definir a consulta com um parâmetro de consulta, o Reporting Services cria automaticamente um parâmetro de relatório e um conjunto de dados para fornecer a lista de valores válidos. Dessa forma, o usuário pode especificar um valor que é passado diretamente para a consulta.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-define-a-query-parameter-in-mdx-in-design-mode"></a>Para definir um parâmetro de consulta em MDX no modo de Design  
  
1.  No painel de dados do relatório, clique com o botão direito do mouse em um conjunto de dados criado com base em um tipo de fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e clique em **Consulta**. O designer de consulta MDX abre no modo de Design.  
  
2.  Arraste uma dimensão até a área de filtro e solte-a na primeira célula da coluna **Dimensão** .  
  
3.  Na coluna **Hierarquia** , escolha um valor na lista suspensa.  
  
4.  Na coluna **Operador** , escolha um operador na lista suspensa.  
  
5.  Na coluna **Expressão de Filtro** , selecione valores individuais na lista suspensa ou clique no membro **Todos** para escolher todos os valores.  
  
6.  Na coluna **Parâmetros** , marque a caixa de seleção para criar um parâmetro de relatório.  
  
7.  Clique em **Executar**.  
  
     Depois de executar a consulta, clique em **Design** , na barra de ferramentas, para alternar para o modo de Consulta e exibir a consulta MDX que foi criada. Não altere o texto da consulta no modo de Consulta se deseja continuar usando o modo de Design para desenvolver a consulta. Clique em **Design** para voltar ao modo de Design.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     No painel de dados do relatório, expanda o nó Parâmetros para exibir o parâmetro de relatório que foi criado automaticamente para o filtro.  
  
     Para exibir o conjunto de dados que fornece os valores disponíveis para o parâmetro de relatório, clique com o botão direito do mouse em qualquer área em branco do painel de dados do relatório e clique em **Mostrar Conjuntos de Dados Ocultos**. O painel de dados do relatório exibe todos os conjuntos de dados do relatório.  
  
### <a name="to-define-a-query-parameter-in-mdx-in-query-mode"></a>Para definir um parâmetro de consulta em MDX no modo de Consulta  
  
1.  No painel de dados do relatório, clique com o botão direito do mouse em um conjunto de dados criado com base em um tipo de fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e clique em **Consulta**. O designer de consulta MDX abre no modo de Design.  
  
2.  Na barra de ferramentas, clique em **Design** para alternar para o modo de Consulta.  
  
3.  Na barra de ferramentas do designer de consultas MDX, clique em **Parâmetros de Consulta** (![Ícone da caixa de diálogo Parâmetros de Consulta](../../reporting-services/report-data/media/iconqueryparameter.gif "Ícone da caixa de diálogo Parâmetros de Consulta")). A caixa de diálogo Parâmetros de Consulta é exibida.  
  
4.  Na coluna **Parâmetro**, clique em **\<Inserir Parâmetro>** e, em seguida, digite o nome de um parâmetro.  
  
5.  Na coluna **Dimensão** , escolha um valor na lista suspensa.  
  
6.  Na coluna **Hierarquia** , escolha um valor na lista suspensa.  
  
7.  Na coluna **Vários valores** , marque a caixa de seleção para criar um parâmetro de vários valores.  
  
8.  Na coluna **Padrão** , selecione um único valor ou vários valores na lista suspensa, conforme sua escolha na etapa 5.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Na barra de ferramentas do designer de consulta, clique em **Executar**.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     No painel de dados do relatório, expanda o nó Parâmetros para exibir o parâmetro de relatório que foi criado automaticamente para o filtro.  
  
     Para exibir o conjunto de dados que fornece os valores disponíveis para o parâmetro de relatório, clique com o botão direito do mouse em qualquer área em branco do painel de dados do relatório e clique em **Mostrar Conjuntos de Dados Ocultos**. O painel de dados do relatório exibe todos os conjuntos de dados do relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipo de conexão Analysis Services para MDX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)   
 [Interface do usuário do Designer de Consulta MDX do Analysis Services](../../reporting-services/report-data/analysis-services-mdx-query-designer-user-interface.md)  
  
  
