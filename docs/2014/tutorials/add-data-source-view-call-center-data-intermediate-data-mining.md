---
title: Adicionando dados de um exibição da fonte de dados de Call Center (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a448e7e4-dbd1-4d31-90bc-4d4a1c23b352
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f212c6436af0e35c7cfaceadf8c519765d0a07a6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171937"
---
# <a name="adding-a-data-source-view-for-call-center-data-intermediate-data-mining-tutorial"></a>Adicionando uma exibição da fonte de dados aos dados de call center (Tutorial de mineração de dados intermediário)
  Nesta tarefa, você adiciona uma exibição da fonte de dados que será usada para acessar os dados do call center. Os mesmos dados serão usados para criar o modelo de rede neural inicial para exploração e o modelo de regressão logística que você usará para fazer recomendações.  
  
 Você também usará o Designer de Exibição da Fonte de Dados para adicionar uma coluna para o dia da semana. Isso é porque, embora os dados de origem acompanhem os dados do call center por datas, sua experiência diz que há padrões recorrentes em termos de volume de chamadas e qualidade de serviço, dependendo se o dia for um fim de semana ou um dia útil.  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-add-a-data-source-view"></a>Para adicionar uma exibição da fonte de dados  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **exibições da fonte de dados**e selecione **nova exibição da fonte de dados**.  
  
     O Assistente de Exibição da Fonte de Dados é exibido.  
  
2.  Na página **Bem-vindo ao Assistente de Exibição da Fonte de Dados** , clique em **Avançar**.  
  
3.  Sobre o **selecionar uma fonte de dados** página, em **fontes de dados relacionais**, selecione o [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] fonte de dados. Se você não tiver essa fonte de dados, consulte [Tutorial básico de mineração de dados](../../2014/tutorials/basic-data-mining-tutorial.md). Clique em **Avançar**.  
  
4.  Sobre o **selecionar tabelas e exibições** página, selecione a tabela a seguir e, em seguida, clique na seta à direita para adicioná-la à exibição de fonte de dados:  
  
    -   **FactCallCenter (dbo)**  
  
    -   **DimDate**  
  
5.  Clique em **Avançar**.  
  
6.  Sobre o **Concluindo o assistente** página, por padrão, a exibição da fonte de dados é denominada [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]. Altere o nome para **CallCenter**e, em seguida, clique em **concluir**.  
  
     Designer de exibição de fonte de dados é aberta para exibir o **CallCenter** exibição da fonte de dados.  
  
7.  Clique com botão direito dentro do painel de exibição da fonte de dados e, em seguida, selecione **Adicionar/remover tabelas**. Selecione a tabela **DimDate** e clique em **Okey**.  
  
     Uma relação deve ser adicionada automaticamente entre o `DateKey` colunas em cada tabela. Você usará essa relação para obter a coluna **EnglishDayNameOfWeek**, da **DimDate** de tabela e usá-lo em seu modelo.  
  
8.  No designer de exibição da fonte de dados, clique na tabela, **FactCallCenter**e selecione **novo cálculo nomeado**.  
  
     No **criar cálculo nomeado** caixa de diálogo, digite os seguintes valores:  
  
    |||  
    |-|-|  
    |**Nome da coluna**|DayOfWeek|  
    |**Descrição**|Obter dia de semana da tabela DimDate|  
    |**Expression**|`(SELECT EnglishDayNameOfWeek AS DayOfWeek FROM DimDate where FactCallCenter.DateKey = DimDate.DateKey)`|  
  
     Para verificar se a expressão cria os dados você precisa, clique na tabela **FactCallCenter**e, em seguida, selecione **explorar dados**.  
  
9. Reserve um minuto para revisar os dados disponíveis, para que você possa entender como são usados na mineração de dados:  
  
|Nome da coluna|Contém|  
|-----------------|--------------|  
|FactCallCenterID|Uma chave arbitrária criada durante a importação dos dados para o data warehouse.<br /><br /> Esta coluna identifica registros exclusivos e deve ser usada como o chave de caso para o modelo de mineração de dados.|  
|DateKey|A data da operação do call center, expressa como um inteiro. Chaves de datas em valores inteiros são usadas frequentemente em data warehouses, mas você pode obter a data no formato data/hora se agrupar por valores de data.<br /><br /> Observe que as datas não são exclusivas porque o fornecedor oferece um relatório separado para cada turno em cada dia de operação.|  
|WageType|Indica se o dia era um dia da semana, um fim de semana ou um feriado.<br /><br /> É possível que haja uma diferença na qualidade de atendimento ao consumidor nos fins de semana versus os dias da semana para que você usará esta coluna como entrada.|  
|Turno|Indica o turno para o qual as chamadas são registradas. Esse call center divide o dia de trabalho em quatro turnos: AM, PM1, PM2 e Meia-noite.<br /><br /> É possível que o turno influencie na qualidade de atendimento ao consumidor; então, você usará isso como entrada.|  
|LevelOneOperators|Indica o número de operadores de nível 1 no imposto.<br /><br /> Os funcionários do call center começam no Nível 1. Então, esses funcionários são menos experientes.|  
|LevelTwoOperators|Indica o número de operadores de Nível 2 em serviço.<br /><br /> Um funcionário deve registrar um certo número de horas de serviço para ser qualificado como operador de Nível 2.|  
|TotalOperators|O número total de operadores presentes durante o turno.|  
|Chamadas|O número de chamadas recebidas durante o turno.|  
|AutomaticResponses|O número de chamadas administradas totalmente pelo processamento de chamada automatizado (Resposta Interativa de Voz ou IVR).|  
|Orders|O número de pedidos resultantes das chamadas.|  
|IssuesRaised|O número de emissões geradas pelas chamadas que exigem acompanhamento.|  
|AverageTimePerIssue|O tempo médio necessário para responder a uma chamada de entrada.|  
|ServiceGrade|Uma métrica que indica a qualidade geral do serviço, medido como o *taxa de abandono* para o turno inteiro. Quanto maior a taxa de abandono, maior a probabilidade de insatisfação dos clientes e de perda dos pedidos em potencial.|  
  
 Observe que os dados incluem quatro colunas diferentes com base em uma única coluna de data: `WageType`, **DayOfWeek**, `Shift`, e `DateKey`. Normalmente, na mineração de dados não é uma boa ideia usar várias colunas derivadas dos mesmos dados, já que os valores se correlacionam entre si muito fortemente e podem ofuscar outros padrões.  
  
 No entanto, não usaremos `DateKey` no modelo porque ela contém muitos valores exclusivos. Não há nenhuma relação direta entre `Shift` e **DayOfWeek**, e `WageType` e **DayOfWeek** são parcialmente relacionados apenas. Se você estivesse preocupado com a colinearidade, poderia criar a estrutura usando todas as colunas disponíveis e depois ignorar colunas diferentes em cada modelo e testar o efeito.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando uma estrutura de rede Neural e o modelo &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de fontes de dados em modelos multidimensionais](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
