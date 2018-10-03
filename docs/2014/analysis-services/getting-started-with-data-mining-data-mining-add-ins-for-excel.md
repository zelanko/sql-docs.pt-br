---
title: Introdução ao Data Mining (Data Mining Add-ins para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: cbe10a19-e194-408e-a65b-5fdf3fb1e880
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5c4fe81ed240f210157e450b6c54fe370e22bcb8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094126"
---
# <a name="getting-started-with-data-mining-data-mining-add-ins-for-excel"></a>Introdução à mineração de dados (Suplementos de Mineração de Dados para Excel)
  A mineração de dados é o processo de descoberta de padrões significativos nos dados. A mineração de dados é um complemento natural ao processo de explorar e entender seus dados por meio de BI tradicional. Os algoritmos da máquina podem processar grandes quantidades de dados e descobrir padrões e tendências que, de outra forma, ficariam ocultos.  
  
 Para fazer mineração de dados, você coleta dados que são relevantes para uma pergunta específica, como "quem são meus clientes?" ou "quais produtos foram comprados?" e, em seguida, aplica um algoritmo para localizar correlações estatísticas nos dados. As tendências e os padrões encontrados por meio de análise são armazenados como um modelo de mineração. Em seguida, é possível aplicar o modelo de mineração aos novos dados, em cenários comerciais como estes:  
  
-   Usar as tendências passadas para prever as vendas para o próximo trimestre, os requisitos de inventário ou a satisfação do cliente.  
  
-   Aplicar o conhecimento de clientes atuais para criar o perfil de novos clientes e recomendar novos produtos ou oportunidades.  
  
-   Localizar correlações entre eventos passados para prever falhas de servidor ou tempo de inatividade.  
  
-   Analisar quais produtos os clientes compram juntos e usar as informações para recomendar pacotes ou planejar a colocação de produto.  
  
 O método de análise escolhido depende de suas metas. Os Suplementos de Mineração de Dados oferecem suporte a estes tipos de análise:  
  
-   Aprendizado supervisionado e não supervisionado  
  
-   Clustering (segmentação)  
  
-   Análise de fatores, usando Bayesiano e redes neurais  
  
-   Análise de série temporal  
  
-   Análise de associação, recomendações e análise da cesta de compras  
  
-   Pontuação de resultados binários  
  
-   Regressão linear  
  
 Além disso, os suplementos fornecem ajuda na fase de preparação de dados: seleção, exploração e limpeza de dados.  
  
## <a name="define-your-goal"></a>Defina sua meta  
 Antes de começar, considere a pergunta que você realmente quer responder. A exploração é esclarecedora por si só, mas se você quiser aplicar suas descobertas a novos dados, deverá mencionar claramente o que espera que o modelo produza e como medirá se o modelo realiza essas metas.  
  
 Por exemplo, em vez de uma meta de “localizar novos clientes”, esclareça seu objetivo como algo mais completo, como “identificar os dados demográficos dos clientes que provavelmente comprarão nosso produto com uma probabilidade de pelo menos 65%”.  
  
-   O conjunto de dados deve conter pelo menos um atributo de "resultado" que você pode usar para treinamento e previsão. Se não houver tal atributo, é possível rotular manualmente alguns dados de treinamento ou usar outras colunas para criar um proxy para o resultado.  
  
     Por exemplo, se você quiser prever “os melhores clientes potenciais”, deverá aplicar algumas regras de negócio antes de rotular clientes existentes, de modo que a mineração de dados possa aprender com os exemplos que você fornece.  
  
-   Se você estiver trabalhando com um valor que é alterado com o passar do tempo e quiser prever tendências do futuro, pense sobre a granularidade dos resultados necessários. Você deseja previsões para um mês, um dia ou anualmente? Os dados precisam ser analisados usando as mesmas unidades que você deseja prever.  
  
     Com padrões cíclicos, se você não tiver bons resultados com dados diários, tente frações de tempo diferentes ou tente usar dias da semana, meses ou mesmo feriados.  
  
-   Antes de iniciar um assistente para localizar novas correlações em seus dados, dê mais uma olhada em seus dados e considere o que tipo de relações existentes que podem estar presentes no conjunto de dados. Há variáveis de confusão? Há duplicatas ou proxies?  
  
-   Quais são as métricas pelas quais o sucesso do modelo será avaliado? Como você saberá que o modelo é "bom o bastante”? “  
  
-   Deseja fazer previsões com base no modelo de mineração de dados ou apenas procurar padrões e associações interessantes?  
  
## <a name="explore-your-data-and-explore-the-model"></a>Explorar seus dados e explorar o modelo  
 Talvez você já compreenda completamente os dados e o domínio. Se você fizer isso, deverá levar algum tempo para criar o perfil dos dados com a modelagem em mente.  
  
 Dedique um tempo à exibição da distribuição de valores e identifique possíveis problemas, como valores ausentes ou espaços reservados.  
  
 Se você estiver planejando executar a mineração de dados em um conjunto de dados que era tão grande ou complexo que você não podia analisá-lo com outros métodos, considere a amostragem ou a redução de dados.  
  
-   Como os dados são distribuídos?  
  
-   Como as colunas estão relacionadas ou, se houver várias tabelas, como elas estão relacionadas?  
  
-   Algum valor não foi encontrado? Há valores que precisam de conversão ou pré-processamento?  
  
-   A maior parte dos dados é composta de texto, números ou uma combinação?  
  
-   Você tem dados suficientes para dar suporte à análise dos resultados de destino? Se você estiver analisando associações entre produtos, poderá precisar de muito mais dados. Se você estiver prevendo um resultado binário, poderá obter com muito menos, supondo que o conjunto de dados seja equilibrado.  
  
 Depois que seu modelo estiver completo, examine os resultados e identifique maneiras de corrigir os dados ou obter resultados melhores. É excessivamente raro que seu primeiro modelo forneça todas as respostas. Em geral, a mineração de dados é um processo iterativo.  
  
 Conforme você tenta compartimentalizar seus dados de maneiras diferentes, ou adicionar novas colunas, lembre-se de usar o **modelo de documento** Assistente para capturar um instantâneo dos metadados e os resultados de cada modelo. Ter um registro facilitará rastrear o progresso em sua exploração.  
  
 [Explorando e limpando dados](exploring-and-cleaning-data.md)  
  
## <a name="validate-your-model"></a>Validar o modelo  
 Ao executar cada assistente ou ferramenta, o algoritmo analisa o conteúdo dos dados e determina se um padrão estatisticamente válido existe. Se o algoritmo não puder localizar padrão válidos, você receberá uma mensagem de erro. Porém, mesmo que um modelo tenha sido criado com êxito, você desejará testar o modelo para ver se ele valida suas suposições. Você pode usar ferramentas como o [gráfico de precisão &#40;SQL Server Data Mining Add-ins&#41; ](accuracy-chart-sql-server-data-mining-add-ins.md) ou [validação cruzada &#40;SQL Server Data Mining Add-ins&#41; ](cross-validation-sql-server-data-mining-add-ins.md) para gerar estatísticas medidas de qualidade do modelo.  
  
 Ao avaliar os resultados do seu primeiro modelo, faça perguntas como estas:  
  
-   Que tipos de padrões foram encontrados? Quais são as probabilidades e os valores de suporte?  
  
-   Nossas previsões sobre tendências estavam corretas ou houve correlações surpreendentes?  
  
-   Coletamos dados suficientes? A compartimentalização de dados gerará padrões mais claros?  
  
-   O conjunto de dados é balanceado? A validação cruzada pode testar a representatividade de seus dados.  
  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
 [Cliente de mineração de dados para Excel &#40;suplementos de mineração de dados do SQL Server&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
 [Escolhendo um modelo](choosing-a-model.md)  
  
## <a name="explore-and-refine"></a>Explorar e refinar  
 Se o modelo parecer válido, você poderá usar o modelo para previsão e recomendação, derivando ideias ou planejando estratégias comerciais.  
  
-   Use o navegador de mineração de dados no Cliente de Mineração de Dados para Excel para explorar e interagir com o modelo.  
  
-   Use o Excel para reorganizar e filtrar os resultados.  
  
-   Use o Visio para criar e realçar mostra as relações encontradas nos dados.  
  
 Geralmente, o primeiro resultado da análise é que você vê maneiras de melhorar a análise, ou percebe que precisa obter dados novos e melhores. Como os modelos que você cria usando os suplementos de mineração de dados para Excel podem ser salvos em uma instância do Analysis Services, é relativamente fácil atualizar o modelo com novos dados, e continuar refinando e reutilizando os modelos bem-sucedidos.  
  
 Um importante uso dos modelos de mineração de dados é criar previsões e recomendações. Os suplementos de mineração de dados para Excel incluem as ferramentas que facilitam a geração até mesmo de consultas de previsão complexas, para converter ideias em resultados acionáveis. Todas essas ferramentas são totalmente integradas aos Excel.  
  
 [Exibindo modelos de &#40;Data Mining Add-ins para o Office&#41;](viewing-models-data-mining-add-ins-for-office.md)  
  
 [Validando modelos e usando modelos para previsão &#40;Data Mining Add-ins para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
## <a name="see-also"></a>Consulte também  
 [O que está incluído nos dados de suplementos de mineração para o Office](what-s-included-in-the-data-mining-add-ins-for-office.md)   
 [Referência técnica do &#40;Data Mining Add-ins para Excel&#41;](technical-reference-data-mining-add-ins-for-excel.md)  
  
  
