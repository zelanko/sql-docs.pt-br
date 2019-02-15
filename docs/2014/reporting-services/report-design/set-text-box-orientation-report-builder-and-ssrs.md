---
title: Definir a orientação da caixa de texto (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 64bd53f4-2f31-4732-8c2e-64c7b54b6972
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3e8beb8a7aa6eec3e62a45b9c3d3a8566f93b540
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56296814"
---
# <a name="set-text-box-orientation-report-builder-and-ssrs"></a>Definir a orientação da caixa de texto (Construtor de Relatórios e SSRS)
  Uma caixa de texto pode ser orientada em direções diferentes: horizontalmente, verticalmente (texto lido de cima para baixo) ou girado 270 graus (texto lido de baixo para cima). Como a orientação é definida na caixa de texto, não no texto, ela se aplica a todo o texto na caixa de texto. Você não pode especificar orientações diferentes para partes do texto. Dimensione manualmente a largura da coluna e a altura da linha para acomodar o texto girado.  
  
 A propriedade WritingMode, que você usa para especificar a orientação do texto, não está disponível na **propriedades da caixa de texto** caixa de diálogo. Abra o painel Propriedades e defina a propriedade. São os valores disponíveis para a propriedade WritingMode **Horizontal** (texto lido da esquerda para a direita), **Vertical** (texto lido de cima para baixo), **Rotate270** (texto lido baixo para cima). Você deve dimensionar manualmente a largura da coluna e a altura da linha para acomodar o texto.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-text-orientation"></a>Para definir a orientação do texto  
  
1.  Crie um novo relatório ou abra um relatório existente.  
  
2.  Se o painel Propriedades não estiver aberto, clique na guia **Exibir** e marque a caixa de seleção **Propriedades** .  
  
3.  Clique na caixa de texto para a qual você deseja alterar a orientação do texto.  
  
4.  Localize a propriedade no painel Propriedades e na lista suspensa Selecionar a orientação do texto a ser aplicado à caixa de texto WritingMode.  
  
    > [!NOTE]  
    >  Quando as propriedades no painel Propriedades estiverem organizadas em categorias, WritingMode estará na categoria **Localização** .  
  
5.  Na caixa de listagem, selecione **Horizontal**, **Vertical**ou **Rotate270**.  
  
## <a name="see-also"></a>Consulte também  
 [Caixas de texto &#40;Construtor de Relatórios e SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [Tutorial: Formatar o texto &#40;construtor de relatórios&#41;](../tutorial-format-text-report-builder.md)  
  
  
