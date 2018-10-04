---
title: Avisos (Designer de banco de dados) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.databasedesigner.warnings.f1
ms.assetid: 13f58b4d-f345-4fbc-ae2d-b3c8290a797d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d83620c0c6463bd6e752f65a97b2fb14e1d1c03f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074376"
---
# <a name="warnings-database-designer-analysis-services---multidimensional-data"></a>Avisos (Designer de Banco de Dados) (Analysis Services - Dados multidimensionais)
  Use a guia **Avisos** para exibir e ignorar regras globalmente e para exibir e reabilitar instâncias específicas de avisos ignorados. A guia **Avisos** exibe duas grades: **Regras de Aviso de Design** e **Avisos Ignorados**.  
  
 **Para exibir a guia avisos**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , clique em **Editar Banco de Dados**e então clique na guia **Avisos** .  
  
## <a name="design-warning-rules-grid"></a>Grade de Regras de Aviso de Design  
 A grade de **Regras de Aviso de Design** exibe todas as regras de aviso de design. Esta grade também controla as regras que são habilitadas para o banco de dados. Para habilitar ou desabilitar uma regra de aviso, selecione ou desmarque sua caixa de seleção.  
  
 A grade **Regras de Aviso de Design** tem as seguintes colunas:  
  
 **Descrição**  
 Exibe o nome da regra. As regras são agrupadas por categoria.  
  
 **Importância**  
 Exibe a importância atribuída à regra.  
  
 **Comentários**  
 (Opcional) Permite ao usuário digitar um comentário que explica por que você está ignorando o aviso.  
  
## <a name="dismissed-warnings-grid"></a>Grade Avisos Ignorados  
 A grade **Avisos Ignorados** exibe todas as ocorrências de avisos específicos que foram ignorados na **Lista de Erros**. Para reabilitar um aviso, selecione-o na grade e clique em **Reabilitar**.  
  
 A grade **Avisos Ignorados** tem o seguinte conteúdo:  
  
 **Objeto**  
 Exibe um ícone que representa o tipo de objeto e o nome do objeto.  
  
 **Tipo**  
 Exibe o tipo de objeto.  
  
 **Descrição**  
 Exibe o nome da regra.  
  
 **Importância**  
 Exibe a importância atribuída à regra.  
  
 **Comentários**  
 Exibe o comentário que foi digitado quando o aviso foi ignorado. Você pode adicionar ou modificar um comentário aqui.  
  
 **Habilitar novamente**  
 Reabilita os avisos selecionados.  
  
> [!NOTE]  
>  Se um objeto tiver um aviso, mas o objeto estiver em um estado inválido ou tiver sido manualmente removido do projeto, um ícone de erro aparecerá próximo ao aviso na lista. Para ignorar o aviso, selecione-o e clique em **Reabilitar**.  
  
## <a name="see-also"></a>Consulte também  
 [Ignorar a caixa de diálogo de aviso &#40;Analysis Services - dados multidimensionais&#41;](dismiss-warning-dialog-box-analysis-services-multidimensional-data.md)   
 [Geral &#40;Designer de banco de dados&#41; &#40;Analysis Services - dados multidimensionais&#41;](general-database-designer-analysis-services-multidimensional-data.md)  
  
  
