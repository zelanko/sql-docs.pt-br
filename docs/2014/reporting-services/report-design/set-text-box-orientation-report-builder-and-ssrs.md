---
title: Definir a orientação da caixa de texto (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 64bd53f4-2f31-4732-8c2e-64c7b54b6972
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: cc2ef22253eaef7c86eeee43ed0260d24d3adfe4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122570"
---
# <a name="set-text-box-orientation-report-builder-and-ssrs"></a>Definir a orientação da caixa de texto (Construtor de Relatórios e SSRS)
  Uma caixa de texto pode ser orientada em direções diferentes: horizontalmente, verticalmente (texto lido de cima para baixo) ou girado 270 graus (texto lido de baixo para cima). Como a orientação é definida na caixa de texto, não no texto, ela se aplica a todo o texto na caixa de texto. Você não pode especificar orientações diferentes para partes do texto. Dimensione manualmente a largura da coluna e a altura da linha para acomodar o texto girado.  
  
 A propriedade WritingMode, que é usada para especificar a orientação do texto, não está disponível na **propriedades da caixa de texto** caixa de diálogo. Abra o painel Propriedades e defina a propriedade. Os valores disponíveis para a propriedade WritingMode **Horizontal** (leitura de texto da esquerda para a direita), **Vertical** (texto lido de cima para baixo), **Rotate270** (leitura de texto baixo para cima). Você deve dimensionar manualmente a largura da coluna e a altura da linha para acomodar o texto.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-text-orientation"></a>Para definir a orientação do texto  
  
1.  Crie um novo relatório ou abra um relatório existente.  
  
2.  Se o painel Propriedades não estiver aberto, clique na guia **Exibir** e marque a caixa de seleção **Propriedades** .  
  
3.  Clique na caixa de texto para a qual você deseja alterar a orientação do texto.  
  
4.  Localize o WritingMode propriedade no painel Propriedades e na lista suspensa Selecionar a orientação do texto para aplicar à caixa de texto.  
  
    > [!NOTE]  
    >  Quando as propriedades no painel Propriedades estiverem organizadas em categorias, WritingMode estará na categoria **Localização** .  
  
5.  Na caixa de listagem, selecione **Horizontal**, **Vertical**ou **Rotate270**.  
  
## <a name="see-also"></a>Consulte também  
 [Caixas de texto &#40;SSRS e construtor de relatórios&#41;](text-boxes-report-builder-and-ssrs.md)   
 [Tutorial: Formatar texto &#40;Construtor de Relatórios&#41;](../tutorial-format-text-report-builder.md)  
  
  