---
title: "Definir consultas nomeadas em uma exibição da fonte de dados (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- named queries [Analysis Services], creating
- modifying named queries
- data source views [Analysis Services], named queries
ms.assetid: f09ba8aa-950e-4c0d-961e-970de13200be
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7a6db35f9ab119025bf5b7d60aed0b27747adaa8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="define-named-queries-in-a-data-source-view-analysis-services"></a>Definir consultas nomeadas em uma exibição da fonte de dados (Analysis Services)
  Uma consulta nomeada é uma expressão SQL representada como uma tabela. Em uma consulta nomeada, você pode especificar uma expressão SQL para selecionar linhas e colunas retornadas de uma ou mais tabelas em uma ou mais fontes de dados. Uma consulta nomeada é como qualquer outra tabela em uma DSV (exibição da fonte de dados) com linhas e relações, exceto que a consulta nomeada baseia-se em uma expressão.  
  
 Uma consulta nomeada permite que você estenda o esquema relacional das tabelas existentes em uma DSV sem modificar as tabelas ou exibições da fonte de dados subjacente. Por exemplo, uma série de consultas nomeadas pode ser usada para dividir uma tabela de dimensões complexa em tabelas de dimensões menores e mais simples para uso nas dimensões do banco de dados. A consulta nomeada também pode ser usada para unir várias tabelas do banco de dados de uma ou mais fontes de dados em uma única tabela de exibição da fonte de dados.  
  
## <a name="creating-a-named-query"></a>Criando uma consulta nomeada  
  
> [!NOTE]  
>  Não é possível adicionar um cálculo nomeado a uma consulta nomeada nem usar como base de uma consulta nomeada uma tabela que contém um cálculo nomeado.  
  
 Ao criar uma consulta nomeada, você especifica uma expressão SQL que retorna colunas e dados para a tabela e, opcionalmente, uma descrição da consulta nomeada. A expressão SQL pode fazer referência a outras tabelas da exibição da fonte de dados. Definida a consulta nomeada, a consulta SQL em uma consulta nomeada é enviada ao provedor da fonte de dados e validada por inteiro. Se o provedor não encontrar erros na consulta SQL, a coluna será adicionada à tabela.  
  
 Tabelas e colunas às quais a consulta SQL faz referência não devem ser qualificadas ou devem ser qualificadas somente pelo nome da tabela. Por exemplo, para fazer referência à coluna SaleAmount em uma tabela, o valor `SaleAmount` ou `Sales.SaleAmount` é válido, mas `dbo.Sales.SaleAmount` produzirá um erro.  
  
 **Observação** Ao definir uma consulta nomeada que consulta uma fonte de dados do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, a consulta nomeada que contiver uma subconsulta correlacionada e uma cláusula GROUP BY falhará. Para obter mais informações, consulte [Erro interno com a instrução SELECT contendo a subconsulta correlacionada e GROUP BY](http://support.microsoft.com/kb/274729) na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="add-or-edit-a-named-query"></a>Adicionar ou editar uma consulta nomeada  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto ou conecte-se ao banco de dados que contém a exibição da fonte de dados à qual você deseja adicionar uma consulta nomeada.  
  
2.  No Gerenciador de Soluções, expanda a pasta **Exibições da Fonte de Dados** e clique duas vezes na exibição da fontes de dados.  
  
3.  Clique com o botão direito do mouse em uma área livre do painel **Tabelas** ou **Diagrama** e clique em **Nova Consulta Nomeada**.  
  
4.  Na caixa de diálogo **Criar Consulta Nomeada** , faça o seguinte:  
  
    1.  Na caixa de texto **Nome** , digite o nome da consulta.  
  
    2.  Opcionalmente, na caixa de texto **Descrição** , digite uma descrição para a consulta.  
  
    3.  Na caixa de listagem **Fonte de Dados** , selecione a fonte de dados na qual a consulta nomeada será executada.  
  
    4.  Digite a consulta no painel inferior ou use as ferramentas gráficas de criação de consulta para criar uma consulta.  
  
    > [!NOTE]  
    >  A interface de usuário para criação de consultas varia de acordo com a fonte de dados. Em vez de obter uma interface de usuário gráfica, você poderá obter uma interface genérica baseada em texto. Você pode realizar as mesmas coisas com essas interfaces de usuário diferentes, mas deve fazê-las de maneiras diferentes. Para obter mais informações, consulte [Caixa de diálogo Criar ou Editar Consulta Nomeada &#40;Analysis Services – Dados Multidimensionais&#41;](http://msdn.microsoft.com/library/8e192ad6-a0b1-4e21-bb3f-087c93e62941).  
  
5.  Clique em **OK**. Um ícone mostrando duas tabelas sobrepostas aparece no título da tabela para indicar que a tabela foi substituída por uma consulta nomeada.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Definir cálculos nomeados em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
