---
title: Definindo uma dimensão | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 38185df9928286acf184fbad21fd75839856d017
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-2-1---defining-a-dimension"></a>Lição 2-1-definir uma dimensão
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Na tarefa a seguir, você usará o Assistente para Dimensões para criar uma dimensão Data.  
  
> [!NOTE]  
> Esta lição requer a conclusão de todos os procedimentos da Lição 1.  
  
### <a name="to-define-a-dimension"></a>Para definir uma dimensão  
  
1.  No Gerenciador de Soluções (no lado direito da janela Microsoft Visual Studio), clique com o botão direito do mouse em **Dimensões**e clique em **Nova Dimensão**. O Assistente para Dimensões é exibido.  
  
2.  Na página **Bem-vindo ao Assistente para Dimensões** , clique em **Avançar**.  
  
3.  Na página **Selecionar Método de Criação** , verifique se a opção **Usar uma tabela existente** está selecionada e clique em **Avançar**.  
  
4.  Na página **Especificar Informações da Fonte** , verifique se a exibição da fonte de dados **Adventure Works DW 2012** está selecionada.  
  
5.  Na lista **Tabela principal** , selecione **Date**.  
  
6.  Clique em **Avançar**.  
  
7.  Na página **Selecionar Atributos de Dimensão** , marque as caixas de seleção dos seguintes atributos:  
  
    -   **Chave de Data**  
  
    -   **Chave Alternativa de Data Completa**  
  
    -   **Nome do Mês em Inglês**  
  
    -   **Calendar Quarter**  
  
    -   **Calendar Year**  
  
    -   **Calendar Semester**  
  
8.  Altere a configuração da coluna **Tipo de Atributo** do atributo **Full Date Alternate Key** de **Regular** para **Date**. Para fazer isso, clique em **Regular** na coluna **Tipo de Atributo** . Em seguida, clique na seta para expandir as opções. Em seguida, clique em **Data** > **Calendário** > **Data**. Clique em **OK**. Repita essas etapas para alterar o tipo de atributo dos atributos da seguinte maneira:  
  
    -   **English Month Name** para **Month**  
  
    -   **Calendar Quarter** para **Quarter**  
  
    -   **Ano Civil** para **Ano**  
  
    -   **Calendar Semester** para **Half Year**  
  
9. Clique em **Avançar**.  
  
10. Na página **Concluindo o Assistente** , no painel Visualização, é possível ver a dimensão **Data** e seus atributos.  
  
11. Clique em **Concluir** para concluir o assistente.  
  
    No Gerenciador de Soluções, no projeto Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , a dimensão Data é exibida na pasta **Dimensões** . No centro do ambiente de desenvolvimento, o Designer de Dimensão exibe a dimensão Data.  
  
12. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Definindo um cubo](../analysis-services/lesson-2-2-defining-a-cube.md)  
  
## <a name="see-also"></a>Consulte também  
[Dimensões em modelos multidimensionais](../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)  
[Criar uma dimensão usando uma tabela existente](../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)  
[Criar uma dimensão usando o Assistente para Dimensões](../analysis-services/multidimensional-models/create-a-dimension-using-the-dimension-wizard.md)  
  
  
  
