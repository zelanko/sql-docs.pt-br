---
title: Opções (página Ambiente – Fontes e Cores)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: ea3aa222-538d-485f-99dc-01eb02cdcfea
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fac8e4cdb99d19da39f60585db3f77a27975983a
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011831"
---
# <a name="options-environment---fonts-and-colors-page"></a>Opções (página Ambiente – Fontes e Cores)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
A caixa de diálogo **Opções** permite que você determine um esquema personalizado de fontes e cores para diversos elementos da interface do usuário no [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No menu **Ferramentas** , clique em **Opções** , expanda a pasta **Ambiente** e selecione **Fontes e Cores**.  
  
As alterações no esquema de cores não são implementadas durante a sessão em que foram feitas. Você pode avaliar as alterações de cores abrindo outra instância do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e produzindo as condições sob as quais espera que suas alterações se apliquem.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
**Mostrar configurações de**  
Exibe todos os elementos da interface do usuário cujos esquemas de fonte e cor você pode alterar. Depois de selecionar um item dessa lista, você pode personalizar as configurações de cor do item selecionado em **Itens de exibição**.  
  
|Termo|Definição|  
|--------|--------------|  
|Editor de Texto|Alterações nas configurações de vídeo de estilo, tamanho, e cor da fonte no Editor de Texto afetam a aparência do texto em seu editor de texto padrão. Documentos abertos em um editor de texto fora do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] não serão afetados por essas configurações.|  
|Impressora|Alterações nas configurações de vídeo de estilo, tamanho, e cor da fonte da impressora afetam a aparência do texto impresso em documentos.<br /><br />Observação: você pode selecionar uma fonte padrão para impressão diferente daquela usada para exibição no Editor de Texto. Isso pode ser útil ao imprimir códigos que contenham caracteres de um byte e caracteres de dois bytes.|  
|[Janelas de Ferramentas Todo o Texto **]**|Alterações nas configurações de vídeo de estilo, tamanho e cor da fonte neste item afetam a aparência do texto nas janelas de ferramentas que têm painéis de saída no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Por exemplo, janela Saída, janela Resultados de Texto e assim por diante.<br /><br />Observação: alterações no texto dos itens [Janelas de Ferramentas Todo o Texto] não entram em vigor durante a sessão em que foram feitas. Você pode avaliar essas alterações abrindo outra instância do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|Janela Localizar Resultados|Alterações nas configurações de exibição de estilo, tamanho e cor da fonte deste item afetam a aparência do texto na janela Localizar Resultados.|  
|Janela de saída|Alterações nas configurações de vídeo de estilo, tamanho e cor da fonte deste item afetam a aparência do texto na janela Saída.|  
|Resultados da Grade|Alterações nas configurações de exibição de estilo, tamanho e cor da fonte desse item afetam a aparência do texto na área **Resultados da Grade** da janela Consulta.|  
|Plano de Execução|Alterações nas configurações de exibição de estilo, tamanho e cor da fonte desse item afetam a aparência do texto do Plano de Execução das consultas do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssEW](../../includes/ssew-md.md)].|  
|Resultados do Texto|Alterações nas configurações de exibição de estilo, tamanho e cor da fonte desse item afetam a aparência do texto na área **Resultados do Texto** da janela Consulta.|  
|Designers do Business Intelligence|Alterações nas configurações de exibição de estilo, tamanho e cor da fonte desse item afetam a aparência do texto na janela Designers do Business Intelligence.|  
  
**Usar Padrões**  
O botão **Usar Padrões** redefine os valores de fonte e de cor padrão do item de lista que você selecionou na lista **Mostrar configurações de** .  
  
**Fonte (em negrito indica fontes que têm largura fixa)**  
Exibe todas as fontes instaladas em seu sistema. Quando essa lista suspensa é aberta pela primeira vez, a fonte atual do elemento que você escolheu na lista **Mostrar configurações de** é selecionada. As fontes fixas, que são mais fáceis de serem alinhadas em um editor, aparecem em negrito.  
  
**Tamanho**  
Lista tamanhos de ponto disponíveis para a fonte selecionada. Alterar o tamanho da fonte afeta todas as entradas de **Itens de exibição** de uma seleção em **Mostrar configurações de** .  
  
**Itens de exibição**  
Exibe os itens cujas cores de primeiro plano e de plano de fundo você pode modificar.  
  
> [!NOTE]  
> **O**item de exibição padrão é Texto. Sendo assim, as propriedades atribuídas a Texto serão substituídas por propriedades atribuídas a outros itens de exibição. Por exemplo, se você atribuir a cor azul a **Texto** e a cor verde a Identificador, todos os identificadores serão exibidos em verde. Nesse exemplo, as propriedades do Identificador substituem as propriedades do Texto.  
  
Alguns itens de exibição incluem:  
  
-   Margem de indicador: a margem à esquerda do Editor de Códigos onde os ícones dos pontos de interrupção e de indicadores são exibidos.  
  
-   Texto recolhível: um bloco de texto ou código que pode ser inserido ou extraído da exibição no Editor de Códigos (apenas XML).  
  
**Primeiro plano do item**  
Exibe as cores disponíveis que você pode escolher para o primeiro plano do item selecionado em **Itens de exibição**. Como alguns itens estão relacionados, deve ser mantido um esquema de exibição consistente. Por exemplo, alterar a cor do primeiro plano do texto também altera a cor do primeiro plano de elementos como Cadeias de caracteres.  
  
**Custom**  
Exibe a caixa de diálogo **Cor** , em que você define uma cor personalizada para o item selecionado na lista **Itens de exibição** .  
  
> [!NOTE]  
> Sua capacidade de definir cores personalizadas pode ser limitada pelas configurações de cor de vídeo do seu computador. Por exemplo, se o seu computador estiver definido para exibir 256 cores e você selecionar uma cor personalizada na caixa de diálogo **Cor** , o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] escolherá o valor disponível mais próximo em **Cores básicas** como padrão e exibirá a cor preta na caixa de diálogo **Cor** .  
  
**Plano de fundo do item**  
Fornece uma paleta de cores na qual você pode escolher uma cor da tela de fundo para o item selecionado em **Itens de exibição**. Como alguns itens estão relacionados, deve ser mantido um esquema de exibição consistente. Por exemplo, alterar a cor do texto de plano de fundo também altera a cor de plano de fundo de elementos como Cadeias de caracteres SQL.  
  
**Custom**  
Exibe a caixa de diálogo **Cor** , em que você define uma cor personalizada para o item selecionado na lista **Itens de exibição** .  
  
**Negrito**  
Marque esta caixa de seleção para exibir o texto dos itens de exibição selecionados em negrito. Texto em negrito é mais fácil de identificar em um editor.  
  
**Amostra**  
Exibe um exemplo de estilo e tamanho de fonte e esquema de cores para valores selecionados em **Mostrar configurações de** e **Itens de exibição**. Você pode usar essa caixa de texto para visualizar os resultados à medida que experimenta opções de formatação diferentes.  
  
## <a name="see-also"></a>Consulte Também  
[Codificação de cores nos editores de códigos](../../relational-databases/scripting/color-coding-in-query-editors.md)  
[Opções (Editor de Texto/página Guia do Editor e Barra de Status)](https://msdn.microsoft.com/e4815678-7885-4631-878f-c6a2b857ee05)  
  
