---
title: Definir parâmetros no Designer de consulta MDX do Analysis Services (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- parameters [Reporting Services], MDX
- Multidimensional Expressions [Reporting Services]
- Data Mining Prediction [Reporting Services]
- MDX [Reporting Services], defining parameters
- DMX [Reporting Services]
ms.assetid: 4ad1e5bc-f510-4752-b4f6-589e55317a90
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c1b3696612ab9d0693b3c0135b6aff34137906b7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107308"
---
# <a name="define-parameters-in-the-mdx-query-designer-for-analysis-services-report-builder-and-ssrs"></a>Definir parâmetros no Designer de Consulta MDX do Analysis Services (Construtor de Relatórios e SSRS)
  Para parametrizar uma consulta MDX referente a uma fonte de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , é necessário adicionar um parâmetro de consulta à consulta. No designer de consulta MDX, você pode adicionar um parâmetro de consulta nos modos de Design e de Consulta especificando um filtro. Depois de definir a consulta com um parâmetro de consulta, o Reporting Services cria automaticamente um parâmetro de relatório e um conjunto de dados para fornecer a lista de valores válidos. Dessa forma, o usuário pode especificar um valor que é passado diretamente para a consulta.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-define-a-query-parameter-in-mdx-in-design-mode"></a>Para definir um parâmetro de consulta em MDX no modo de Design  
  
1.  No painel de dados do relatório, clique com o botão direito do mouse em um conjunto de dados criado com base em um tipo de fonte de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e clique em **Consulta**. O designer de consulta MDX abre no modo de Design.  
  
2.  Arraste uma dimensão até a área de filtro e solte-a na primeira célula da coluna **Dimensão** .  
  
3.  Na coluna **Hierarquia** , escolha um valor na lista suspensa.  
  
4.  Na coluna **Operador** , escolha um operador na lista suspensa.  
  
5.  Na coluna **Expressão de Filtro** , selecione valores individuais na lista suspensa ou clique no membro **Todos** para escolher todos os valores.  
  
6.  Na coluna **Parâmetros** , marque a caixa de seleção para criar um parâmetro de relatório.  
  
7.  Clique em **Executar**.  
  
     Depois de executar a consulta, clique em **Design** , na barra de ferramentas, para alternar para o modo de Consulta e exibir a consulta MDX que foi criada. Não altere o texto da consulta no modo de Consulta se deseja continuar usando o modo de Design para desenvolver a consulta. Clique em **Design** para voltar ao modo de Design.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     No painel de dados do relatório, expanda o nó Parâmetros para exibir o parâmetro de relatório que foi criado automaticamente para o filtro.  
  
     Para exibir o conjunto de dados que fornece os valores disponíveis para o parâmetro de relatório, clique com o botão direito do mouse em qualquer área em branco do painel de dados do relatório e clique em **Mostrar Conjuntos de Dados Ocultos**. O painel de dados do relatório exibe todos os conjuntos de dados do relatório.  
  
### <a name="to-define-a-query-parameter-in-mdx-in-query-mode"></a>Para definir um parâmetro de consulta em MDX no modo de Consulta  
  
1.  No painel de dados do relatório, clique com o botão direito do mouse em um conjunto de dados criado com base em um tipo de fonte de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e clique em **Consulta**. O designer de consulta MDX abre no modo de Design.  
  
2.  Na barra de ferramentas, clique em **Design** para alternar para o modo de Consulta.  
  
3.  Na barra de ferramentas do designer de consultas MDX, clique em **Parâmetros de Consulta** (![Ícone da caixa de diálogo Parâmetros de Consulta](../../analysis-services/media/iconqueryparameter.gif "Ícone da caixa de diálogo Parâmetros de Consulta")). A caixa de diálogo Parâmetros de Consulta é exibida.  
  
4.  Na coluna **Parâmetro**, clique em **\<Inserir Parâmetro>** e, em seguida, digite o nome de um parâmetro.  
  
5.  Na coluna **Dimensão** , escolha um valor na lista suspensa.  
  
6.  Na coluna **Hierarquia** , escolha um valor na lista suspensa.  
  
7.  Na coluna **Vários valores** , marque a caixa de seleção para criar um parâmetro de vários valores.  
  
8.  Na coluna **Padrão** , selecione um único valor ou vários valores na lista suspensa, conforme sua escolha na etapa 5.  
  
9. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
10. Na barra de ferramentas do designer de consulta, clique em **Executar**.  
  
11. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     No painel de dados do relatório, expanda o nó Parâmetros para exibir o parâmetro de relatório que foi criado automaticamente para o filtro.  
  
     Para exibir o conjunto de dados que fornece os valores disponíveis para o parâmetro de relatório, clique com o botão direito do mouse em qualquer área em branco do painel de dados do relatório e clique em **Mostrar Conjuntos de Dados Ocultos**. O painel de dados do relatório exibe todos os conjuntos de dados do relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de conexão Analysis Services para MDX &#40;SSRS&#41;](analysis-services-connection-type-for-mdx-ssrs.md)   
 [Interface do usuário do Designer de Consulta MDX do Analysis Services](analysis-services-mdx-query-designer-user-interface.md)  
  
  
