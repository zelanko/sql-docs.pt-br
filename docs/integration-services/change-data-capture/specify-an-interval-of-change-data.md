---
title: Especificar um intervalo de dados de alteração | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],specifying interval
ms.assetid: 17899078-8ba3-4f40-8769-e9837dc3ec60
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3cb5949943cb03095328bc43599fbfef2fa74da2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294567"
---
# <a name="specify-an-interval-of-change-data"></a>Especificar um intervalo de dados de alteração

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  No fluxo de controle de um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que realiza uma carga incremental de dados de alteração, a primeira tarefa serve para calcular os pontos de extremidade do intervalo de alteração. Estes pontos de extremidade são valores **datetime** e são armazenados em variáveis do pacote para uso posterior.  
  
> [!NOTE]  
>  Para obter uma descrição do processo geral de criação do fluxo de controle, consulte [Change Data Capture &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md).  
  
## <a name="set-up-package-variables-for-the-endpoints"></a>Definir Variáveis do Pacote para os pontos de extremidade  
 Antes de configurar a tarefa Execute SQL para calcular os pontos de extremidade, as variáveis do pacote que irão armazenar os pontos de extremidade devem ter sido definidas.  
  
#### <a name="to-set-up-package-variables"></a>Para definir as variáveis do pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra um novo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Na janela **Variáveis** , criar as seguintes variáveis:  
  
    1.  Crie uma variável com o tipo de dados **datetime** para guardar o ponto inicial para o intervalo.  
  
         Este exemplo usa o nome de variável, ExtractStartTime.  
  
    2.  Crie outra variável com o tipo de dados **datetime** para guardar o ponto final para o intervalo.  
  
         Este exemplo usa o nome de variável, ExtractEndTime.  
  
 Ao se calcular os pontos de extremidade em um pacote mestre que executa vários pacotes filho, é possível usar as configurações de Variável de Pacote Pai para passar os valores destas variáveis para cada pacote filho. Para obter mais informações, consulte [Tarefa Executar Pacote](../../integration-services/control-flow/execute-package-task.md) e [Usar os valores de variáveis e parâmetros em um pacote filho](../../integration-services/packages/legacy-package-deployment-ssis.md#child).  
  
## <a name="calculate-a-starting-point-and-an-ending-point-for-change-data"></a>Calcule um Ponto Inicial e um Ponto Final para Dados de Alteração  
 Depois de definir as variáveis do pacote para os pontos de extremidade do intervalo, é possível calcular os valores reais para esses pontos de extremidade e mapear esses valores para as variáveis correspondentes. Devido a esses pontos de extremidade serem valores **datetime** , deve-se usar funções que podem calcular ou trabalhar com valores **datetime** . A linguagem de expressão [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e o Transact-SQL têm funções que funcionam com valores **datetime** :  
  
 Funções na linguagem de expressão [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que funcionam com valores **datetime**  
 -   [DATEADD &#40;Expressão do SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)  
  
-   [DATEDIFF &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)  
  
-   [DATEPART &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)  
  
-   [DAY &#40;Expressão do SSIS&#41;](../../integration-services/expressions/day-ssis-expression.md)  
  
-   [GETDATE &#40;Expressão do SSIS&#41;](../../integration-services/expressions/getdate-ssis-expression.md)  
  
-   [GETUTCDATE &#40;Expressão do SSIS&#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)  
  
-   [MONTH &#40;Expressão do SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)  
  
-   [YEAR &#40;Expressão do SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)  
  
 Funções no Transact-SQL que funcionam com valores **datetime**  
 [Tipos de dados e funções de data e hora&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 Antes de usar uma destas funções **datetime** para calcular os pontos de extremidade, deve-se determinar se o intervalo é fixo e se ocorre regularmente. Normalmente, você quer aplicar alterações que aconteceram em tabelas fonte para tabelas destino em um período regular. Por exemplo, você poderia querer aplicar essas alterações de hora em hora, diariamente, ou semanalmente.  
  
 Depois que você entender se seu intervalo de alteração é fixo ou é mais aleatório, você pode calcular os pontos de extremidade:  
  
-   **Calculando a data e hora inicial**. Usar a data e hora final da carga anterior como a data e hora inicial atual. Se você usar um intervalo fixo para cargas incrementais, será possível calcular este valor usando as funções **datetime** do Transact-SQL ou da linguagem de expressão [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Caso contrário, talvez seja preciso manter os pontos de extremidade entre execuções e usar uma tarefa Execute SQL ou uma tarefa Script para carregar o ponto de extremidade anterior.  
  
-   **Calculando a data e hora final**. Se você usar um intervalo fixo para cargas incrementais, calcule a data e hora final atual como um deslocamento da data e hora inicial. Novamente, é possível calcular este valor usando as funções **datetime** do Transact-SQL ou da linguagem de expressão [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 No procedimento seguinte, o intervalo de alteração usa um intervalo fixo e assume que o pacote de carga incremental é executado diariamente sem exceção. Caso contrário, os dados de alteração para intervalos ausentes seriam perdidos. O ponto inicial para o intervalo é meia-noite de anteontem, ou seja, entre 24 e 48 horas atrás. O ponto final para o intervalo é meia-noite de ontem, ou seja, a noite anterior, entre 0 e 24 horas atrás.  
  
#### <a name="to-calculate-the-starting-point-and-ending-point-for-the-capture-interval"></a>Para calcular o ponto inicial e final para o intervalo de captura  
  
1.  Na guia **Fluxo de Controle** do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , adicione uma tarefa Execute SQL ao pacote.  
  
2.  Abra o **Editor da tarefa Execute SQL**e na página **Geral** do editor, selecione as seguintes opções:  
  
    1.  Para **Conjunto de Resultados**, selecione **Linha simples**.  
  
    2.  Configure uma conexão válida com o banco de dados fonte.  
  
    3.  Para **SQLSourceType**, selecione **Entrada direta**.  
  
    4.  Para **SQLStatement**, digite a seguinte instrução SQL:  
  
        ```sql
        SELECT DATEADD(dd,0, DATEDIFF(dd,0,GETDATE()-1)) AS ExtractStartTime,  
          DATEADD(dd,0, DATEDIFF(dd,0,GETDATE())) AS ExtractEndTime  
  
        ```  
  
3.  Na página **Conjunto de Resultados** do **Editor da tarefa Executar SQL**, mapeie o resultado de ExtractStartTime para a variável do pacote ExtractStartTime e o resultado de ExtractEndTime para a variável do pacote ExtractEndTime.  
  
    > [!NOTE]  
    >  Quando você usa uma expressão para definir o valor de uma variável [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], a expressão é avaliada sempre que o valor da variável é acessado.  
  
## <a name="next-step"></a>Próxima etapa  
 Depois de calcular o ponto inicial e final para um intervalo de alterações, a próxima etapa é determinar se os dados de alteração estão prontos.  
  
 **Próximo tópico:** [Determinar se os dados de alterações estão protos](../../integration-services/change-data-capture/determine-whether-the-change-data-is-ready.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Usar variáveis em pacotes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)   
 [Expressões do SSIS &#40;Integration Services&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)   
 [Tarefa Executar SQL](../../integration-services/control-flow/execute-sql-task.md)   
 [Tarefa Script](../../integration-services/control-flow/script-task.md)  
  
  
