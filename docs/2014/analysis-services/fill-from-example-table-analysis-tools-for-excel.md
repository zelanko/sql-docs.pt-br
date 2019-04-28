---
title: Preencher com base no exemplo (ferramentas de análise de tabela para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- fill from example
ms.assetid: dac57d8f-1c65-4878-8ea0-9c680df5e4fb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f5ca47ac10549a727f284eb412ba2b35127a518
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731576"
---
# <a name="fill-from-example-table-analysis-tools-for-excel"></a>Preencher com Base no Exemplo (Ferramentas de Análise de Tabela para Excel)
  ![Botão preencher com base no exemplo nas ferramentas de análise de tabela](media/tat-fillex.gif "botão preencher com base no exemplo nas ferramentas de análise de tabela")  
  
 O **preencher do exemplo** ferramenta o ajuda a criar novas colunas de dados com base nos valores existentes.  
  
 Por exemplo, suponha que seus dados contiverem uma **Purchase Amount** coluna, um **Orders Quantity** coluna e um **Premier Customer** coluna se baseia em alguma fórmula usando o outras colunas. Se o **Premier Customer** coluna contém muitas linhas em branco, você pode usar o **Purchase Amount** e **Orders Quantity** colunas como entradas, para inferir os valores ausentes. A ferramenta analisa os padrões existentes nos dados junto com os exemplos inseridos, e faz previsões sobre a categoria a ser atribuída a cada cliente.  
  
 Caso você não esteja satisfeito com os resultados, forneça mais exemplos para defini-los.  
  
## <a name="using-the-fill-from-example-tool"></a>Usando a ferramenta Preencher com Base no Exemplo  
  
1.  No **Analyze** faixa de opções, clique em **preencher do exemplo**.  
  
2.  A ferramenta escolherá automaticamente uma coluna a ser preenchida com base na análise dos dados e você poderá aceitar ou substituir sua sugestão.  
  
3.  Crie uma coluna para os novos dados e digite exemplos dos dados que você deseja prever. Verifique se há pelo menos um exemplo de cada valor que você deseja prever. Se você estiver preenchendo dados em uma coluna existente, selecione a coluna com os valores ausentes.  
  
4.  Opcionalmente, clique em **escolher colunas a serem usadas na análise**. No **seleção de colunas avançada** caixa de diálogo, especifique as colunas que provavelmente serão úteis durante o preenchimento dos dados ausentes.  
  
     Por exemplo, se, com base na sua experiência, você souber que há um efeito causal entre uma coluna e a coluna com valores ausentes, poderá desmarcar outras colunas para obter resultados melhores.  
  
     Clique em **OK**.  
  
5.  Clique em **Executar**.  
  
     Quando a análise for concluída, a ferramenta cria um novo **padrões** planilha que contém os resultados da análise. O relatório lista as regras ou os influenciadores principais encontrados e mostra a probabilidade para cada regra.  
  
     A ferramenta também adicionará automaticamente uma coluna que contém os novos valores à tabela de dados original. Você pode examinar os valores e compará-los com o original.  
  
### <a name="requirements"></a>Requisitos  
 Somente é possível trabalhar com dados em colunas. Se a série que você deseja preencher estiver armazenada em uma linha, use a função Colar, Transpor no Excel para alterar esses dados para um formato de coluna.  
  
## <a name="understanding-the-pattern-report"></a>Entendendo o Relatório de Padrão  
 Quando você executa o **preencher do exemplo** ferramenta, é criado um relatório que fornece mais informações sobre os padrões que foram detectados. Esses padrões são usados para extrapolar novos valores de dados.  
  
 O Relatório de Padrão mostra os influenciadores principais para cada valor previsto. Cada regra ou influenciador é descrito como uma combinação de uma coluna, o valor nessa coluna e o impacto relativo da regra na previsão.  
  
 Por exemplo, se você estivesse tentando preencher uma planilha que mostrasse a distância de entrega dos pedidos, talvez esperasse logicamente que o destino tivesse um grande impacto no valor dessa distância. Nesse caso, talvez a o relatório tivesse a seguinte linha:  
  
|coluna|Valor|Favorece|Impacto relativo|  
|------------|-----------|------------|---------------------|  
|StateProvinceCode|AB|> 500 quilômetros|80%|  
  
 Isso significa que o valor AB na **StateProvinceCode** coluna prevê uma distância de entrega de > 500 quilômetros.  
  
 Em geral, as previsões se baseiam em padrões bem mais complexos do que este exemplo e o relatório pode conter muitas linhas de regras para cada previsão. Os efeitos de todas as regras são combinados para derivar o valor previsto.  
  
> [!NOTE]  
>  **Impacto relativo** é mostrado como uma barra sombreada. Quanto maior a barra, maior a probabilidade de essa regra ser uma previsão do valor preenchido.  
  
 A ferramenta também adiciona uma nova coluna à tabela de dados original, denominada \<nome da coluna > estendida.  
  
 Se a coluna de dados original contiver um valor, ele será copiado na nova coluna. No entanto, se a coluna contiver uma célula em branco, a nova coluna terá o valor previsto pelo assistente.  
  
## <a name="related-tools-and-information"></a>Ferramentas e informações relacionadas  
 Você também pode usar o [explorar dados](explore-data-sql-server-data-mining-add-ins.md) wizard, disponível no cliente de mineração de dados para Excel, para examinar a distribuição dos valores em uma coluna do Excel. Para obter mais informações, consulte [Explorando e limpando dados](exploring-and-cleaning-data.md).  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
  
