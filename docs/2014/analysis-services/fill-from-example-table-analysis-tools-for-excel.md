---
title: Preenchimento de exemplo (ferramentas de análise de tabela para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- fill from example
ms.assetid: dac57d8f-1c65-4878-8ea0-9c680df5e4fb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d1e09e439469f23412c84ea7bab65c0aa748f286
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081311"
---
# <a name="fill-from-example-table-analysis-tools-for-excel"></a>Preencher com Base no Exemplo (Ferramentas de Análise de Tabela para Excel)
  ![Botão Preencher com Base no Exemplo em Ferramentas de Análise de Tabela](media/tat-fillex.gif "Botão Preencher com Base no Exemplo em Ferramentas de Análise de Tabela")  
  
 A ferramenta **preencher com exemplo** ajuda a criar novas colunas de dados com base em valores existentes.  
  
 Por exemplo, suponha que seus dados contenham uma coluna de **valor de compra** , uma coluna de **quantidade de pedidos** e uma coluna de **cliente Premier** com base em alguma fórmula usando as outras colunas. Se a coluna **cliente Premier** contiver muitas linhas em branco, você poderá usar as colunas **quantidade de compra** e quantidade de **pedidos** como as entradas para inferir os valores ausentes. A ferramenta analisa os padrões existentes nos dados junto com os exemplos inseridos, e faz previsões sobre a categoria a ser atribuída a cada cliente.  
  
 Caso você não esteja satisfeito com os resultados, forneça mais exemplos para defini-los.  
  
## <a name="using-the-fill-from-example-tool"></a>Usando a ferramenta Preencher com Base no Exemplo  
  
1.  Na faixa de faixas **analisar** , clique em **preencher com base em exemplo**.  
  
2.  A ferramenta escolherá automaticamente uma coluna a ser preenchida com base na análise dos dados e você poderá aceitar ou substituir sua sugestão.  
  
3.  Crie uma coluna para os novos dados e digite exemplos dos dados que você deseja prever. Verifique se há pelo menos um exemplo de cada valor que você deseja prever. Se você estiver preenchendo dados em uma coluna existente, selecione a coluna com os valores ausentes.  
  
4.  Opcionalmente, clique em **escolher colunas a serem usadas na análise**. Na caixa de diálogo **seleção de colunas avançadas** , especifique as colunas que são mais prováveis de serem úteis ao preencher os dados ausentes.  
  
     Por exemplo, se, com base na sua experiência, você souber que há um efeito causal entre uma coluna e a coluna com valores ausentes, poderá desmarcar outras colunas para obter resultados melhores.  
  
     Clique em **OK**.  
  
5.  Clique em **Executar**.  
  
     Quando a análise é concluída, a ferramenta cria uma nova planilha de **padrões** que contém os resultados da análise. O relatório lista as regras ou os influenciadores principais encontrados e mostra a probabilidade para cada regra.  
  
     A ferramenta também adicionará automaticamente uma coluna que contém os novos valores à tabela de dados original. Você pode examinar os valores e compará-los com o original.  
  
### <a name="requirements"></a>Requisitos  
 Somente é possível trabalhar com dados em colunas. Se a série que você deseja preencher estiver armazenada em uma linha, use a função Colar, Transpor no Excel para alterar esses dados para um formato de coluna.  
  
## <a name="understanding-the-pattern-report"></a>Entendendo o Relatório de Padrão  
 Quando você executa a ferramenta **preencher com exemplo** , é criado um relatório que fornece mais informações sobre os padrões detectados. Esses padrões são usados para extrapolar novos valores de dados.  
  
 O Relatório de Padrão mostra os influenciadores principais para cada valor previsto. Cada regra ou influenciador é descrito como uma combinação de uma coluna, o valor nessa coluna e o impacto relativo da regra na previsão.  
  
 Por exemplo, se você estivesse tentando preencher uma planilha que mostrasse a distância de entrega dos pedidos, talvez esperasse logicamente que o destino tivesse um grande impacto no valor dessa distância. Nesse caso, talvez a o relatório tivesse a seguinte linha:  
  
|Coluna|Valor|Favorece|Impacto relativo|  
|------------|-----------|------------|---------------------|  
|StateProvinceCode|AB|>de 500 quilômetros|80%|  
  
 Isso significa que o valor AB na coluna **StateProvinceCode** prevê rigidamente uma distância de remessa de >de 500 quilômetros.  
  
 Em geral, as previsões se baseiam em padrões bem mais complexos do que este exemplo e o relatório pode conter muitas linhas de regras para cada previsão. Os efeitos de todas as regras são combinados para derivar o valor previsto.  
  
> [!NOTE]  
>  O **impacto relativo** é mostrado como uma barra sombreada. Quanto maior a barra, maior a probabilidade de essa regra ser uma previsão do valor preenchido.  
  
 A ferramenta também adiciona uma nova coluna à tabela de dados original, denominada \<nome da coluna> estendida.  
  
 Se a coluna de dados original contiver um valor, ele será copiado na nova coluna. No entanto, se a coluna contiver uma célula em branco, a nova coluna terá o valor previsto pelo assistente.  
  
## <a name="related-tools-and-information"></a>Ferramentas e informações relacionadas  
 Você também pode usar o assistente para [explorar dados](explore-data-sql-server-data-mining-add-ins.md) , disponível no cliente de mineração de dados para Excel, para examinar a distribuição de valores em uma coluna do Excel. Para obter mais informações, consulte [explorando e limpando dados](exploring-and-cleaning-data.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
  
