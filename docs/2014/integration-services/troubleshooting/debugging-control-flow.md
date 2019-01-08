---
title: Depurando o fluxo de controle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- progress reporting [Integration Services]
- breakpoints [Integration Services]
- debugging [Integration Services], control flow
- control flow [Integration Services], debugging
- color-coded progress reporting [Integration Services]
- Set Breakpoints dialog box
ms.assetid: 54a458cc-9f4f-4b48-8cf2-db2e0fa7756c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 786ede341e899acf2831c5c3e0a6204d3a80b1b6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791938"
---
# <a name="debugging-control-flow"></a>Depurando o fluxo de controle
  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] include features e o tools that you can use to troubleshoot the control flow in an [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .  
  
-   [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] oferece suporte a pontos de interrupção em contêineres e tarefas.  
  
-   [!INCLUDE[ssIS](../../../includes/ssis-md.md)] fornece relatórios de progresso em tempo de execução.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] fornece janelas de depuração.  
  
## <a name="breakpoints"></a>Pontos de interrupção  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] fornece a caixa de diálogo **Definir Pontos de Interrupção** , na qual você pode definir pontos de interrupção ao habilitar as condições de interrupção e especificando o número de vezes que um ponto de interrupção pode ocorrer antes que a execução do pacote seja anulada. Os pontos de interrupção podem ser habilitados no nível do pacote ou no nível do componente individual. Se as condições da interrupção estiverem habilitadas no nível da tarefa ou contêiner, o ícone do ponto de interrupção aparecerá próximo à tarefa ou contêiner sobre a superfície de design da guia **Fluxo de Controle** . Se as condições de interrupção estiverem habilitadas no pacote, o ícone de ponto de interrupção aparecerá no rótulo da guia **Fluxo de Controle** .  
  
 Quando um ponto de interrupção é atingido, o ícone de ponto de interrupção muda para ajudá-lo a identificar a fonte do ponto de interrupção. Você pode adicionar, excluir e alterar pontos de interrupção quando o pacote estiver executando.  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] fornece dez pontos de interrupção que você pode habilitar em todas as tarefas e contêineres. Na caixa de diálogo **Definir Pontos de Interrupção** , você pode habilitar os pontos de interrupção das seguintes condições:  
  
|Condição de interrupção|Descrição|  
|---------------------|-----------------|  
|Quando a tarefa ou o contêiner recebe o evento `OnPreExecute`.|Chamado quando uma tarefa está prestes a ser executada. Este evento é criado por uma tarefa ou contêiner imediatamente antes da sua execução.|  
|Quando a tarefa ou o contêiner recebe o evento `OnPostExecute`.|Chamado imediatamente após a execução lógica do término da tarefa. Este evento é criado por uma tarefa ou contêiner imediatamente após sua execução.|  
|Quando a tarefa ou o contêiner recebe o evento `OnError`.|Chamado por uma tarefa ou contêiner quando ocorre um erro.|  
|Quando a tarefa ou o contêiner recebe o evento `OnWarning`.|Chamado quando a tarefa está em um estado que não justifica um erro, mas autoriza uma advertência.|  
|Quando a tarefa ou o contêiner recebe o evento `OnInformation`.|Chamado quando a tarefa é exigida a fornecer informações.|  
|Quando a tarefa ou o contêiner recebe o evento `OnTaskFailed`.|Chamado pelo host de tarefa quando ele falha.|  
|Quando a tarefa ou o contêiner recebe o evento `OnProgress`.|Chamado para atualizar o progresso da execução de tarefa.|  
|Quando a tarefa ou o contêiner recebe o evento `OnQueryCancel`.|Chamado a qualquer momento do processamento da tarefa quando você pode cancelar execução.|  
|Quando a tarefa ou o contêiner recebe o evento `OnVariableValueChanged`.|Chamado pelo tempo de execução [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] quando o valor de uma variável muda. O RaiseChangeEvent da variável deve ser definido como `true` para gerar este evento.<br /><br /> **\*\* Aviso \*\*** A variável associada a esse ponto de interrupção deve ser definida no escopo de **contêiner** . Se a variável for definida ao escopo de pacote, o ponto de interrupção não será atingido.|  
|Quando a tarefa ou o contêiner recebe o evento `OnCustomEvent`.|Chamado por tarefas para gerar eventos personalizados definidos por tarefa.|  
  
 Além das condições dos pontos de interrupção disponíveis a todas as tarefas e contêineres, algumas tarefas e contêineres incluem condições especiais de interrupção para definir os pontos de interrupção. Por exemplo, você pode habilitar uma condição de interrupção no contêiner Loop For que defina um ponto de interrupção que suspenda a execução no início de cada iteração do loop.  
  
 Para adicionar flexibilidade e força ao ponto de interrupção, você pode modificar o comportamento de um ponto de interrupção especificando as seguintes condições:  
  
-   A contagem de ocorrência ou o número máximo de vezes que uma condição de interrupção ocorre antes de a execução ser suspensa.  
  
-   O tipo de contagem de ocorrência ou a regra que especifica o momento em que a condição de interrupção aciona o ponto de interrupção.  
  
 Os tipos de contagem de ocorrência, com exceção do tipo Sempre, são sempre qualificados pela contagem de ocorrência. Por exemplo, se o tipo for "Contagem de ocorrências igual a" e a contagem de ocorrência for 5, a execução é suspensa na sexta ocorrência da condição da interrupção.  
  
 A tabela a seguir descreve os tipos de contagem de ocorrência.  
  
|Tipo de contagem de ocorrências|Descrição|  
|--------------------|-----------------|  
|Always|A execução será sempre suspensa quando ocorrer o ponto de interrupção.|  
|Contagem de ocorrências igual a|A execução será suspensa quando o número de vezes que o ponto de interrupção ocorreu for igual à contagem de ocorrências.|  
|Contagem de ocorrências maior que ou igual a|A execução será suspensa quando o número de vezes que o ponto de interrupção ocorreu for igual ou maior que a contagem de ocorrências.|  
|Várias contagens de ocorrências|A execução será suspensa quando ocorrerem várias contagens de ocorrências. Por exemplo, se você definir esta opção como 5, a execução será suspensa a cada quinta vez.|  
  
#### <a name="to-set-breakpoints"></a>Para definir pontos de interrupção  
  
-   [Depurar um pacote por meio da definição de pontos de interrupção em uma tarefa ou contêiner](../debug-a-package-by-setting-breakpoints-on-a-task-or-a-container.md)  
  
## <a name="progress-reporting"></a>Relatório de progresso  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] O Designer inclui dois tipos de relatórios de progresso: codificação de cores na superfície de design da guia **Fluxo de Controle** e mensagens de progresso na guia **Progresso** .  
  
 Quando você executa um pacote, o Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] descreve o progresso da execução exibindo cada tarefa ou contêiner usando uma cor que indica o seu status. Você pode identificar pela cor se o elemento está esperando para ser executado, está em execução, terminou com sucesso ou terminou sem-sucesso. Depois que você parar a execução de pacote, a codificação de cor desaparece.  
  
 A tabela a seguir descreve as cores usadas para indicar o estado de execução.  
  
|Cor|Status de execução|  
|-----------|----------------------|  
|Cinza|Esperando para executar|  
|Amarelo|Executando|  
|Verde|Executado com sucesso|  
|realçado|Executado com erros|  
  
 A guia **Progresso** exibe as tarefas e contêineres na ordem de execução e inclui os tempos de início e fim, avisos e mensagens de erro. Depois que você parar a execução do pacote, as informações de progresso continuarão disponíveis na guia **Resultados da Execução** .  
  
> [!NOTE]  
>  Para habilitar ou desabilitar a exibição de mensagens na guia **Progresso** , marque ou desmarque a opção **Depurar Relatório do Progresso** no menu **SSIS** .  
  
 O diagrama a seguir mostra a guia **Progresso** .  
  
 ![Guia Progresso do Designer do SSIS](../media/mw-dtsflow04.gif "Progress tab of SSIS Designer")  
  
## <a name="debug-windows"></a>Janelas de depuração  
 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] inclui muitas janelas que você pode usar para trabalhar com pontos de interrupção e para depurar pacotes contendo pontos de interrupção. Para aprender mais sobre cada janela, abra a janela e, então, pressione F1 para exibir a Ajuda da janela.  
  
 Para abrir essas janelas no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], clique no menu **Depurar** , aponte para **Janelas**, e, então, clique em **Pontos de Interrupção**, **Saída**ou **Imediato**.  
  
 A tabela a seguir descreve as janelas.  
  
|Janela|Descrição|  
|------------|-----------------|  
|Pontos de interrupção|Exibe os pontos de interrupção em um pacote e fornece opções para habilitar e excluir pontos de interrupção.|  
|Saída|Exibe mensagens de status dos recursos no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].|  
|Imediato|Usado para depurar e avaliar expressões e imprimir valores variáveis.|  
  
## <a name="see-also"></a>Consulte também  
 [Solucionando problemas de ferramentas para desenvolvimento de pacotes](troubleshooting-tools-for-package-development.md)  
  
  
