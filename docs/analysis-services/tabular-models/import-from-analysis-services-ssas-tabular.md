---
title: Importar do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 625ac4fb1bf7c09aa0cfa651e105b6621e5be4b8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="import-from-analysis-services"></a>Importar do Analysis Services 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve como criar um novo projeto de modelo tabular importando os metadados de um modelo tabular existente usando a importação do modelo de projeto de servidor em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="create-a-new-model-by-importing-metadata-from-an-existing-model-in-analysis-services"></a>Criar um novo modelo com a importação de metadados de um modelo existente no Analysis Services  
 Use o modelo de projeto Importar de Servidor para criar um novo projeto de modelo tabular copiando os metadados de um modelo tabular existente em um servidor do Analysis Services. O novo projeto será criado com as mesmas conexões da fonte de dados, tabelas, relações, medidas, KPIs, funções, hierarquias, perspectivas e partições como o modelo do qual foi importado. Porém, os dados não são copiados do modelo existente para o novo espaço de trabalho modelo. Quando o processo de importação tiver sido concluído, e o novo projeto de modelo criado, você deverá executar um Processar Tudo (Atualizar Tudo) para carregar os dados das fontes de dados no novo banco de dados do espaço de trabalho do projeto do modelo.  
  
#### <a name="to-create-a-new-model-by-importing-metadata-from-an-existing-model"></a>Para criar um novo modelo com a importação de metadados de um modelo existente  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], no menu **Arquivo** , clique em **Novo**e, em seguida, em **Projeto**.  
  
2.  Na caixa de diálogo **Novo Projeto** , em **Modelos Instalados**, clique em **Business Intelligence**e clique em **Importar de Servidor**.  
  
3.  Em **Nome**, digite um nome para o projeto e especifique um local e um nome para a solução e clique em **OK**.  
  
4.  Na caixa de diálogo **Importar do Analysis Services** , em **Nome do Servidor**, especifique o nome do servidor do Analysis Services que contém os metadados modelo que você deseja importar.  
  
5.  Em **Nome do Banco de Dados**, selecione o banco de dados modelo de tabela que contém os metadados de modelo que você deseja importar e clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do projeto](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
