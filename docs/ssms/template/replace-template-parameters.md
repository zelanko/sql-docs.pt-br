---
title: Substituir Parâmetros do Modelo
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.templates.replaceparameters.f1
helpviewer_keywords:
- template parameters [Template Explorer]
- templates [Transact-SQL], replacing parameters
- Replace (Query) Template Parameters dialog box
- replacing template parameters
ms.assetid: 1234aa14-3464-4a3e-922a-5cfb8fb23627
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b0c4cc26fddff13e388b74593aa9d8f9331359f8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245675"
---
# <a name="replace-template-parameters"></a>Substituir Parâmetros do Modelo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Modelos contêm parâmetros que podem ser substituídos por valores específicos de implementação cada vez que o modelo é usado. Depois de abrir um modelo em um editor de código, você pode substituir os parâmetros pelos valores relevantes à sua implementação.  
  
## <a name="before-you-begin"></a>Antes de começar  
A caixa de diálogo **Especificar Valores para Parâmetros de Modelo** é uma grade com três colunas. As colunas **Parâmetro** e **Tipo** são somente leitura e não podem ser alteradas. Examine o conteúdo da coluna **Valor** e altere qualquer um dos padrões para valores apropriados para sua implementação.  
  
Para usar essa caixa de diálogo, os parâmetros em seu script devem estar entre colchetes angulares (`< >`) no formato `<`*parameter_name*`,` *data_type*`,` *default_value*`>`.  
  
## <a name="replace-template-parameters"></a>Substituir Parâmetros do Modelo  
Depois de abrir o modelo em uma janela de editor de código:  
  
1.  No menu **Consulta** , clique em **Especificar Valores para Parâmetros de Modelo**.  
  
2.  Na caixa de diálogo **Especificar Valores para Parâmetros de Modelo** , a coluna **Valores** contém um valor sugerido para cada parâmetro. Aceite o valor ou substitua-o por um novo valor.  
  
3.  Clique em **OK** para fechar a caixa de diálogo **Substituir Parâmetros do Modelo** e modificar o script no editor de consulta.  
  
## <a name="see-also"></a>Consulte Também  
[Explorador de Modelos](../../ssms/template/template-explorer.md)  
[Abrir um modelo](../../ssms/template/open-a-template.md)  
  
