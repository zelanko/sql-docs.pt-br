---
title: "Criar uma nova estrutura de mineração relacional | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], relational
- mining structures [Analysis Services], creating
- relational mining models [Analysis Services]
ms.assetid: 55bac3bd-700e-4f91-bcc6-f3cd8c026da1
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6784d7ab5e13d5e842794041589db515a6fd2a30
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-new-relational-mining-structure"></a>Criar uma nova estrutura de mineração relacional
  Use o Assistente de Mineração de Dados para criar uma nova estrutura de mineração, usando dados de um banco de dados relacional ou outras fontes e, em seguida, salve a estrutura e os modelos relacionados em um banco de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="to-create-a-relational-mining-structure"></a>Para criar uma estrutura de mineração relacional  
  
1.  No gerenciador de soluções, clique com o botão direito do mouse na pasta **Estruturas de Mineração** no projeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e depois clique em **Nova Estrutura de Mineração**.  
  
     O Assistente de Mineração de Dados é exibido.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  Na página **Selecionar Método de Definição** , selecione **De banco de dados relacional ou data warehouse existente**e clique em **Avançar**.  
  
4.  Na página **Selecionar Técnica de Mineração de Dados** , selecione o algoritmo de mineração de dados que deseja usar e clique em **Avançar**.  
  
     Para obter mais informações sobre os algoritmos de mineração de dados, consulte [Algoritmos de mineração de dados &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
5.  Na página **Selecionar a Exibição da Fonte de Dados** , em **Exibições de fonte de dados disponíveis**, clique na exibição da fonte de dados que deseja usar e, em seguida, clique em **Avançar**.  
  
     Para obter mais informações sobre exibições de fonte de dados, consulte [Exibições de Fonte de Dados em Modelos Multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
6.  Na página **Especificar Tipos de Tabelas** , em **Tabelas de entrada**, selecione uma tabela de casos e uma tabela aninhada.  
  
7.  Na página **Especificar os Dados de Treinamento** , em **Estrutura de modelo de mineração**, selecione as colunas de chave, de entrada e as colunas previsíveis.  
  
     Depois de selecionar a coluna previsível, você pode clicar no botão **Sugerir** para abrir a caixa de diálogo **Sugerir Colunas Relacionadas** . Você pode aceitar as colunas sugeridas clicando em **OK** nessa caixa de diálogo, para incluir as colunas selecionadas na estrutura de mineração ou pode alterar as seleções na coluna **Entrada** primeiro e, em seguida, clicar em **OK**. Para ignorar as sugestões, clique em **Cancelar**.  
  
8.  Clique em **Avançar**.  
  
9. Na página **Especificar Conteúdo e Tipos de Dados das Colunas** , em **Estrutura de modelo de mineração**, você pode ajustar o tipo de conteúdo e o tipo de dados para cada coluna.  
  
    > [!NOTE]  
    >  Você pode clicar em **Detectar** para detectar automaticamente se uma coluna contém dados contínuos ou distintos. Depois de clicar nesse botão, o conteúdo e os tipos de dados da coluna serão atualizado nas colunas **Tipo de Conteúdo** e **Tipo de Dados** . Para obter mais informações sobre tipos de conteúdo e de dados, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](../../analysis-services/data-mining/content-types-data-mining.md) e [Tipos de dados &#40;Mineração de dados&#41;](../../analysis-services/data-mining/data-types-data-mining.md).  
  
10. Clique em **Avançar**.  
  
11. Na página **Concluindo o Assistente** , forneça um nome para a estrutura de mineração e o modelo de mineração inicial correspondente a ser criado e, em seguida, clique em **Concluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções da estrutura de mineração](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  

