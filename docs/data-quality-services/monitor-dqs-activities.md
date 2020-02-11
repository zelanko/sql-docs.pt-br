---
title: Monitorar atividade do DQS
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.administration.activitymonitoring.f1
helpviewer_keywords:
- monitoring activity
- activity monitoring
ms.assetid: 1d4c76f3-0d7b-498e-b792-4db4a0349814
author: swinarko
ms.author: sawinark
ms.openlocfilehash: d9926eb251d109eb8ed9529a4ae739e8a1915b07
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245464"
---
# <a name="monitor-dqs-activities"></a>Monitorar atividade do DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve como monitorar as seguintes atividades de modo centralizado no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS): descoberta de conhecimento, gerenciamento de domínio, política de correspondência, limpeza de dados, correspondência de dados e limpeza do SSIS.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
 Somente os usuários com a função dqs_administrator no banco de dados DQS_Main podem encerrar uma atividade ou interromper um processo em uma atividade.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
  
-   Você deve ter a função dqs_kb_editor ou dqs_kb_operator no banco de dados DQS_MAIN para exibir as atividades do DQS.  
  
-   Você deve ter a função dqs_administrator no banco de dados DQS_MAIN para encerrar uma atividade ou interromper um processo em uma atividade, além de exibir as atividades do DQS.  
  
##  <a name="View"></a>Exibir atividades do DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Monitoramento de Atividades**. A tela de monitoramento de atividades aparece.  
  
     ![Tela Monitoramento de Atividades](../data-quality-services/media/dqs-activitymonitoring.gif "Tela Monitoramento de Atividades")  
  
3.  A tela de monitoramento de atividades exibe informações sobre cada atividade executada em uma grade de atividade. A grade de atividade exibe as seguintes informações sobre cada atividade do DQS:  
  
     **ID**: um valor inteiro. Número de atividade exclusivo gerado pelo sistema para o monitoramento de atividades.  
  
     **Nome**: o nome da base de dados de conhecimento ou do projeto de qualidade do dado que é usado para esta atividade.  
  
     **Está ativo**: indica se a atividade está ativa no momento ou não. Ele pode ter os seguintes valores:  
  
    -   **Ativo**: a atividade está em execução no momento.  
  
    -   **Encerrado**: a atividade foi concluída.  
  
    -   **Encerrado**: a atividade foi encerrada usando a tela de monitoramento de atividades pelo administrador do DQS ou a atividade foi cancelada pelo usuário ao executá-la na [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]respectiva área de recursos no.  
  
     **Tipo**: indica o tipo de atividade. **Subtipo** indica o fluxo de trabalho específico que é executado para um tipo de atividade. Os seguintes tipos de atividades são monitorados:  
  
    -   Subtipos de **Gerenciamento de conhecimento** :  
  
        -   **Descoberta de conhecimento**  
  
        -   **Gerenciamento de domínio**  
  
        -   **Política de correspondência**  
  
    -   Subtipos de **projeto do DQ** :  
  
        -   **Limpeza**  
  
        -   **Combine**  
  
    -   Subtipos de **limpeza do SSIS** :  
  
        -   **Limpeza**  
  
     **Status atual**: indica o status atual de uma atividade. O status da atividade é determinado pelo último processo computacional. Observe que pode haver vários processos computacionais em uma atividade, como executar o processo de descoberta várias vezes (dentro da atividade de descoberta da base de dados de conhecimento). Portanto, o status pode ser alterado várias vezes durante o tempo de vida da atividade.  
  
     O **status atual** pode ter os seguintes valores:  
  
    -   **Em execução**: o processo computacional está em execução.  
  
    -   **Êxito**: esse status é definido antes que um processo computacional seja executado e novamente depois que um processo computacional terminar com êxito.  
  
    -   **Falha**: o processo computacional falhou.  
  
    -   **Parado**: o processo computacional foi interrompido.  
  
     **DQKB**: o nome da base de dados de conhecimento que é usada para a atividade.  
  
     **Usuário**: o nome do usuário que iniciou a atividade ou o último usuário que trabalhou na atividade (caso não sejam iguais).  
  
     **Hora de início da atividade**: a data e a hora em que a atividade foi iniciada  
  
     **Tempo decorrido**: o tempo decorrido desde que a atividade foi iniciada. Exibido na notação HH:MM:SS.  
  
     **Hora de término da atividade**: a data e a hora em que a atividade foi concluída.  
  
##  <a name="Filter"></a>Filtrar informações da atividade do DQS  
 Você pode usar o painel de filtragem (**Filtrar por**, **Valor**, **Data Inicial**, e **Data Final**) na tela de monitoramento de atividades para filtrar e exibir as atividades necessárias com base em um critério de filtro específico. Para filtrar registros de atividade:  
  
1.  Decida o critério de filtragem: se você deseja filtrar os registros de atividade com base no valor de uma das colunas na grade de atividade (baseada em valor), com base em um intervalo de datas ou ambos.  
  
    1.  **Filtragem baseada em valor**: selecione um critério de filtro na lista **Filtrar por** e, em seguida, selecione o valor apropriado a ser filtrado na lista **valor** . Ao selecionar uma opção na lista **Filtrar por** , a lista **Valor** será atualizada com os valores possíveis. Você pode realizar a filtragem com base nos seguintes campos dos registros de atividade: **Está Ativo**, **Tipo**, **Subtipo**, **Status Atual**, **DQKB**e **Usuário**.  
  
    2.  **Filtragem baseada em intervalo de data**: selecionando datas apropriadas nos controles **de data de** data e **até data** . Por padrão, a data exibida em **Data Inicial** é dois dias antes da data atual, e a data exibida em **Data Final** é a data atual. A filtragem não é feita com base nas datas *inicial* e *final* , mas no intervalo. Isso significa que cada atividade que estava sendo executada durante o intervalo de datas selecionado será exibida.  
  
2.  Clique no ícone **Atualizar a lista de atividades** para aplicar a filtragem e exibir apenas as atividades de DQS filtradas.  
  
##  <a name="ActivityDetails"></a>Exibir detalhes da atividade do DQS  
 Você pode exibir as informações detalhadas de uma atividade de DQS; por exemplo, as etapas da atividade e as informações do criador de perfil na tela de monitoramento de atividades. Para fazer isso:  
  
1.  Selecione uma atividade de DQS na grade de atividade (no painel superior).  
  
2.  O painel inferior exibe os detalhes de atividade selecionada nas duas guias a seguir:  
  
    -   **Etapas da atividade**: exibe uma grade dos processos computacionais (etapas da atividade) associados à atividade selecionada. Pode haver várias etapas de atividade exibidas para uma atividade sob essa guia. Isso pode acontecer caso a mesma etapa de atividade dentro da atividade tenha sido executada várias vezes pelo usuário. Por exemplo, a etapa de atividade foi interrompida e iniciada novamente. A grade desta guia exibe as seguintes informações sobre cada etapa associada à atividade: **Tipo**, **Status Atual**, **Hora de Início**, **Tempo Decorrido**e **Hora de Término**.  
  
    -   **Criador de perfil**: exibe as informações de criação de perfil para atividades atuais e históricas. Para atividades atuais, contém informações parciais, mas consistentes. As informações de perfil de uma atividade são exportadas para um arquivo do Excel quando você exporta os detalhes de atividade correspondentes para um arquivo do Excel. As informações estão disponíveis nas planilhas **Criador de Perfil – Origem** e **Criador de Perfil – Campos** no arquivo do Excel exportado.  
  
##  <a name="Export"></a>Exportar detalhes da atividade do DQS  
 Você pode exportar as propriedades da atividade, os processos da atividade e as informações de perfil de uma atividade na tela de monitoramento para um arquivo do Excel. Para fazer isso:  
  
1.  Selecione uma atividade na grade de atividade (no painel superior).  
  
2.  Clique no ícone **Exportar a atividade selecionada para o Excel** . Se desejar, clique com o botão direito do mouse em qualquer atividade na grade de atividade e clique em **Exportar Atividade** no menu de atalho.  
  
3.  Você é solicitado a especificar um nome e local para o arquivo do Excel a ser salvo. O arquivo do Excel exportado contém as seguintes planilhas:  
  
    |Nome da planilha|DESCRIÇÃO|  
    |----------------|-----------------|  
    |Atividade|Contém informações (colunas) sobre a atividade como na grade de atividade.|  
    |Processos|Contém informações (colunas) sobre os processos da atividade como na guia **Etapas da Atividade** .|  
    |Criador de Perfil - Origem|Para o subtipo **Limpeza** , contém as seguintes informações sobre a atividade: Registros, Registros Corretos, Registros Corrigidos e Registros Inválidos.<br /><br /> Para os subtipos **Descoberta da Base de Dados de Conhecimento**, **Gerenciamento de Domínio**, **Política de Correspondência**e **Correspondência** , contém as seguintes informações sobre a atividade: Registros, Valores Totais, Novo Valores, Valores Exclusivos e Novos Valores Exclusivos.|  
    |Criador de Perfil - Campos|Para os subtipos **Limpeza** e **Limpeza do SSIS** , contém as seguintes informações sobre a atividade: Campo, Domínio, Valores Corrigidos, Valores Sugeridos, Integridade e Precisão.<br /><br /> Para os subtipos **Descoberta da Base de Dados de Conhecimento**, **Gerenciamento de Domínio**, **Política de Correspondência**e **Correspondência** , contém as seguintes informações sobre a atividade: Campo, Domínio, Novo, Exclusivo, Válido no Domínio e Integridade.|  
  
##  <a name="Terminate"></a>Encerrar uma atividade do DQS  
 Os administradores de DQS (função dqs_administrator) podem encerrar uma atividade (ativa) em execução que não é do tipo **Limpeza do SSIS**. O encerramento de uma atividade interromperá todos os processos em execução na atividade e removerá tudo que estiver relacionado à atividade. Essa operação não pode ser desfeita. Encerrar uma atividade na tela de monitoramento de atividades é equivalente a cancelar a respectiva atividade clicando em **Cancelar** durante sua execução na área de recurso no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Para encerrar uma atividade:  
  
1.  Selecione uma atividade em execução na grade de atividade (no painel superior).  
  
2.  Clique no ícone **Encerrar a atividade selecionada** . Se desejar, clique com o botão direito do mouse na atividade na grade de atividade e clique em **Encerrar Atividade** no menu de atalho.  
  
3.  Uma mensagem é exibida para confirmar sua ação. Clique em **Sim**.  
  
##  <a name="Stop"></a>Parar um processo na atividade do DQS  
 Os administradores de DQS (função dqs_administrator) podem interromper um processo (ativo) em execução em uma atividade que não é do tipo **Limpeza do SSIS**. Interromper um processo na tela de monitoramento de atividades é equivalente a interromper o processo na respectiva atividade na área de recurso do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Por exemplo, interromper o processo de limpeza assistido por computador em uma atividade de limpeza ou interromper o processo correspondente em uma atividade correspondente. Um processo interrompido não pode ser reiniciado na tela de monitoramento de atividades. Você precisará reiniciar o processo na respectiva área de recurso do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Nesse caso, uma linha adicional é adicionada à grade processos na guia etapas da **atividade** . O status de processo interrompido continua a exibir **parado**. Para interromper um processo:  
  
1.  Selecione um processo em execução na grade de detalhes da atividade (no painel inferior).  
  
2.  Clique no ícone **Parar o processo selecionado** . Se desejar, clique com o botão direito do mouse no processo na grade de detalhes da atividade e clique em **Parar Processo** no menu de atalho.  
  
3.  Uma mensagem é exibida para confirmar sua ação. Clique em **Sim**.  
  
  
