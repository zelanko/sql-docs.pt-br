---
title: Analisar um modelo tabular do Analysis Services no Excel | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a3cd28375a60dc2cbf7447068fde8c5a1c7dba07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163125"
---
# <a name="analyze-a-tabular-model-in-excel"></a>Analisar um modelo tabular no Excel  
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  O recurso Analisar no Excel no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] abre o Microsoft Excel, cria uma conexão da fonte de dados para o banco de dados de workspace modelo e adiciona uma Tabela Dinâmica à planilha. Os objetos de modelo (tabelas, colunas, medidas, hierarquias e KPIs) são incluídos como campos na lista de campos da Tabela Dinâmica.  
  
> [!NOTE]  
>  Para usar o recurso Analisar no Excel, você deve ter o Microsoft Office 2003 ou superior instalado no mesmo computador que o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Se o Office não estiver instalado no mesmo computador, você poderá usar o Excel em outro computador e conectar-se ao banco de dados de workspace do modelo como uma fonte de dados. Você pode então adicionar manualmente uma Tabela Dinâmica à planilha. Os objetos de modelo (tabelas, colunas, medidas e KPIs) são incluídos como campos na lista de campos da Tabela Dinâmica.  
  
## <a name="tasks"></a>Tarefas  
  
#### <a name="to-analyze-a-tabular-model-project-by-using-the-analyze-in-excel-feature"></a>Para analisar um projeto de modelo tabular usando o recurso Analisar no Excel  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Analisar no Excel**.  
  
2.  Na caixa de diálogo **Escolher Credencial e Perspectiva**, selecione uma das opções de credencial a seguir para conectar-se à fonte de dados de workspace modelo:  
  
    -   Para usar a conta de usuário atual, selecione **Usuário atual do Windows**.  
  
    -   Para usar uma conta de usuário diferente, selecione **Outro Usuário do Windows**.  
  
         Normalmente, esta conta de usuário será membro de uma função. Nenhuma senha é necessária. A conta só pode ser usada no contexto de uma conexão do Excel com o banco de dados de workspace.  
  
    -   Para usar uma função de segurança, selecione **Função**e, na caixa de listagem, selecione uma ou mais funções.  
  
         As funções de segurança devem ser definidas usando o Gerenciador de Função. Para obter mais informações, consulte [criar e gerenciar funções](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
3.  Para usar uma perspectiva, na caixa de listagem **Perspectiva** , selecione uma perspectiva.  
  
     As perspectivas (além das padrão) devem ser definidas usando a caixa de diálogo Perspectivas. Para obter mais informações, consulte [criar e gerenciar perspectivas](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md).  
  
> [!NOTE]  
>  A Lista de campos Tabela Dinâmica no Excel não é atualizada automaticamente à medida que você faz alterações no projeto de modelo no designer modelo. Para atualizar a Lista de campos de Tabela Dinâmica, no Excel, na faixa de opções **Opções** , clique em **Atualizar**.  
  
## <a name="see-also"></a>Confira também  
 [Analisar no Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  
