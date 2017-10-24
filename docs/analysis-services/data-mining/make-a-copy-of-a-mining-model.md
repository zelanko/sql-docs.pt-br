---
title: "Faça uma cópia de um modelo de mineração | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], copying
- mining models [Analysis Services], creating
- mining models [Analysis Services], how-to topics
- copying mining models
ms.assetid: 7975bb02-f188-49a0-b7de-5b9b216254ad
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aaa773a470cb0c2fea7929e3e6b331cfb0e7ed31
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="make-a-copy-of-a-mining-model"></a>Criar uma cópia de um modelo de mineração
  A criação de uma cópia de um modelo de mineração é útil quando você deseja criar rapidamente vários modelos de mineração com base nos mesmos dados. Após copiar o modelo, você pode editar a nova cópia alterando parâmetros ou adicionando um filtro.  
  
 Por exemplo, se você tem uma tabela Clientes vinculada a uma tabela de compras, pode criar cópias para gerar modelos de mineração separados para cada demografia de cliente, filtrando atributos como idade ou região.  
  
 Para obter informações sobre como copiar o conteúdo do modelo (como a representação gráfica ou os padrões de modelo) na Área de Transferência para uso em outros programas, consulte [Copiar a exibição de um modelo de mineração](../../analysis-services/data-mining/copy-a-view-of-a-mining-model.md).  
  
### <a name="to-create-a-related-mining-model"></a>Para criar um modelo de mineração relacionado  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no Gerenciador de Soluções, clique na estrutura de mineração que contém o modelo de mineração.  
  
2.  Clique na guia **Modelos de Mineração** .  
  
3.  Selecione o modelo, e clique com o botão direito do mouse para abrir o menu de atalho.  
  
     –ou–  
  
     Selecione o modelo. No menu **Modelo de Mineração** , selecione **Novo Modelo de Mineração**.  
  
4.  Digite um nome para o novo modelo de mineração e selecione um algoritmo. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-the-filter-on-the-copied-mining-model"></a>Para editar o filtro no modelo de mineração copiado  
  
1.  Selecione o modelo de mineração.  
  
2.  Na janela **Propriedades** , clique na caixa de texto da propriedade **Filtro** e, em seguida, clique no botão de criação **(…)** .  
  
3.  Altere as condições do filtro.  
  
     Para obter mais informações sobre como utilizar as caixas de diálogo do editor de filtro, consulte [Aplicar um filtro a um modelo de mineração](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md).  
  
4.  Na janela **Propriedades** , na caixa de texto **AlgorithmParameters** , clique em **Definir parâmetros de algoritmo**e altere os parâmetros do algoritmo, se desejar.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Filtros para modelos de mineração &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Excluir um filtro de um modelo de mineração](../../analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)  
  
  

