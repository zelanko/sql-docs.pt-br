---
title: Configurar propriedades de comportamento de tabela para relatórios de Power View (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.tablebehavior.f1
ms.assetid: 1386aae0-1d73-4a50-9c69-ae12405d855c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f6ade5a39c974af7a87bb33aab6da490e0c3ae0e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66066835"
---
# <a name="configure-table-behavior-properties-for-power-view-reports-ssas-tabular"></a>Configurar propriedades de comportamento de tabela para relatórios de Power View (SSAS tabular)
  Se você estiver usando um modelo de tabela como um modelo de dados para o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], poderá definir propriedades de comportamento de tabela que exponham linhas de detalhes em um mais nível granular. Definir as propriedades do comportamento da tabela altera o comportamento do agrupamento das linhas de detalhes e produz uma melhor colocação padrão de identificação de informações (como nomes, IDs de fotografia ou imagens de logotipo) em layouts de peça, cartão e gráfico.  
  
 
  [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] difere de outros aplicativos de relatório porque agrupará itens automaticamente durante o design do relatório, avaliando quais colunas colocou você na lista de campos de relatório em relação ao formato de apresentação que você está usando. Na maioria dos casos, o agrupamento padrão gera um resultado ótimo. Mas, para algumas tabelas, principalmente as que contêm dados de detalhes, o comportamento de agrupamento padrão às vezes agrupará linhas que não deveriam ser agrupadas. Para essas tabelas, você pode definir propriedades que alteram como os grupos são avaliados.  
  
 Definir propriedades de comportamento de tabela é recomendado para tabelas onde as linhas individuais são de interesse primário, como registros de funcionário ou cliente. Em contraste, as tabelas que não se beneficiam destas propriedades incluem as que agem como uma tabela de pesquisa (por exemplo, uma tabela de data, uma tabela de categoria de produto ou uma tabela de departamento, onde a tabela consiste em um número relativamente pequeno de linhas e colunas) ou tabelas resumidas que contêm linhas que só são interessantes quando resumidas (por exemplo, dados de censo que acumulam por gênero, idade ou geografia). Para tabelas de pesquisa e resumo, o comportamento do agrupamento padrão gera o melhor resultado.  
  
> [!NOTE]  
>  As propriedades de comportamento de tabela só afetam modelos de tabela usados como modelos de dados no [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. As propriedades do comportamento de tabela não têm suporte em relatórios dinâmicos do Excel.  
  
 As propriedades do comportamento de tabela incluem o seguinte:  
  
-   **Identificador de linha** ─ especifica uma coluna que contém apenas valores exclusivos, permitindo que essa coluna seja usada como uma chave de agrupamento interna.  
  
-   **Manter linhas exclusivas** ─ especifica quais colunas fornecem valores que devem ser tratados como exclusivos mesmo se forem duplicatas (por exemplo, nome do funcionário e sobrenome, para casos em que dois ou mais funcionários compartilham o mesmo nome).  
  
-   **Rótulo padrão** : especifica qual coluna fornece um nome de exibição para representar os dados da linha (por exemplo, nome do funcionário em um registro de funcionário).  
  
-   **Imagem padrão** : especifica qual coluna fornece uma imagem que representa os dados da linha (por exemplo, uma ID de foto em um registro de funcionário).  
  
> [!NOTE]  
>  Veja a seção a seguir para obter otimizações de layout do ponto de vista de um formato de apresentação específico:  [Otimizando para layouts específicos](#bkmk_optimizeforlayout).  
  
## <a name="opening-the-table-behavior-dialog-box"></a>Abrindo a caixa de diálogo de Comportamento da Tabela  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique na tabela (guia) para a qual você está configurando uma lista de campos padrão.  
  
2.  Na janela **Propriedades** , na propriedade **Comportamento da Tabela** , clique em **Clicar para editar**.  
  
3.  Na caixa de diálogo **Comportamento da Tabela** , defina o **Identificador de Linha**e especifique outras propriedades nesta caixa de diálogo.  
  
## <a name="setting-the-row-identifier-property"></a>Definindo a propriedade Identificador de Linha  
 Dentro da tabela, o identificador de linha especifica uma única coluna que só contém valores exclusivos e nenhum valor em branco. A propriedade identificador de linha é usada para alterar o agrupamento para que um grupo não seja baseado na composição de campo de uma linha, mas em uma coluna fixa que é sempre usada para identificar exclusivamente uma linha, independentemente dos campos usados em um layout de relatório específico.  
  
 Definir esta propriedade altera o comportamento de agrupamento padrão de agrupamento dinâmico baseado nas colunas presentes na tela, para um comportamento de agrupamento fixo que é resumido com base no identificador de linha. Alterar o comportamento do agrupamento padrão é pertinente para layouts de relatório, como uma matriz, que, de outro modo, agruparia (ou mostraria subtotais) para cada coluna na linha.  
  
 No [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], definir um identificador de linha habilita as seguintes propriedades adicionais: **Manter Linhas Exclusivas** , **Rótulo Padrão** e **Imagem Padrão** .  
  
 Você também pode usar **Identificador de Linha** sozinho, como uma propriedade autônoma, para habilitar o seguinte:  
  
-   Uso de imagens binárias em um relatório. Ao remover a ambiguidade em torno da exclusividade de linha, o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] pode determinar como atribuir imagens padrão e rótulos padrão para uma determinada linha.  
  
-   Remover subtotais indesejáveis de um relatório de matriz. O agrupamento padrão no nível do campo cria um subtotal para cada campo. Se você desejar somente um único subtotal que seja calculado no nível de linha, definir o Identificador de Linha gerará este resultado.  
  
 Você não pode definir um Identificador de Linha para tabelas marcadas como tabelas de data. Para tabelas de data, o identificador de linha é especificado quando você marca a tabela. Para obter mais informações, consulte [Caixa de diálogo Marcar Como Tabela de Data &#40;SSAS&#41;](../mark-as-date-table-dialog-box-ssas.md).  
  
## <a name="setting-the-keep-unique-rows-property"></a>Definindo a propriedade Manter Linhas Exclusivas  
 Esta propriedade permite especificar quais colunas transmitem informações de identidade (como um nome de funcionário ou um código de produto) de modo que possa distinguir uma linha da outra. Nos casos em que as linhas parecem idênticas (como dois clientes com o mesmo nome), as colunas que você especificar para esta propriedade serão repetidas na tabela de relatório.  
  
 Dependendo das colunas que acrescentar a um relatório, você poderá localizar as linhas que são tratadas como linhas idênticas porque os valores em cada uma delas parecem ser iguais (por exemplo, dois clientes chamados Jon Yang). Isto pode ocorrer porque outras colunas que fornecem diferenciação (como nome do meio, endereço ou data de aniversário) não estão na tela do relatório. Nesse tipo de cenário, o comportamento padrão é agrupar as linhas aparentemente idênticas em uma única linha, resumindo os valores calculados em um único resultado maior das linhas combinadas.  
  
 Ao definir a propriedade **Manter Linhas Exclusivas** , você pode designar uma ou mais colunas que sempre devem se repetir, mesmo se houver instâncias duplicadas, sempre que acrescentar essa coluna à tela de relatório. Valores calculados associados à linha agora serão alocados com base em cada linha individual em vez de acumulados em uma única linha. Ao escolher colunas para a propriedade  **Manter Linhas Exclusivas** , escolha as que contiverem valores exclusivos ou quase exclusivos.  
  
> [!NOTE]  
>  Como as colunas que o usuário final seleciona podem afetar o agrupamento, o que altera o contexto de filtro para cálculos de expressão, os designers de modelo devem procurar criar medidas que retornem os resultados corretos. Para obter mais informações, consulte [Perguntas frequentes do Power View](https://go.microsoft.com/fwlink/?LinkId=220674).  
  
## <a name="setting-a-default-label"></a>Definindo um rótulo padrão  
 Esta propriedade especifica um rótulo que aparece na tira de navegação de um relatório de peças. Quando usado com uma imagem padrão, o rótulo padrão aparece abaixo da imagem. Sem uma imagem, o rótulo padrão aparece sozinho. Ao escolher um rótulo padrão, escolha a coluna que transmite a maioria das informações sobre a linha (por exemplo, um nome).  
  
 Em um layout lado a lado, o rótulo padrão aparece na área de título abaixo de uma imagem, conforme definido pela propriedade Imagem Padrão. Por exemplo, se você tiver uma lista de funcionários, poderá organizar as informações de funcionários, usando a ID de foto deles como a imagem padrão e o Nome de Funcionário como o rótulo padrão. Em uma peça, o rótulo padrão aparece abaixo da imagem padrão. Estas colunas sempre aparecem no quadro, mesmo que você não as selecione explicitamente na lista de campos de relatório.  
  
## <a name="setting-a-default-image"></a>Definindo uma imagem padrão  
 Esta propriedade especifica uma imagem que aparece na tira de navegação de um relatório de peças ou na frente de um cartão. No relatório, quando você seleciona a coluna que contém a imagem padrão, ela será colocada na tira de navegação de um layout de relatório de peças, ou na frente de um cartão. Uma imagem padrão deve ser conteúdo visual. Exemplos incluem uma ID de foto na tabela de funcionários, um logotipo de cliente em uma tabela de cliente, ou uma forma de país em uma tabela de geografia.  
  
> [!NOTE]  
>  As imagens podem se obtidas de endereços de URL para um arquivo de imagem em um servidor Web, ou como dados binários inseridos na pasta de trabalho Se a imagem for baseada em uma URL, defina também a coluna como um tipo de imagem de forma que o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] recupere a imagem em vez de exibir a URL como dados de texto no relatório.  
  
##  <a name="bkmk_optimizeforlayout"></a>Otimizando para layouts específicos  
 Esta seção descreve o efeito de definir propriedades de comportamento de tabela do ponto de vista de um formato de apresentação específico e características dos dados. Se você estiver tentando ajustar o layout de um relatório de matriz, por exemplo, poderá usar estas informações para entender como melhorar uma apresentação de matriz usando as propriedades de comportamento de tabela no modelo.  
  
### <a name="images-are-missing"></a>Imagens faltando  
 As propriedades que você define no modelo determinam se as imagens são visualizadas em um relatório, ou representadas como valores de texto no relatório.  
  
 ![URLs de imagem aparecem como texto em um relatório](../media/ssas-rptprop-noimageurl.gif "URLs de imagem aparecem como texto em um relatório")  
  
 Por padrão, o texto no modelo é interpretado como texto no relatório. Se uma coluna de texto for um endereço de URL para uma imagem de relatório, lembre-se de definir a propriedade **Image URL** para que o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] recupere o arquivo de imagem. Para imagens binárias, lembre-se de definir a propriedade **Identificador de Linha** .  
  
### <a name="tables-are-missing-one-or-more-rows"></a>Estão faltando uma ou mais linhas nas tabelas  
 Às vezes, os resultados de comportamento de agrupamento padrão são o oposto do que você pretendeu; especificamente, as linhas de detalhes que estão presentes no modelo não aparecem no relatório. Por padrão, o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] agrupa nas colunas que você adiciona à tela. Se você adicionar **Nome de País** ao relatório, cada país aparecerá uma vez na tela, embora a tabela subjacente possa conter milhares de linhas que incluam várias instâncias de cada nome de país. Neste caso, o comportamento de agrupamento padrão gera o resultado correto.  
  
 Porém, considere um exemplo diferente em que você possa querer que apareçam várias instâncias de uma linha, porque, na realidade, as linhas subjacentes contêm dados sobre entidades diferentes. Nesse exemplo, suponha que você tenha dois clientes chamados **Davi Barros**. Usando o comportamento de agrupamento padrão, somente uma instância de **Davi Barros** aparecerá no relatório. Além disso, como somente uma instância aparece na lista, a medida **Renda Anual** é a soma daquele valor para ambos os clientes.  
  
 ![O grupo padrão consolida 2 em 1](../media/ssas-jonyang-norowid.gif "O grupo padrão consolida 2 em 1")  
  
 Para alterar o comportamento de agrupamento padrão, defina as propriedades **Identificador de Linha** e **Manter Linhas Exclusivas** . Em **Manter Linhas Exclusivas**, escolha a coluna Sobrenome para que este valor seja repetido para uma linha, mesmo que já apareça em uma linha diferente. Depois de alterar as propriedades e republicar a pasta de trabalho, você pode criar o mesmo relatório, só que, desta vez, verá os dois clientes chamados **Davi Barros**, com a **Renda Anual** corretamente alocada para cada um.  
  
 ![Dados de linha contendo duplicatas baseadas na ID da linha](../media/ssas-jonyang.gif "Dados de linha contendo duplicatas baseadas na ID da linha")  
  
### <a name="matrix-layout-is-too-crowded"></a>O layout de matriz está cheio demais  
 Quando você apresenta uma tabela de detalhes em uma matriz, o agrupamento padrão fornece um valor resumido para cada coluna. Dependendo de seus objetivos, podem ser mais resumos do que você deseja. Para alterar este comportamento, defina **Identificador de Linha**. Nenhuma propriedade adicional precisa ser definida; apenas definir o identificador de linha é suficiente para alterar o agrupamento de forma que os resumos sejam calculados para cada linha com base em seu identificador de linha exclusivo.  
  
 Compare as seguintes imagens de antes e depois que mostram o efeito de definir esta propriedade para um layout de matriz.  
  
 **Antes: agrupamento padrão com base em campos na matriz**  
  
 ![Layout de matriz agrupado em identificador de linha](../media/ssas-rptprop-matrixrowid.gif "Layout de matriz agrupado em identificador de linha")  
  
 **Após: agrupamento no identificador de linha**  
  
 ![Layout de matriz agrupado em identificador de linha](../media/ssas-rptprop-matrixrowid.gif "Layout de matriz agrupado em identificador de linha")  
  
### <a name="chart-showing-too-many-items-and-levels-on-the-axis"></a>Gráfico mostrando itens e níveis demais no eixo  
 Relatórios de gráfico que mostram dados de detalhes devem usar o identificador de linha como um eixo. Sem um identificador de linha, o eixo é indeterminado, resultando em um layout aproximado que pode não fazer sentido. Para alterar este comportamento, defina **Identificador de Linha**. Nenhuma propriedade adicional precisa ser definida; apenas definir o identificador de linha é suficiente para alterar o agrupamento de forma que os resumos sejam calculados para cada linha com base em seu identificador de linha exclusivo.  
  
 Compare as seguintes imagens de antes e depois que mostram o efeito de definir esta propriedade para um layout de gráfico. É o mesmo relatório, com campos e apresentação idênticos. A única diferença é que a imagem inferior mostra um relatório depois que **Identificador de Linha** foi definido na tabela de Itens.  
  
 **Antes: agrupamento padrão com base em campos em um gráfico**  
  
 ![Gráfico baseado em agrupamento padrão em nível de campo](../media/ssas-rptprop-chartfieldgroup.gif "Gráfico baseado em agrupamento padrão em nível de campo")  
  
 **Após: agrupamento no identificador de linha (o identificador de linha se torna o eixo)**  
  
 ![Gráfico baseado em agrupamento de IDs de linha](../media/ssas-rptprop-chartrowid.gif "Gráfico baseado em agrupamento de IDs de linha")  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de avaliar as tabelas em seu modelo e definir as propriedades de comportamento da tabela nelas contendo linhas de detalhes que sempre devem aparecer como itens individuais, você poderá otimizar ainda mais o modelo por meio de propriedades ou configurações adicionais.  
  
  
