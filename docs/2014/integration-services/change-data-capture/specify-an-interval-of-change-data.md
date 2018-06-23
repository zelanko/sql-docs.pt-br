---
title: Especificar um intervalo de dados de alteração | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- incremental load [Integration Services],specifying interval
ms.assetid: 17899078-8ba3-4f40-8769-e9837dc3ec60
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 50b8ca15207eaa89726ed2abe90bb8d862b2f266
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012065"
---
# <a name="specify-an-interval-of-change-data"></a>Especificar um intervalo de dados de alteração
  No fluxo de controle de um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que realiza uma carga incremental de dados de alteração, a primeira tarefa serve para calcular os pontos de extremidade do intervalo de alteração. Esses pontos de extremidade são `datetime` valores e serão armazenados em variáveis de pacote para uso posteriormente no pacote.  
  
> [!NOTE]  
>  Para obter uma descrição do processo geral de criação do fluxo de controle, consulte [Change Data Capture &#40;SSIS&#41;](change-data-capture-ssis.md).  
  
## <a name="set-up-package-variables-for-the-endpoints"></a>Definir Variáveis do Pacote para os pontos de extremidade  
 Antes de configurar a tarefa Execute SQL para calcular os pontos de extremidade, as variáveis do pacote que irão armazenar os pontos de extremidade devem ter sido definidas.  
  
#### <a name="to-set-up-package-variables"></a>Para definir as variáveis do pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra um novo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Na janela **Variáveis** , criar as seguintes variáveis:  
  
    1.  Crie uma variável com o `datetime` tipo de dados para guardar o ponto de partida para o intervalo.  
  
         Este exemplo usa o nome de variável, ExtractStartTime.  
  
    2.  Crie outra variável com o `datetime` tipo de dados para guardar o ponto final para o intervalo.  
  
         Este exemplo usa o nome de variável, ExtractEndTime.  
  
 Ao se calcular os pontos de extremidade em um pacote mestre que executa vários pacotes filho, é possível usar as configurações de Variável de Pacote Pai para passar os valores destas variáveis para cada pacote filho. Para obter mais informações, consulte [Tarefa Executar Pacote](../control-flow/execute-package-task.md) e [Usar os valores de variáveis e parâmetros em um pacote filho](../use-the-values-of-variables-and-parameters-in-a-child-package.md).  
  
## <a name="calculate-a-starting-point-and-an-ending-point-for-change-data"></a>Calcule um Ponto Inicial e um Ponto Final para Dados de Alteração  
 Depois de definir as variáveis do pacote para os pontos de extremidade do intervalo, é possível calcular os valores reais para esses pontos de extremidade e mapear esses valores para as variáveis correspondentes. Devido a esses pontos de extremidade serem valores `datetime`, deve-se usar funções que podem calcular ou trabalhar com valores `datetime`. Ambos os [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] linguagem de expressão e Transact-SQL têm funções que trabalham com `datetime` valores:  
  
 Funções no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] linguagem de expressão que funcionam com `datetime` valores  
 -   [DATEADD &#40;expressão SSIS&#41;](../expressions/dateadd-ssis-expression.md)  
  
-   [DATEDIFF &#40;expressão SSIS&#41;](../expressions/datediff-ssis-expression.md)  
  
-   [DATEPART &#40;expressão SSIS&#41;](../expressions/datepart-ssis-expression.md)  
  
-   [DIA &#40;expressão SSIS&#41;](../expressions/day-ssis-expression.md)  
  
-   [GETDATE &#40;expressão SSIS&#41;](../expressions/getdate-ssis-expression.md)  
  
-   [GETUTCDATE &#40;expressão SSIS&#41;](../expressions/getutcdate-ssis-expression.md)  
  
-   [MÊS &#40;expressão SSIS&#41;](../expressions/month-ssis-expression.md)  
  
-   [ANO &#40;expressão SSIS&#41;](../expressions/year-ssis-expression.md)  
  
 Funções em Transact-SQL que trabalham com `datetime` valores  
 [Tipos de dados e funções de data e hora&#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql).  
  
 Antes de usar uma destas funções `datetime` para calcular os pontos de extremidade, deve-se determinar se o intervalo é fixo e se ocorre regularmente. Normalmente, você quer aplicar alterações que aconteceram em tabelas fonte para tabelas destino em um período regular. Por exemplo, você poderia querer aplicar essas alterações de hora em hora, diariamente, ou semanalmente.  
  
 Depois que você entender se seu intervalo de alteração é fixo ou é mais aleatório, você pode calcular os pontos de extremidade:  
  
-   **Calculando a data e hora inicial**. Usar a data e hora final da carga anterior como a data e hora inicial atual. Se você usar um intervalo fixo para cargas incrementais, você pode calcular esse valor usando o `datetime` funções do Transact-SQL ou do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] linguagem de expressão. Caso contrário, talvez seja preciso manter os pontos de extremidade entre execuções e usar uma tarefa Execute SQL ou uma tarefa Script para carregar o ponto de extremidade anterior.  
  
-   **Calculando a data e hora final**. Se você usar um intervalo fixo para cargas incrementais, calcule a data e hora final atual como um deslocamento da data e hora inicial. Novamente, você pode calcular esse valor usando o `datetime` funções do Transact-SQL ou do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] linguagem de expressão.  
  
 No procedimento seguinte, o intervalo de alteração usa um intervalo fixo e assume que o pacote de carga incremental é executado diariamente sem exceção. Caso contrário, os dados de alteração para intervalos ausentes seriam perdidos. O ponto inicial para o intervalo é meia-noite de anteontem, ou seja, entre 24 e 48 horas atrás. O ponto final para o intervalo é meia-noite de ontem, ou seja, a noite anterior, entre 0 e 24 horas atrás.  
  
#### <a name="to-calculate-the-starting-point-and-ending-point-for-the-capture-interval"></a>Para calcular o ponto inicial e final para o intervalo de captura  
  
1.  Na guia **Fluxo de Controle** do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , adicione uma tarefa Execute SQL ao pacote.  
  
2.  Abra o **Editor da tarefa Execute SQL**e na página **Geral** do editor, selecione as seguintes opções:  
  
    1.  Para **Conjunto de Resultados**, selecione **Linha simples**.  
  
    2.  Configure uma conexão válida com o banco de dados fonte.  
  
    3.  Para **SQLSourceType**, selecione **Entrada direta**.  
  
    4.  Para **SQLStatement**, digite a seguinte instrução SQL:  
  
        ```  
        SELECT DATEADD(dd,0, DATEDIFF(dd,0,GETDATE()-1)) AS ExtractStartTime,  
          DATEADD(dd,0, DATEDIFF(dd,0,GETDATE())) AS ExtractEndTime  
  
        ```  
  
3.  Na página **Conjunto de Resultados** do **Editor da tarefa Executar SQL**, mapeie o resultado de ExtractStartTime para a variável do pacote ExtractStartTime e o resultado de ExtractEndTime para a variável do pacote ExtractEndTime.  
  
    > [!NOTE]  
    >  Quando você usa uma expressão para definir o valor de uma variável [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , a expressão é avaliada sempre que o valor da variável é acessado.  
  
## <a name="next-step"></a>Próxima etapa  
 Depois de calcular o ponto inicial e final para um intervalo de alterações, a próxima etapa é determinar se os dados de alteração estão prontos.  
  
 **Próximo tópico:** [Determinar se os dados de alteração estão prontos](determine-whether-the-change-data-is-ready.md)  
  
## <a name="see-also"></a>Consulte também  
 [Usar variáveis em pacotes](../use-variables-in-packages.md)   
 [Expressões do SSIS &#40;Integration Services&#41;](../expressions/integration-services-ssis-expressions.md)   
 [Tarefa Executar SQL](../control-flow/execute-sql-task.md)   
 [Tarefa Script](../control-flow/script-task.md)  
  
  
