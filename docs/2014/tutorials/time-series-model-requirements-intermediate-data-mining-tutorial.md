---
title: Noções básicas sobre os requisitos de um modelo de série temporal (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1ce2b3e3-108a-4f7e-985f-a20b816d0da7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8e46d7fc8a0c214501841de448a94d1211b95fa1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892959"
---
# <a name="understanding-the-requirements-for-a-time-series-model-intermediate-data-mining-tutorial"></a>Compreendendo os requisitos para um modelo de série temporal (Tutorial de mineração de dados intermediário)
  Quando for preparar os dados para usá-los em um modelo de previsão, você deverá garantir que eles contenham uma coluna que possa ser usada na identificação das etapas da série temporal. Essa coluna será designada como a coluna `Key Time`. Como é uma chave, a coluna deve conter valores numéricos exclusivos.  
  
 Escolher a unidade certa para a coluna `Key Time` é uma parte importante da análise. Por exemplo, suponha que seus dados de vendas sejam atualizados a cada minuto. Você não precisa necessariamente usar minutos como a unidade para a série temporal; você pode achar mais significativo acumular os dados de vendas por dia, semana ou mês. Se você não tiver certeza sobre qual unidade de tempo usar, poderá criar uma nova exibição da fonte de dados para cada agregação e criar modelos relacionados, para ver se tendências diferentes emergem a cada nível de agregação.  
  
 Neste tutorial, os dados de vendas são coletados diariamente no banco de dados de vendas transacional, mas para a mineração de dados, os dados foram pré-agregados por mês, usando uma exibição.  
  
 Além disso, é recomendável para a análise que os dados tenham o mínimo possível de lacunas. Se você planeja analisar várias séries de dados, todas as séries devem iniciar ou terminar preferencialmente na mesma data. Se houver lacunas nos dados, mas não no início ou no final de uma série, você poderá usar o parâmetro MISSING_VALUE_SUBSTITUTION para preenchê-la. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] também oferece diversas opções para a substituição de dados ausentes por valores, como o uso de médias ou de constantes.  
  
> [!WARNING]  
>  As ferramentas Gráfico Dinâmico e Tabela Dinâmica que eram fornecidas em versões anteriores do designer de exibição da fonte de dados não são mais fornecidas. Recomendamos que você identifique as lacunas nos dados de série temporal de antemão, usando ferramentas como o Criador de Perfil de Dados fornecidas no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
### <a name="to-identify-the-time-key-for-the-forecasting-model"></a>Para identificar a chave de tempo para o modelo de previsão  
  
1.  No painel, **SalesByRegion. dsv [Design]**, clique com o botão direito do mouse na tabela vTimeSeries e, em seguida, selecione **explorar dados**.  
  
     Uma nova guia é aberta, intitulada **explorar a tabela vTimeSeries**.  
  
2.  Na guia **tabela** , examine os dados que são usados nas colunas TimeIndex e data de relatório.  
  
     Ambos são sequências com valores exclusivos e podem ser usados como a chave de série temporal; porém, os tipos de dados das colunas são diferentes. O algoritmo MTS não requer um tipo de dados `datetime`, apenas que os valores sejam distintos e ordenados. Dessa forma, cada coluna pode ser usada como a chave de tempo para o modelo de previsão.  
  
3.  Na superfície de design da exibição da fonte de dados, selecione a coluna, data de relatório e selecione **Propriedades**. Em seguida, clique na coluna TimeIndex e selecione **Properties**.  
  
     O campo TimeIndex tem o tipo de dados System. Int32, enquanto a data de relatório do campo tem o tipo de dados System. DateTime. Muitos data warehouses convertem valores de data/hora em inteiros e usam a coluna de inteiros como chave, para melhorar desempenho da indexação. No entanto, se você usar essa coluna, o algoritmo MTS fará previsões usando valores futuros como 201014, 201014 e assim sucessivamente. Como você deseja representar sua previsão de dados de vendas usando datas de calendário, você usará a coluna data de relatório como o identificador de série exclusivo.  
  
### <a name="to-set-the-key-in-the-data-source-view"></a>Para definir a chave na exibição da fonte de dados.  
  
1.  No painel **SalesByRegion. dsv**, selecione a tabela vTimeSeries.  
  
2.  Clique com o botão direito do mouse na coluna, data do relatório e selecione **definir chave primária lógica**.  
  
## <a name="handling-missing-data-optional"></a>Manipulando dados ausentes (opcional)  
 Se qualquer série tiver dados ausentes, talvez você obtenha um erro ao tentar processar o modelo. Existem diversas maneiras de contornar dados ausentes:  
  
-   Você pode deixar que o Analysis Services preencha os valores ausentes, por meio do cálculo de uma média ou usando um valor anterior. Você faz isso ao definir o parâmetro MISSING_VALUE_SUBSTITUTION no modelo de mineração. Para obter mais informações sobre esse parâmetro, consulte [referência técnica do algoritmo do Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md). Para obter informações sobre como alterar parâmetros em um modelo de mineração existente, consulte [Exibir ou alterar parâmetros de algoritmo](../../2014/analysis-services/data-mining/view-or-change-algorithm-parameters.md).  
  
-   Você pode alterar a fonte de dados ou filtrar a exibição subjacente para eliminar a série irregular ou substituir valores. Você pode fazer isso na fonte de dados relacional ou pode modificar a exibição da fonte de dados criando consultas nomeadas ou cálculos nomeados personalizados. Para obter mais informações, consulte [Exibições de fontes de dados em modelos multidimensionais](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models). Uma tarefa posterior nesta lição oferecerá um exemplo de como construir uma consulta nomeada e um cálculo personalizado.  
  
 Para este cenário, alguns dados estão faltando no início de uma série: ou seja, não há dados para a linha de produto T1000 até julho de 2007. Caso contrário, todas as séries terminariam na mesma data e não haveria valores ausentes.  
  
 O requisito do algoritmo Microsoft Time Series é que qualquer série que você inclua em um único modelo deve ter o mesmo ponto **final** . Como o modelo de bicicleta T1000 foi apresentado em 2007, os dados dessa série começam depois de outros modelos de bicicleta, mas a série termina na mesma data e, portanto, os dados são usáveis.  
  
#### <a name="to-close-the-data-source-view-designer"></a>Para fechar o designer da exibição da fonte de dados  
  
-   Clique com o botão direito do mouse na guia, **Explore a tabela vTimeSeries**e selecione **fechar**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando uma estrutura de previsão e modelo &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo MTS](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
