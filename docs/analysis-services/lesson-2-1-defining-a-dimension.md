---
title: "Definindo uma dimensão | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 112696db-3838-4b50-91bd-d2ce5fa04ee5
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b6969c73bc6f466eb1a2acfd9d41ff21e80d727c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-1---defining-a-dimension"></a>Lição 2-1-definir uma dimensão
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
  
  
  

