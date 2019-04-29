---
title: Configurar a memória disponível para aplicativos do Servidor de Relatório | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- memory [Reporting Services]
- memory thresholds [Reporting Services]
ms.assetid: ac7ab037-300c-499d-89d4-756f8d8e99f6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dcd685965d6a8265ac7d8cddeb4a319d0e95a338
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011042"
---
# <a name="configure-available-memory-for-report-server-applications"></a>Configurar memória disponível para aplicativos do Servidor de Relatórios
  Embora o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] possa usar toda a memória disponível, você pode substituir o comportamento padrão configurando um limite superior no valor total dos recursos de memória alocados a aplicativos do servidor do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Você também poderá definir limites que façam com que o servidor de relatório altere a maneira de priorizar e processar solicitações se a pressão de memória estiver baixa, média ou alta. Em níveis baixos de pressão de memória, o servidor de relatório responde dando uma prioridade ligeiramente mais alta a um processamento de relatório interativo ou sob demanda. Em níveis altos de pressão de memória, o servidor de relatório usa várias técnicas para permanecer operacional usando os recursos limitados disponíveis.  
  
 Este tópico descreve as definições de configuração que você pode especificar e como o servidor responde quando a pressão de memória torna-se um fator nas solicitações de processamento.  
  
## <a name="memory-management-policies"></a>Políticas de gerenciamento de memória  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] responde às restrições de recurso do sistema ajustando a quantidade de memória alocada a aplicativos e tipos de solicitações de processamentos específicos. Os aplicativos executados no serviço do Servidor de Relatório e sujeitos ao gerenciamento de memória incluem:  
  
-   O Gerenciador de Relatórios, um aplicativo front-end da Web para o servidor de relatório.  
  
-   O serviço Web Servidor de Relatórios, usado para processamento de relatório interativo e solicitações sob demanda.  
  
-   Um aplicativo de processamento em segundo plano, usado para manutenção de banco de dados, entrega de assinatura e processamento de relatório agendado.  
  
 As políticas de gerenciamento de memória aplicam-se ao serviço do Servidor de Relatório como um todo e não a aplicativos individuais executados no processo:  
  
 Se não houver pressão de memória no sistema, cada aplicativo do servidor solicita memória na inicialização, antecipadamente ao recebimento de solicitações, para obter desempenho ideal quando as solicitações forem finalmente recebidas. À medida que a pressão de memória aumenta, o servidor de relatório ajusta esse processo conforme descrito na tabela a seguir.  
  
|Pressão de memória|Resposta do servidor|  
|---------------------|---------------------|  
|Baixa|As solicitações atuais continuam sendo processadas. As novas solicitações são quase sempre aceitas. As solicitações direcionadas ao aplicativo de processamento em segundo plano recebem uma prioridade menor que as solicitações direcionadas ao serviço Web Servidor de Relatórios.|  
|Média|As solicitações atuais continuam sendo processadas. Novas solicitações podem ser aceitas. As solicitações direcionadas ao aplicativo de processamento em segundo plano recebem uma prioridade menor que as solicitações direcionadas ao serviço Web Servidor de Relatórios. As alocações de memória de todos os três aplicativos de servidor são reduzidas, com reduções relativamente maiores no processamento em segundo plano para tornar mais memória disponível para as solicitações de serviço Web.|  
|Alta|A alocação de memória é reduzida ainda mais. Os aplicativos de servidor que solicitam mais memória são negados. As solicitações atuais são retardadas e demoram mais tempo para serem concluídas. Novas solicitações não são aceitas. O servidor de relatório troca arquivos de dados na memória com o disco.<br /><br /> Se as restrições de memória se tornarem severas e não houver memória disponível para trabalhar com novas solicitações, o servidor de relatório retornará um erro de servidor indisponível HTTP 503 enquanto as solicitações estiverem sendo concluídas. Em alguns casos, os domínios de aplicativo podem ser imediatamente reciclados para reduzir a pressão de memória.|  
  
 Apesar de não ser possível personalizar as respostas de servidor de relatório em diferentes cenários de pressão de memória, você pode especificar as definições de configuração que definem os limites que separam as respostas de pressão de memória alta, média e baixa.  
  
## <a name="when-to-customize-memory-management-settings"></a>Quando personalizar as configurações de gerenciamento de memória  
 As configurações padrão especificam intervalos desiguais para pressão de memória baixa, média e alta. Por padrão, a zona de pressão de memória baixa é maior que as zonas média e alta. Essa configuração é ideal para processamento de cargas igualmente distribuídas que crescem ou diminuem incrementalmente. Nesse cenário, a transição entre zonas é gradual e o servidor de relatório tem hora para ajustar sua resposta.  
  
 Modificar as definições padrão será útil se o padrão de carga incluir picos. Quando há picos repentinos na carga de processamento, o servidor de relatório pode passar de nenhuma pressão de memória para falhas de alocação de memória muito rapidamente. Isso poderá acontecer se você tiver várias instâncias simultâneas de um relatório que consome bastante memória. Para trabalhar com esse tipo de carga de processamento, é necessário que o servidor de relatório passe para uma resposta de pressão de memória média ou alta o mais breve possível, de modo que ele possa desacelerar o processamento. Isso permite que mais solicitações sejam concluídas. Para fazer isso, você deve diminuir o valor de `MemorySafetyMargin` para tornar a zona de baixa pressão de memória menor em relação a outras zonas. Isso fará com que as respostas para pressão de memória média e alta ocorram anteriormente.  
  
## <a name="configuration-settings-for-memory-management"></a>Definições de configuração para gerenciamento de memória  
 As definições de configuração que controlam alocação de memória para o servidor de relatório incluem `WorkingSetMaximum`, `WorkingSetMinimum`, `MemorySafetyMargin` e `MemoryThreshold`.  
  
-   `WorkingSetMaximum` e `WorkingSetMinimum` definem o intervalo de memória disponível. Você pode configurar essas configurações para definir um intervalo de memória disponível para os aplicativos de servidor de relatório. Isso poderá ser útil se você estiver hospedando vários aplicativos no mesmo computador e determinar que o servidor de relatório está usando uma quantidade desproporcional de recursos do sistema para outros aplicativos no mesmo computador.  
  
-   `MemorySafetyMargin` e `MemoryThreshold` definem os limites para pressão de memória baixa, média e alta. Para cada estado, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] executa a ação corretiva para assegurar que o processamento de relatório e outras solicitações sejam tratados apropriadamente em relação à quantidade de memória disponível no computador. Você pode especificar as definições de configuração que determinam a delineação entre níveis de pressão baixa, média e alta.  
  
     Embora você possa alterar as definições de configuração, isso não melhorará desempenho de processamento de relatórios. Alterar as definições de configuração será útil apenas se as solicitações estiverem sendo descartadas antes de sua conclusão. A melhor maneira de melhorar o desempenho do servidor é implantando o servidor de relatório ou aplicativos individuais de servidor de relatório em computadores dedicados.  
  
 A ilustração a seguir mostra como as configurações são usadas em conjunto para distinguir entre níveis de pressão de memória baixa, média e alta.  
  
 ![Definições de configuração do estado de memória](../media/rs-memoryconfigurationzones.gif "Definições de configuração do estado de memória")  
  
 A tabela a seguir descreve as configurações `WorkingSetMaximum`, `WorkingSetMinimum`, `MemorySafetyMargin` e `MemoryThreshold`. As definições de configuração são especificadas no arquivo [RSReportServer.config](rsreportserver-config-configuration-file.md).  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`WorkingSetMaximum`|Especifica um limite de memória depois do qual nenhuma nova solicitação de alocação de memória é concedida a aplicativos de servidor de relatório.<br /><br /> Por padrão, o servidor de relatório define `WorkingSetMaximum` como a quantidade de memória disponível no computador. Esse valor é detectado quando o serviço é iniciado.<br /><br /> Essa configuração não aparece no arquivo RSReportServer.config a menos que você a adicione manualmente. Para que o servidor de relatório use menos memória, modifique o arquivo RSReportServer.config e adicione o elemento e o valor. O intervalo de valores válidos é de 0 ao inteiro máximo. Esse valor é expresso em quilobytes.<br /><br /> Quando o valor para `WorkingSetMaximum` for alcançado, o servidor de relatório não aceitará novas solicitações. As solicitações atualmente em progresso podem ser concluídas. Novas solicitações são aceitas apenas quando o uso da memória fica abaixo do valor especificado em `WorkingSetMaximum`.<br /><br /> Se solicitações existentes continuarem a consumir memória adicional após o valor `WorkingSetMaximum` ter sido alcançado, todos os domínios de aplicativo do servidor de relatório serão reciclados. Para obter mais informações, consulte [Application Domains for Report Server Applications](application-domains-for-report-server-applications.md).|  
|`WorkingSetMinimum`|Especifica um limite inferior para consumo de memória; o servidor de relatório não liberará memória se o uso de memória geral estiver abaixo desse limite.<br /><br /> Por padrão, o valor é calculado na inicialização do serviço. O cálculo é que a solicitação de alocação de memória inicial é de 60 por cento de `WorkingSetMaximum`.<br /><br /> Essa configuração não aparece no arquivo RSReportServer.config a menos que você a adicione manualmente. Se você quiser personalizar esse valor, será necessário adicionar o elemento `WorkingSetMinimum` ao arquivo RSReportServer.config. O intervalo de valores válidos é de 0 ao inteiro máximo. Esse valor é expresso em kilobytes.|  
|`MemoryThreshold`|Especifica uma porcentagem de `WorkingSetMaximum` que define o limite entre cenários de pressão média e alta. Se o uso da memória do servidor de relatório alcançar esse valor, o servidor de relatório reduzirá o processamento de solicitações e alterará a quantidade de memória alocada a diferentes aplicativos do servidor. O valor padrão é 90. Esse valor deve ser maior do que o valor definido para `MemorySafetyMargin`.|  
|`MemorySafetyMargin`|Especifica uma porcentagem de `WorkingSetMaximum` que define o limite entre cenários de pressão média e baixa. Esse valor é a porcentagem de memória disponível reservada para o sistema e não pode ser usado para operações de servidor de relatório. O valor padrão é 80.|  
  
> [!NOTE]  
>  As configurações `MemoryLimit` e `MaximumMemoryLimit` estão obsoletas no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores. Se você atualizou uma instalação existente ou estiver usando um arquivo RSReportServer.config que contenha essas configurações, o servidor de relatório não mais lerá esses valores.  
  
#### <a name="example-of-memory-configuration-settings"></a>Exemplo de definições de configuração de memória  
 O exemplo a seguir mostra as definições de configuração de um computador de servidor de relatório que usa valores de configuração de memória personalizados. Para adicionar `WorkingSetMaximum` ou `WorkingSetMinimum`, digite os elementos e os valores no arquivo RSReportServer.config. Ambos os valores são inteiros que expressam quilobytes de RAM que você está alocando aos aplicativos de servidor. O exemplo a seguir especifica que a alocação de memória total dos aplicativos de servidor de relatório não pode exceder 4 gigabytes. Se o valor padrão de `WorkingSetMinimum` (60% de `WorkingSetMaximum`) for aceitável, você poderá omiti-lo e especificar apenas `WorkingSetMaximum` no arquivo RSReportServer.config. Este exemplo inclui `WorkingSetMinimum` para mostrar como seria se você quisesse adicioná-lo:  
  
```  
      <MemorySafetyMargin>80</MemorySafetyMargin>  
      <MemoryThreshold>90</MemoryThreshold>  
      <WorkingSetMaximum>4000000</WorkingSetMaximum>  
      <WorkingSetMinimum>2400000</WorkingSetMinimum>  
```  
  
#### <a name="about-aspnet-memory-configuration-settings"></a>Sobre definições de configuração de memória ASP.NET  
 Embora o serviço Web Servidor de Relatórios e o Gerenciador de Relatórios sejam aplicativos do [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)], nenhum aplicativo responde às definições de configuração de memória especificadas na seção `processModel` de machine.config para aplicativos do [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] executados no modo de compatibilidade do IIS 5.0. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] lê as definições de configuração de memória somente no arquivo RSReportServer.config.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivo de configuração RSReportServer](rsreportserver-config-configuration-file.md)   
 [Arquivo de configuração RSReportServer](rsreportserver-config-configuration-file.md)   
 [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Application Domains for Report Server Applications](application-domains-for-report-server-applications.md)  
  
  
