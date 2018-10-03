---
title: Processando opções e configurações (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- process data option [Analysis Services]
- processing objects [Analysis Services]
- unprocess option [Analysis Services]
- process full option [Analysis Services]
- process index option [Analysis Services]
- process structure option [Analysis Services]
- process incremental option [Analysis Services]
- process update option [Analysis Services]
- process clear structure option [Analysis Services]
- process default option [Analysis Services]
ms.assetid: 2e858c74-ad3e-45f1-8745-efe2c0c3a7fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b832da95e823966af1c8d259087721119eed85e0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049496"
---
# <a name="processing-options-and-settings-analysis-services"></a>Processando opções e configurações (Analysis Services)
  Ao processar objetos no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode selecionar uma opção de processamento para controlar o tipo de processamento que ocorre para cada objeto. Os tipos de processamento variam de um objeto para outro e por alterações ocorridas no objeto desde que ele foi processado pela última vez. Se você habilitar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para selecionar automaticamente um método de processamento, ele usará o método que retornar o objeto a um estado inteiramente processado no menor tempo.  
  
 As configurações de processamento permitem controlar os objetos que são processados e os métodos usados para processar esses objetos. Algumas configurações de processamento são usadas principalmente para trabalhos de processamento em lotes. Para obter mais informações sobre processamento em lote, consulte [Processamento em lote &#40;Analysis Services&#41;](batch-processing-analysis-services.md).  
  
> [!NOTE]  
>  Esse tópico aplica-se a soluções multidimensionais e de mineração de dados. Para obter informações sobre as soluções tabulares, consulte [processar banco de dados, tabela ou partição](../tabular-models/process-database-table-or-partition-analysis-services.md).  
  
## <a name="processing-options"></a>Opções de processamento  
 A tabela a seguir descreve os métodos de processamento disponíveis no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e identifica os objetos compatíveis com cada método.  
  
|Modo|Aplica-se a|Description|  
|----------|----------------|-----------------|  
|**Processar Padrão**|Cubos, bancos de dados, dimensões, cubos, grupos de medidas, modelos de mineração, estruturas de mineração e partições.|Detecta o estado de processamento de objetos de banco de dados e realiza o processamento necessário para passar os objetos não processados ou parcialmente processados para um estado completamente processado. Se você alterar a associação de dados, Processar Padrão fará um Processar Completo no objeto afetado.|  
|**Processar Completo**|Cubos, bancos de dados, dimensões, cubos, grupos de medidas, modelos de mineração, estruturas de mineração e partições.|Processa um objeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e todos os objetos associados. Quando o comando Processar Completo é executado em um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] descarta todos os dados do objeto e, em seguida, processa o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural foi feita em um objeto, por exemplo, ao adicionar, excluir ou renomear uma hierarquia de atributo.|  
|**Processar Limpeza**|Cubos, bancos de dados, dimensões, cubos, grupos de medidas, modelos de mineração, estruturas de mineração e partições.|Descarta os dados no objeto especificado e em qualquer objeto constituinte de nível inferior. Depois de serem descartados, os dados não são recarregados.|  
|**Processar dados**|Dimensões, cubos, grupos de medidas e partições.|Processa apenas os dados sem criar agregações ou índices. Se houver dados nas partições, eles serão descartados antes de a partição ser populada novamente com dados de origem.|  
|**Processar adição**|Dimensões, grupos de medidas e partições.<br /><br /> Observação: O processo de adicionar não está disponível para processamento de dimensão no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], mas você pode escrever o script XMLA para executar esta ação.|Para dimensões, adiciona novos membros e atualiza legendas de atributo de dimensão e descrições.<br /><br /> Para grupos de medidas e partições, adiciona processos e dados de fatos recém-disponibilizados apenas às partições pertinentes.|  
|**Processar Atualização**|Dimensões|Força uma releitura dos dados e uma atualização dos atributos de dimensão. Agregações flexíveis e índices em partições relacionadas serão descartados.|  
|**Processar Índice**|Cubos, dimensões, grupos de medidas e partições|Cria ou recria índices e agregações para todas as partições processadas. Para objetos não processados, esta opção gera um erro.<br /><br /> O processamento com esta opção será necessário se você desativar Processamento Lento.|  
|**Processar Estrutura**|Cubos e estruturas de mineração|Se o cubo não estiver processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] processará, se necessário, todas as dimensões do cubo. Depois disso, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] criará apenas definições de cubo. Se esta opção for aplicada a uma estrutura de mineração, essa estrutura será populada com dados de origem. Diferente da opção Processar Completo, essa opção não itera o processamento para os modelos de mineração propriamente ditos.|  
|**Processar Limpeza de Estrutura**|Estruturas de mineração|Remove todos os dados de treinamento de uma estrutura de mineração.|  
  
## <a name="processing-settings"></a>Configurações de processamento  
 A tabela a seguir descreve as configurações de processamento que estão disponíveis ao criar uma operação de processo.  
  
|Opção de processamento|Description|  
|-----------------------|-----------------|  
|**Parallel**|Usado para o processamento em lotes. Esta configuração faz com que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bifurque as tarefas de processamento para executá-las em paralelo dentro de uma única transação. Se houver uma falha, o resultado será uma reversão de todas as alterações. É possível definir o número máximo de tarefas paralelas explicitamente ou deixar o servidor decidir a distribuição ideal. A opção Paralelo é útil para acelerar o processamento.|  
|**Sequencial (Modo da Transação)**|Controla o comportamento de execução do trabalho de processamento. Ao processar usando a opção **Uma Transação**, todas as alterações são confirmadas após o trabalho de processamento ser concluído com êxito. Isso significa que todos os objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] afetados por um determinado trabalho de processamento permanecem disponíveis para consulta até o processo de confirmação. Desse modo, os objetos ficam temporariamente indisponíveis. Com a opção **Separar Transações** , todos os objetos afetados por um processo do trabalho de processamento ficam indisponíveis para consulta assim que o processo é executado com êxito. As duas opções disponíveis são:<br /><br /> **Uma Transação**. O trabalho de processamento é executado como uma transação. Se nenhum processo do trabalho de processamento falhar, todas as alterações feitas pelo trabalho de processamento serão confirmadas. Se algum processo falhar, todas as alterações feitas pelo trabalho de processamento serão revertidas. **Uma Transação** é o valor padrão.<br /><br /> **Separar Transações**. Cada processo do trabalho de processamento é executado como um trabalho autônomo. Se um processo falhar, apenas aquele processo será revertido e o trabalho de processamento continuará. Cada trabalho confirma todas as alterações de processo no final do trabalho.|  
|**Opção da Tabela de Write-back**|Controla como as tabelas de write-back são tratadas durante o processamento. Esta opção se aplica às partições de write-back em um cubo e usa as seguintes opções:<br /><br /> **Usar Existente**. Usa a tabela de write-back existente. Este é o valor padrão.<br /><br /> **Criar**. Cria uma nova tabela de write-back e provoca a falha de um processo caso já exista algum.<br /><br /> **Criar Sempre**. Cria uma nova tabela de write-back, mesmo que já exista uma. A tabela existente é excluída e substituída.|  
|**Objetos Afetados pelo Processo**|Controla o escopo do objeto do trabalho de processamento. Um objeto afetado é definido pela dependência de objeto. Por exemplo, as partições dependem das dimensões que determinam a agregação, mas as dimensões não dependem das partições. Você pode usar as seguintes opções:<br /><br /> **False**. O trabalho processa os objetos explicitamente nomeados no trabalho e em todos os objetos dependentes. Por exemplo, se o trabalho de processamento contiver apenas dimensões, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] processará somente esses objetos identificados explicitamente no trabalho. Se o trabalho de processamento contiver partições, o processamento das partições invocará automaticamente o processamento das dimensões afetadas. **False** é a configuração padrão.<br /><br /> **True**. O trabalho processa os objetos nomeados explicitamente no trabalho, todos os objetos dependentes e todos os objetos afetados pelos objetos que estão sendo processados sem alterar o estado dos objetos afetados. Por exemplo, se o trabalho de processamento contiver apenas dimensões, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também processará todas as partições afetadas pelo processamento de dimensão em partições que estão em um estado processado. As partições afetadas que estão atualmente em um estado não processado não são processadas. No entanto, como as partições dependem das dimensões, se o trabalho de processamento contiver somente partições, o processamento das partições invocará automaticamente o processamento das dimensões afetadas, mesmo quando a dimensão estiver em um estado não processado.|  
|**Erros de chave de dimensão**|Determina a ação tomada por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quando ocorrem erros durante o processamento. Quando a opção Usar configuração de erro padrão é selecionada, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa a configuração de erro definida para cada objeto que está sendo processado. Se um objeto for configurado para usar a configuração padrão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizará as configurações padrão listadas para cada opção. Ao selecionar **Usar configuração de erro personalizada**, é possível selecionar valores para que as seguintes ações controlem o comportamento de tratamento de erros:<br /><br /> **Ação do erro de chave**. Se um valor de chave ainda não existir em um registro, uma destas ações será selecionada:<br /><br /> **Converter em desconhecido**. A chave é interpretada como um membro desconhecido. Essa é a configuração padrão.<br /><br /> **Descartar registro**. O registro é descartado.|  
||**Limite de erros de processamento**. Controla o número de erros processados selecionando uma das seguintes opções:<br /><br /> **Ignorar contagem de erros**. O processamento continuará independentemente do número de erros. <br />**Parar se houver erro**. Com esta opção, você controla duas configurações adicionais. **Número de erros** limita o processamento à ocorrência de um número específico de erros. **Ação se houver erro** permite determinar a ação a ser tomada quando o **Número de erros** for atingido. É possível selecionar **Parar processamento**para que o trabalho de processamento falhe e reverta todas as alterações ou **Parar log**para que o processamento continue sem registrar erros. **Parar se houver erro** é a configuração padrão com a opção **Número de erros** definida como **0** e **Ação se houver erro** está definido como **Parar processamento**.|  
||Condições de erro específicas. Você pode definir as seguintes opções para controlar o comportamento específico de tratamento de erros:<br /><br /> **Chave não encontrada**. Ocorre quando um valor de chave existe em uma partição, mas não existe na dimensão correspondente. A configuração padrão é **Relatar e continuar**. Outras configurações são **Ignorar erro** e **Relatar e parar**.<br /><br /> **Chave duplicada**. Ocorre quando mais de um valor de chave existe em uma dimensão. A configuração padrão é **Ignorar erro**. Outras configurações são **Relatar e continuar** e **Relatar e parar**.<br /><br /> **Chave nula convertida em desconhecida**. Ocorre quando um valor de chave é nulo e a opção **Ação do erro de chave** é definida como **Converter em desconhecido**. A configuração padrão é **Ignorar erro**. Outras configurações são **Relatar e continuar** e **Relatar e parar**.<br /><br /> **Chave nula não permitida**. Ocorre quando **Ação do erro de chave** é definido como **Descartar registro**. A configuração padrão é **Relatar e continuar**. Outras configurações são **Ignorar erro** e **Relatar e parar**.|  
  
## <a name="see-also"></a>Consulte também  
 [Processamento de objetos de modelo multidimensional](processing-a-multidimensional-model-analysis-services.md)  
  
  
