---
title: Substituir parâmetros do modelo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.templates.replaceparameters.f1
helpviewer_keywords:
- template parameters [Template Explorer]
- templates [Transact-SQL], replacing parameters
- Replace (Query) Template Parameters dialog box
- replacing template parameters
ms.assetid: 1234aa14-3464-4a3e-922a-5cfb8fb23627
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f6d68ec50bf711a05d7168d8bea56db9e2a0e779
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010327"
---
# <a name="replace-template-parameters"></a>Substituir Parâmetros do Modelo
  Modelos contêm parâmetros que podem ser substituídos por valores específicos de implementação cada vez que o modelo é usado. Depois de abrir um modelo em um editor de código, você pode substituir os parâmetros pelos valores relevantes à sua implementação.  
  
## <a name="before-you-begin"></a>Antes de começar  
 A caixa de diálogo **Especificar Valores para Parâmetros de Modelo** é uma grade com três colunas. As colunas **Parâmetro** e **Tipo** são somente leitura e não podem ser alteradas. Examine o conteúdo da coluna **Valor** e altere qualquer um dos padrões para valores apropriados para sua implementação.  
  
 Para usar essa caixa de diálogo, os parâmetros em seu script devem estar entre colchetes angulares (`< >`) no formato `<`*parameter_name*`,` *data_type*`,` *default_value*`>`.  
  
## <a name="replace-template-parameters"></a>Substituir Parâmetros do Modelo  
 Depois de abrir o modelo em uma janela de editor de código:  
  
1.  No menu **Consulta** , clique em **Especificar Valores para Parâmetros de Modelo**.  
  
2.  Na caixa de diálogo **Especificar Valores para Parâmetros de Modelo** , a coluna **Valores** contém um valor sugerido para cada parâmetro. Aceite o valor ou substitua-o por um novo valor.  
  
3.  Clique em **OK** para fechar a caixa de diálogo **Substituir Parâmetros do Modelo** e modificar o script no editor de consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de modelos](template-explorer.md)   
 [Abrir um modelo](open-a-template.md)  
  
  