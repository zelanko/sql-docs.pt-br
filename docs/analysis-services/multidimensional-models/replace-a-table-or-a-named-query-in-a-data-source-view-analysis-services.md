---
title: Substituir uma tabela ou uma consulta nomeada em uma exibição da fonte de dados (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a171eafc35446f588d64c74457792912dcebe75a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services"></a>Substituir uma tabela ou uma consulta nomeada em uma exibição da fonte de dados (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  No Designer de Exibição da Fonte de Dados, é possível substituir uma tabela, exibição ou consulta nomeada de uma DSV (exibição da fonte de dados) por outra tabela ou exibição da mesma fonte de dados ou de outra ou ainda por uma consulta nomeada definida na DSV. Quando você substitui uma tabela, as referências existentes para essa tabela em todos os outros objetos do banco de dados ou projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são preservadas porque a identificação do objeto para a tabela na DSV não é alterada. Todas as relações que ainda são relevantes (com base no nome e na correspondência coluna-tipo) são mantidas. Diferentemente, se você excluir e, em seguida, adicionar uma tabela, as referências e relações serão perdidas e terão de ser recriadas.  
  
 Para substituir uma tabela por outra, é necessária uma conexão ativa com a fonte de dados no Designer de Exibição da Fonte de Dados em modo de projeto.  
  
 O que ocorre com mais frequência é a substituição de uma tabela da exibição da fonte de dados por outra tabela da fonte de dados. No entanto, você também pode substituir uma consulta nomeada por uma tabela. Por exemplo, anteriormente, você substituiu uma tabela por uma consulta nomeada e agora deseja voltar para a tabela.  
  
> [!IMPORTANT]  
>  Se você renomear uma tabela de uma fonte de dados, siga os passos de substituição de tabela e especifique a tabela renomeada como a fonte da tabela correspondente na DSV antes de atualizá-la. A conclusão do processo de substituir e renomear preservará a tabela, suas referências e relações na DSV. Caso contrário, quando você atualizar a DSV, uma tabela renomeada na fonte de dados será interpretada como se tivesse sido excluída. Para obter mais informações, consulte [Atualizar o esquema em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/refresh-the-schema-in-a-data-source-view-analysis-services.md).  
  
##  <a name="bkmk_nq"></a> Substituir uma tabela com uma consulta nomeada  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto ou conecte-se ao banco de dados que contém a exibição da fonte de dados na qual existe uma tabela ou consulta nomeada que você deseja substituir.  
  
2.  No Gerenciador de Soluções, expanda a pasta **Exibições da Fonte de Dados** e clique duas vezes na exibição da fontes de dados.  
  
3.  Abra a caixa de diálogo **Criar Consulta Nomeada** . No painel **Tabelas** ou **Diagrama** , clique com o botão direito do mouse na tabela que você deseja substituir, aponte para **Substituir Tabela** e, em seguida, clique em **Com Nova Consulta Nomeada**.  
  
4.  Na caixa de diálogo **Criar Consulta Nomeada** , defina a consulta nomeada e, em seguida, clique em **OK**.  
  
5.  Salve a exibição de fonte de dados modificada.  
  
## <a name="replace-a-table-or-named-query-with-a-table"></a>Substituir uma tabela ou consulta nomeada por uma tabela  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto ou conecte-se ao banco de dados que contém a exibição da fonte de dados na qual existe uma tabela ou consulta nomeada que você deseja substituir.  
  
2.  No Gerenciador de Soluções, expanda a pasta **Exibições da Fonte de Dados** e clique duas vezes na exibição da fontes de dados.  
  
3.  Abra a caixa de diálogo **Substituir Tabela por Outra** . No painel **Tabelas** ou **Diagrama** , clique com o botão direito do mouse na tabela ou na consulta nomeada que você deseja substituir, aponte para **Substituir Tabela** e, em seguida, clique em **Com Outra Tabela**.  
  
4.  Na caixa de diálogo **Substituir Tabela por Outra** :  
  
    1.  Na caixa de listagem suspensa **Fonte de dados** , selecione a fonte de dados desejada  
  
    2.  Selecione a tabela pela qual você deseja substituir a tabela ou consulta nomeada.  
  
5.  Clique em **OK**.  
  
6.  Salve a exibição de fonte de dados modificada.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições da fonte de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
