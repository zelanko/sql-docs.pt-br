---
title: Ferramentas de solução de problemas para desenvolvimento de pacotes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: 41dd248c-dab3-4318-b8ba-789a42d5c00c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 43eed16aa9cd69d70f308c3ce397720020446fdd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62885565"
---
# <a name="troubleshooting-tools-for-package-development"></a>Solucionando problemas de ferramentas para desenvolvimento de pacotes
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui recursos e ferramentas que podem ser usados para solucionar problemas de pacotes enquanto você os estiver desenvolvendo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="troubleshooting-design-time-validation-issues"></a>Solucionando problemas de validação de tempo de design  
 Na versão atual do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], quando um pacote é aberto, o sistema valida todas as conexões antes de validar todo os componentes de fluxo de dados e define as conexões que são lentas ou indisponíveis para trabalhar offline. Isto ajuda a reduzir o atraso na validação do fluxo de dados do pacote.  
  
 Depois que um pacote é aberto, você também pode desativar uma conexão clicando com o botão direito do mouse no gerenciador de conexões na área **Gerenciadores de Conexões** e clicando em **Trabalhar Offline**. Isto pode acelerar as operações no Designer SSIS.  
  
 As conexões que foram definidas para trabalhar offline permanecerão offline até que você faça o seguinte:  
  
-   Teste a conexão clicando com o botão direito do mouse no gerenciador de conexões na área **Gerenciadores de Conexões** do Designer SSIS e clicando em **Testar Conectividade**.  
  
     Por exemplo, uma conexão é definida inicialmente para trabalhar offline quando o pacote é aberto. Você modifica a cadeia de conexão para resolver o problema e clica em **Testar Conectividade** para testar a conexão.  
  
-   Reabra o pacote ou reabra o projeto que contém o pacote. A validação é executada novamente em todas as conexões no pacote.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui os recursos adicionais a seguir para ajudar a evitar erros de validação:  
  
-   **Definir todos os pacotes e todas as conexões para trabalhar offline quando as fontes de dados não estiverem disponíveis**. Você pode habilitar **Trabalhar Offline** no menu **SSIS** . Ao contrário do `DelayValidation` propriedade, o **Trabalhar Offline** opção está disponível antes mesmo de você abre um pacote. Você também pode habilitar a opção **Trabalhar Offline** para acelerar as operações no designer e a desabilitar apenas quando você desejar validar seu pacote.  
  
-   **Configure a propriedade DelayValidation em elementos do pacote que não são válidos até o tempo de execução**. Você pode definir `DelayValidation` como `True` em elementos do pacote cujas configurações não são válidas no tempo de design para evitar erros de validação. Por exemplo, você pode ter uma tarefa Fluxo de Dados que usa uma tabela de destino que não existe até que uma tarefa Executar SQL crie a tabela no tempo de execução. A propriedade `DelayValidation` pode ativada no nível do pacote ou no nível das tarefas individuais e contêineres que o pacote inclui. Normalmente, ao implantar o pacote, você deve deixar esta propriedade definida como `True` nos mesmos elementos do pacote, para evitar os mesmos erros de validação no tempo de execução.  
  
     A propriedade `DelayValidation` pode ser definida em uma tarefa de Fluxo de Dados, mas não em componentes de fluxo de dados individuais. Você pode conseguir um efeito semelhante definindo a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> dos componentes de fluxo de dados individuais como `false`. Entretanto, quando o valor dessa propriedade for `false`, o componente não reconhecerá as alterações para o metadados de fontes de dados externas.  
  
 Se os objetos de banco de dados que forem usados pelo pacote estiverem bloqueados durante a validação, o processo poderá ser interrompido. Nestas circunstâncias, o [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer também para de responder. Você pode retomar a validação usando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para encerrar a sessão associada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você também pode evitar este problema usando as configurações descritas nesta seção.  
  
## <a name="troubleshooting-control-flow"></a>Solucionando problemas de fluxo de controle  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui os seguintes recursos e ferramentas que você pode usar para solucionar problemas do fluxo de controle em pacotes durante o desenvolvimento de pacotes:  
  
-   **Definir pontos de interrupção em tarefas, contêineres e pacote**. Você pode definir pontos de interrupção usando as ferramentas gráficas fornecidas pelo [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Os pontos de interrupção podem ser habilitados no nível do pacote, ou no nível das tarefas individuais e contêineres que o pacote inclui. Algumas tarefas e contêineres fornecem condições de interrupção adicionais para definir os pontos de interrupção. Por exemplo, você pode habilitar uma condição de interrupção no contêiner Loop For que suspende a execução no início de cada iteração do loop.  
  
-   **Usar janelas de depuração**. Quando você executa um pacote que tem pontos de interrupção, as janelas de depuração do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornecem acesso a valores de variáveis e mensagens de status.  
  
-   **Analisar as informações na guia Progresso**. [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer fornece informações adicionais sobre fluxo de controle quando você executa um pacote no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. A guia Progresso lista tarefas e contêineres em ordem de execução e inclui horários de início e término, avisos e mensagens de erro para cada tarefa e contêiner, inclusive do próprio pacote.  
  
 Para obter mais informações sobre esses recursos, consulte [Debugging Control Flow](debugging-control-flow.md).  
  
## <a name="troubleshooting-data-flow"></a>Solucionando problemas de fluxo de dados  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui os seguintes recursos e ferramentas que você pode usar para solucionar problemas do fluxo de dados em pacotes durante desenvolvimento de pacotes:  
  
-   **Testar com apenas um subconjunto de seus dados**. Se você quiser solucionar problemas de fluxo de dados em um pacote usando apenas uma amostra do conjunto de dados, poderá incluir uma transformação Amostragem Percentual ou Amostragem de Linhas para criar uma amostra de dados embutida no tempo de execução. Para obter mais informações, consulte [Percentage Sampling Transformation](../data-flow/transformations/percentage-sampling-transformation.md) e [Row Sampling Transformation](../data-flow/transformations/row-sampling-transformation.md).  
  
-   **Usar visualizadores de dados para monitorar dados enquanto se movimentam pelo fluxo de dados**. Os visualizadores de dados exibem valores de dados enquanto os dados se movimentam entre fontes, transformações e destinos. Um visualizador de dados pode exibir dados em uma grade. Você pode copiar os dados de um visualizador de dados para a Área de transferência e colar os dados em um arquivo ou planilha do Excel. Para obter mais informações, consulte [Adicionar um visualizador de dados para um fluxo de dados](../add-a-data-viewer-to-a-data-flow.md).  
  
-   **Configurar saídas de erro em componentes de fluxo de dados que dá suporte a saídas de erro**. Muitas fontes de fluxo de dados, transformações e destinos também dão suporte a saídas de erro. Configurando a saída de erro de um componente de fluxo de dados, você pode direcionar os dados que contêm erros a um destino diferente. Por exemplo, você pode capturar os dados com falha ou que estavam truncados em um arquivo de texto separado. Além disso, pode anexar visualizadores de dados às saídas de erro e examinar somente os dados errados. No tempo de design, as saídas de erro capturam valores de dados problemáticos para ajudar você a desenvolver pacotes que lidam efetivamente com dados reais. Porém, enquanto outras ferramentas de solução de problemas e recursos são úteis apenas no tempo de design, as saídas de erro mantêm sua utilidade no ambiente de produção. Para obter mais informações, consulte [Tratamento de erros em dados](../data-flow/error-handling-in-data.md).  
  
-   **Capturar a contagem das linhas processadas**. Quando você executa um pacote no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer o número de linhas que passaram por um caminho é exibido no designer do fluxo de dados. Este número é atualizado periodicamente enquanto os dados se movimentam pelo caminho. Você também pode adicionar uma transformação Contagem de Linhas ao fluxo de dados para capturar a contagem final de linhas em uma variável. Para obter mais informações, consulte [Row Count Transformation](../data-flow/transformations/row-count-transformation.md).  
  
-   **Analisar as informações na guia Progresso**. [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer fornece informações adicionais sobre fluxos de dados quando você executa um pacote no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. A guia Progresso lista componentes de fluxo de dados em ordem de execução e inclui informações sobre o progresso para cada fase do pacote, exibida como um percentual completo, e o número de linhas gravadas no destino.  
  
 Para obter mais informações sobre esses recursos, consulte [Debugging Data Flow](debugging-data-flow.md).  
  
## <a name="troubleshooting-scripts"></a>Solucionando problemas de scripts  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] O VSTA (Tools for Applications) é o ambiente de desenvolvimento no qual você grava os scripts usados pela tarefa Script e pelo componente Script. O VSTA inclui os seguintes recursos e ferramentas que você pode usar para solucionar problemas de scripts durante o desenvolvimento de pacotes:  
  
-   **Definir os pontos de interrupção em scripts nas tarefas Script.** O VSTA dá suporte à depuração somente para scripts na tarefa Script. Os pontos de interrupção definidos nas tarefas Script são integrados aos pontos de interrupção definidos nos pacotes e às tarefas e contêineres do pacote, habilitando a depuração contínua de todos os elementos do pacote.  
  
    > [!NOTE]  
    >  Quando você depura um pacote que contém várias tarefas Script, o depurador acessa os pontos de interrupção em apenas uma tarefa Script e ignora os pontos de interrupção em outras tarefas Script. Se uma tarefa Script fizer parte de um contêiner Loop Foreach ou Loop For, o depurador ignorará os pontos de interrupção na tarefa Script depois da primeira iteração do loop.  
  
 Para obter mais informações, consulte [Debugging Script](debugging-script.md). Para obter sugestões sobre como depurar o componente Script, consulte [codificando e depurando o componente Script] (... / extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md.  
  
## <a name="troubleshooting-errors-without-a-description"></a>Solucionando problemas de erros sem uma descrição  
 Se você encontrar um número de erro do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sem a respectiva descrição durante o desenvolvimento de pacotes, poderá localizar a descrição em [Referência de mensagens e erros do Integration Services](../integration-services-error-and-message-reference.md). No momento, a lista não inclui informações para solução de problemas.  
  
## <a name="see-also"></a>Consulte também  
 [Solucionando problemas de ferramentas para execução de pacotes](troubleshooting-tools-for-package-execution.md)   
 [Data Flow Performance Features](../data-flow/data-flow-performance-features.md)  
  
  
