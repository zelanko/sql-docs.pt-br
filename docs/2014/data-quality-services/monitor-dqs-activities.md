---
title: Monitorar as atividades do DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.administration.activitymonitoring.f1
helpviewer_keywords:
- monitoring activity
- activity monitoring
ms.assetid: 1d4c76f3-0d7b-498e-b792-4db4a0349814
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a44434be6f3908ebf7837a80b188affe226d88f3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035157"
---
# <a name="monitor-dqs-activities"></a>Monitorar atividade do DQS
  Este tópico descreve como monitorar as seguintes atividades de modo centralizado no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS): descoberta de conhecimento, gerenciamento de domínio, política de correspondência, limpeza de dados, correspondência de dados e limpeza do SSIS.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="LimitationsRestrictions"></a> Limitações e Restrições  
 Somente os usuários com a função dqs_administrator no banco de dados DQS_Main podem encerrar uma atividade ou interromper um processo em uma atividade.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
  
-   Você deve ter a função dqs_kb_editor ou dqs_kb_operator no banco de dados DQS_MAIN para exibir as atividades do DQS.  
  
-   Você deve ter a função dqs_administrator no banco de dados DQS_MAIN para encerrar uma atividade ou interromper um processo em uma atividade, além de exibir as atividades do DQS.  
  
##  <a name="View"></a> Exibir atividades do DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Monitoramento de Atividades**. A tela de monitoramento de atividades aparece.  
  
     ![Tela de Monitoramento de Atividades](../../2014/data-quality-services/media/dqs-activitymonitoring.gif "Activity Monitoring screen")  
  
3.  A tela de monitoramento de atividades exibe informações sobre cada atividade executada em uma grade de atividade. A grade de atividade exibe as seguintes informações sobre cada atividade do DQS:  
  
    |Informações|Descrição|  
    |-----------------|-----------------|  
    |**ID**|Um valor inteiro. Número de atividade exclusivo gerado pelo sistema para o monitoramento de atividades.|  
    |**Nome**|O nome da base de dados de conhecimento ou do projeto de qualidade de dados usado para esta atividade.|  
    |**Está ativo**|Indica se a atividade está ativa no momento ou não. Pode ter um dos valores a seguir:<br /><br /> **Active Directory**: Atividade está sendo executado.<br /><br /> **finalizada**: Atividade está concluída.<br /><br /> **Encerrada**: Atividade foi encerrada usando a tela de monitoramento de atividade pelo administrador de DQS ou a atividade foi cancelada pelo usuário durante sua execução na respectiva área de recurso no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].|  
    |**Tipo**|Indica o tipo da atividade. Seguintes tipos de atividades são monitorados: **Gerenciamento de conhecimentos**, **projeto do DQ**, e **limpeza do SSIS**.|  
    |**Subtipo**|Indica o fluxo de trabalho específico executado para um tipo de atividade.<br /><br /> Um **gerenciamento de Conhecimento** tipo de atividade pode ter os seguintes fluxos de trabalho ou subtipos: **Descoberta de Conhecimento**, **gerenciamento de domínio**, e **política de correspondência**.<br /><br /> Um **projeto do DQ** tipo de atividade pode ter os seguintes fluxos de trabalho ou subtipos: **Limpeza** e **correspondência**.<br /><br /> O tipo de atividade **Limpeza do SSIS** pode ter apenas um fluxo de trabalho ou subtipo **Limpeza** .|  
    |**Status atual**|Indica o status atual de uma atividade. O status da atividade é determinado pelo último processo computacional. Pode ter um dos valores a seguir:<br /><br /> **Executando**: O processo computacional está em execução.<br /><br /> **Êxito**: Antes de qualquer processo computacional ser executado, o status é definido como **bem-sucedido**. Novamente, depois de qualquer processo ser finalizado com êxito, o status é definido como **Êxito**.<br /><br /> **Falha ao**: Falha no processo computacional.<br /><br /> **Parado**: O processo computacional foi interrompido.<br /><br /> <br /><br /> Observação: Pode haver vários processos computacionais em uma atividade, como executar o processo de descoberta várias vezes (dentro da atividade de descoberta da base de dados de conhecimento). Portanto, o status pode ser alterado várias vezes durante o tempo de vida da atividade.|  
    |**DQKB**|O nome da base de dados de conhecimento usada para a atividade.|  
    |**Usuário**|O nome do usuário que iniciou a atividade ou o último usuário que trabalhou na atividade (caso não sejam os mesmos).|  
    |**Hora de início da atividade**|A data e a hora em que a atividade foi iniciada.|  
    |**Tempo decorrido**|O tempo decorrido desde que a atividade foi iniciada. Exibido na notação HH:MM:SS.|  
    |**Hora de término da atividade**|A data e a hora em que a atividade foi finalizada.|  
  
##  <a name="Filter"></a> Filtrar informações da atividade do DQS  
 Você pode usar o painel de filtragem (**Filtrar por**, **Valor**, **Data Inicial**, e **Data Final**) na tela de monitoramento de atividades para filtrar e exibir as atividades necessárias com base em um critério de filtro específico. Para filtrar registros de atividade:  
  
1.  Decida o critério de filtragem: se você deseja filtrar os registros de atividade com base no valor de uma das colunas na grade de atividade (baseada em valor), com base em um intervalo de datas ou ambos.  
  
    1.  **Filtragem baseada em valor**: Selecione um critério de filtro na **filtrar por** lista e, em seguida, selecione o valor apropriado pelo qual filtrar na **valor** lista. Ao selecionar uma opção na lista **Filtrar por** , a lista **Valor** será atualizada com os valores possíveis. Você pode filtrar pelos seguintes campos nos registros de atividades: **Está ativo**, **tipo**, **subtipo**, **Status atual**, **DQKB**, e **usuário**.  
  
    2.  **Filtragem baseada em intervalo de datas**: Seleção das datas apropriadas nos **data de início** e **até a data** controles de data. Por padrão, a data exibida em **Data Inicial** é dois dias antes da data atual, e a data exibida em **Data Final** é a data atual. A filtragem não é feita com base nas datas *inicial* e *final* , mas no intervalo. Isso significa que cada atividade que estava sendo executada durante o intervalo de datas selecionado será exibida.  
  
2.  Clique no ícone **Atualizar a lista de atividades** para aplicar a filtragem e exibir apenas as atividades de DQS filtradas.  
  
##  <a name="ActivityDetails"></a> Exibir detalhes da atividade do DQS  
 Você pode exibir as informações detalhadas de uma atividade de DQS; por exemplo, as etapas da atividade e as informações do criador de perfil na tela de monitoramento de atividades. Para fazer isso:  
  
1.  Selecione uma atividade de DQS na grade de atividade (no painel superior).  
  
2.  O painel inferior exibe os detalhes de atividade selecionada nas duas guias a seguir:  
  
    -   **Etapas da atividade**: Exibe uma grade dos processos computacionais (etapas da atividade) que estão associados com a atividade selecionada. Pode haver várias etapas exibidas para uma atividade nesta guia. Isso pode acontecer caso a mesma etapa da atividade tenha sido executada várias vezes pelo usuário. Por exemplo, a etapa de atividade foi interrompida e iniciada novamente. A grade desta guia exibe as seguintes informações sobre cada etapa associada à atividade: **Tipo de**, **Status atual**, **hora de início**, **tempo decorrido**, e **hora de término**.  
  
    -   **Profiler**: Exibe as informações de criação de perfil para atividades atuais e históricas. Para atividades atuais, contém informações parciais, mas consistentes. As informações de perfil de uma atividade são exportadas para um arquivo do Excel quando você exporta os detalhes de atividade correspondentes para um arquivo do Excel. As informações estão disponíveis nas planilhas **Criador de Perfil – Origem** e **Criador de Perfil – Campos** no arquivo do Excel exportado.  
  
##  <a name="Export"></a> Exportar detalhes da atividade do DQS  
 Você pode exportar as propriedades da atividade, os processos da atividade e as informações de perfil de uma atividade na tela de monitoramento para um arquivo do Excel. Para fazer isso:  
  
1.  Selecione uma atividade na grade de atividade (no painel superior).  
  
2.  Clique no ícone **Exportar a atividade selecionada para o Excel** . Se desejar, clique com o botão direito do mouse em qualquer atividade na grade de atividade e clique em **Exportar Atividade** no menu de atalho.  
  
3.  Você é solicitado a especificar um nome e local para o arquivo do Excel a ser salvo. O arquivo do Excel exportado contém as seguintes planilhas:  
  
    |Nome da planilha|Descrição|  
    |----------------|-----------------|  
    |Atividade|Contém informações (colunas) sobre a atividade como na grade de atividade.|  
    |Processos|Contém informações (colunas) sobre os processos da atividade como na guia **Etapas da Atividade** .|  
    |Criador de Perfil - Origem|Para o **limpeza** subtipo, contém as seguintes informações sobre a atividade:   Registros, registros corretos, registros corrigidos e registros inválidos.<br /><br /> Para **descoberta de Conhecimento**, **gerenciamento de domínio**, **política de correspondência**, e **correspondentes** subtipos, contém o seguinte informações sobre a atividade:   Registros, valores totais, novo valores, valores exclusivos e novos valores exclusivos.|  
    |Criador de Perfil - Campos|Para **limpeza** e **limpeza do SSIS** subtipos, contém as seguintes informações sobre a atividade:   Campo, domínio, valores, corrigidos sugerido valores, a integridade e a precisão.<br /><br /> Para **descoberta de Conhecimento**, **gerenciamento de domínio**, **política de correspondência**, e **correspondentes** subtipos, contém o seguinte informações sobre a atividade:   Campo, domínio, novo, exclusivo, válido no domínio e integridade.|  
  
##  <a name="Terminate"></a> Encerrar uma atividade do DQS  
 Os administradores de DQS (função dqs_administrator) podem encerrar uma atividade (ativa) em execução que não é do tipo **Limpeza do SSIS**. O encerramento de uma atividade interromperá todos os processos em execução na atividade e removerá tudo que estiver relacionado à atividade. Essa operação não pode ser desfeita. Encerrar uma atividade na tela de monitoramento de atividades é equivalente a cancelar a respectiva atividade clicando em **Cancelar** durante sua execução na área de recurso no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Para encerrar uma atividade:  
  
1.  Selecione uma atividade em execução na grade de atividade (no painel superior).  
  
2.  Clique no ícone **Encerrar a atividade selecionada** . Se desejar, clique com o botão direito do mouse na atividade na grade de atividade e clique em **Encerrar Atividade** no menu de atalho.  
  
3.  Uma mensagem é exibida para confirmar sua ação. Clique em **Sim**.  
  
##  <a name="Stop"></a> Interromper um processo na atividade do DQS  
 Os administradores de DQS (função dqs_administrator) podem interromper um processo (ativo) em execução em uma atividade que não é do tipo **Limpeza do SSIS**. Interromper um processo na tela de monitoramento de atividades é equivalente a interromper o processo na respectiva atividade na área de recurso do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Por exemplo, interromper o processo de limpeza assistido por computador em uma atividade de limpeza ou interromper o processo correspondente em uma atividade correspondente. Um processo interrompido não pode ser reiniciado na tela de monitoramento de atividades. Você precisará reiniciar o processo na respectiva área de recurso do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Nesse caso, uma linha adicional será adicionada à grade de processos na guia **Etapas da Atividade** . O status de processo interrompido continua sendo exibido como **Parado**. Para interromper um processo:  
  
1.  Selecione um processo em execução na grade de detalhes da atividade (no painel inferior).  
  
2.  Clique no ícone **Parar o processo selecionado** . Se desejar, clique com o botão direito do mouse no processo na grade de detalhes da atividade e clique em **Parar Processo** no menu de atalho.  
  
3.  Uma mensagem é exibida para confirmar sua ação. Clique em **Sim**.  
  
  
