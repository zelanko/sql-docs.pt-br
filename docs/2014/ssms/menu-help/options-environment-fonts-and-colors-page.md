---
title: 'Opções (página ambiente: fontes e cores) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: ea3aa222-538d-485f-99dc-01eb02cdcfea
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 40bd2c5735b68a165bcdff4a26069505994dbd85
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211255"
---
# <a name="options-environment-fonts-and-colors-page"></a>Opções (Ambiente: página Fontes e Cores)
  A caixa de diálogo **Opções** permite estabelecer uma fonte personalizada e um esquema de cores para vários elementos da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]interface do usuário no. No menu **Ferramentas** , clique em **Opções** , expanda a pasta **Ambiente** e selecione **Fontes e Cores**.  
  
 As alterações no esquema de cores não são implementadas durante a sessão em que foram feitas. Você pode avaliar as alterações de cores abrindo outra instância do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e produzindo as condições sob as quais espera que suas alterações se apliquem.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Mostrar configurações para**  
 Exibe todos os elementos da interface do usuário cujos esquemas de fonte e cor você pode alterar. Depois de selecionar um item dessa lista, você pode personalizar as configurações de cor do item selecionado em **Itens de exibição**.  
  
|Termo|Definição|  
|----------|----------------|  
|Editor de Texto|Alterações nas configurações de vídeo de estilo, tamanho, e cor da fonte no Editor de Texto afetam a aparência do texto em seu editor de texto padrão. Documentos abertos em um editor de texto fora do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] não serão afetados por essas configurações.|  
|Impressora|Alterações nas configurações de vídeo de estilo, tamanho, e cor da fonte da impressora afetam a aparência do texto impresso em documentos.<br /><br /> Dica: conforme necessário, você pode selecionar uma fonte padrão diferente para impressão do que a usada para exibição no editor de texto. Isso pode ser útil ao imprimir códigos que contenham caracteres de um byte e caracteres de dois bytes.|  
|[Janelas de Ferramentas Todo o Texto **]**|Alterações nas configurações de vídeo de estilo, tamanho e cor da fonte neste item afetam a aparência do texto nas janelas de ferramentas que têm painéis de saída no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Por exemplo, janela Saída, janela Resultados de Texto e assim por diante.<br /><br /> Observação: alterações no texto dos itens [Janelas de Ferramentas Todo o Texto] não entram em vigor durante a sessão em que foram feitas. Você pode avaliar essas alterações abrindo outra instância do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|Janela Localizar Resultados|Alterações nas configurações de exibição de estilo, tamanho e cor da fonte deste item afetam a aparência do texto na janela Localizar Resultados.|  
|Janela de saída|Alterações nas configurações de vídeo de estilo, tamanho e cor da fonte deste item afetam a aparência do texto na janela Saída.|  
|Resultados da Grade|Alterações nas configurações de exibição de estilo, tamanho e cor da fonte desse item afetam a aparência do texto na área **Resultados da Grade** da janela Consulta.|  
|Plano de Execução|Alterações nas configurações de exibição de estilo, tamanho e cor da fonte desse item afetam a aparência do texto no plano de execução [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de [!INCLUDE[ssEW](../../includes/ssew-md.md)] consultas e.|  
|Resultados do Texto|Alterações nas configurações de exibição de estilo, tamanho e cor da fonte desse item afetam a aparência do texto na área **Resultados do Texto** da janela Consulta.|  
|Designers do Business Intelligence|Alterações nas configurações de exibição de estilo, tamanho e cor da fonte desse item afetam a aparência do texto na janela Designers do Business Intelligence.|  
  
 **Usar padrões**  
 O botão **Usar Padrões** redefine os valores de fonte e de cor padrão do item de lista que você selecionou na lista **Mostrar configurações de** .  
  
 **Font (negrito indica fontes de largura fixa)**  
 Exibe todas as fontes instaladas em seu sistema. Quando essa lista suspensa é aberta pela primeira vez, a fonte atual do elemento que você escolheu na lista **Mostrar configurações de** é selecionada. As fontes fixas, que são mais fáceis de serem alinhadas em um editor, aparecem em negrito.  
  
 **Tamanho**  
 Lista tamanhos de ponto disponíveis para a fonte selecionada. Alterar o tamanho da fonte afeta todas as entradas de **Itens de exibição** de uma seleção em **Mostrar configurações de** .  
  
 **Exibir itens**  
 Exibe os itens cujas cores de primeiro plano e de plano de fundo você pode modificar.  
  
> [!NOTE]  
>  Oitem de exibição padrão é Texto. Sendo assim, as propriedades atribuídas a Texto serão substituídas por propriedades atribuídas a outros itens de exibição. Por exemplo, se você atribuir a cor azul a **Texto** e a cor verde a Identificador, todos os identificadores serão exibidos em verde. Nesse exemplo, as propriedades do Identificador substituem as propriedades do Texto.  
  
 Alguns itens de exibição incluem:  
  
-   Margem de indicador: a margem à esquerda do Editor de Códigos onde os ícones dos pontos de interrupção e de indicadores são exibidos.  
  
-   Texto recolhível: um bloco de texto ou código que pode ser inserido ou extraído da exibição no Editor de Códigos (apenas XML).  
  
 **Primeiro plano do item**  
 Exibe as cores disponíveis que você pode escolher para o primeiro plano do item selecionado em **Itens de exibição**. Como alguns itens estão relacionados, deve ser mantido um esquema de exibição consistente. Por exemplo, alterar a cor do primeiro plano do texto também altera a cor do primeiro plano de elementos como Cadeias de caracteres.  
  
 **Custom**  
 Exibe a caixa de diálogo **Cor** , em que você define uma cor personalizada para o item selecionado na lista **Itens de exibição** .  
  
> [!NOTE]  
>  Sua capacidade de definir cores personalizadas pode ser limitada pelas configurações de cor de vídeo do seu computador. Por exemplo, se o seu computador estiver definido para exibir 256 cores e você selecionar uma cor personalizada na caixa de diálogo **Cor** , o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] escolherá o valor disponível mais próximo em **Cores básicas** como padrão e exibirá a cor preta na caixa de diálogo **Cor** .  
  
 **Plano de fundo do item**  
 Fornece uma paleta de cores na qual você pode escolher uma cor da tela de fundo para o item selecionado em **Itens de exibição**. Como alguns itens estão relacionados, deve ser mantido um esquema de exibição consistente. Por exemplo, alterar a cor do texto de plano de fundo também altera a cor de plano de fundo de elementos como Cadeias de caracteres SQL.  
  
 **Custom**  
 Exibe a caixa de diálogo **Cor** , em que você define uma cor personalizada para o item selecionado na lista **Itens de exibição** .  
  
 **Aplique**  
 Marque esta caixa de seleção para exibir o texto dos itens de exibição selecionados em negrito. Texto em negrito é mais fácil de identificar em um editor.  
  
 **Amostra**  
 Exibe um exemplo de estilo e tamanho de fonte e esquema de cores para valores selecionados em **Mostrar configurações de** e **Itens de exibição**. Você pode usar essa caixa de texto para visualizar os resultados à medida que experimenta opções de formatação diferentes.  
  
## <a name="see-also"></a>Consulte Também  
 [Codificação por cores em editores de consulta](../../relational-databases/scripting/color-coding-in-query-editors.md)   
 [Opções &#40;editor de texto: guia Editor e página barra de status&#41;](../../database-engine/options-text-editor-editor-tab-and-status-bar-page.md)  
  
  
