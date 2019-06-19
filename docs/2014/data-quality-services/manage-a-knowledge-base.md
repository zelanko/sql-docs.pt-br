---
title: Gerenciar uma base de dados de conhecimento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 27f306f4-d67c-47f5-b35c-4260cc5d36e3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 552cd3a091699c42001ab42e64ff875760fe1e53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484170"
---
# <a name="manage-a-knowledge-base"></a>Gerenciar uma base de dados de conhecimento
  Este tópico descreve como executar funções de gerenciamento em uma base de dados de conhecimento no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Você pode excluir uma base de dados de conhecimento, desbloqueá-la, descartar seu trabalho nela, renomeá-la e exibir suas propriedades.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para gerenciar uma base de dados de conhecimento, ela já deve ter sido criada e publicada (caso outra pessoa a tenha criado) ou fechada (se você a criou).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para abrir uma base de dados de conhecimento.  
  
##  <a name="Manage"></a> Gerenciar uma base de dados de conhecimento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Abrir base de dados de conhecimento**.  
  
3.  Clique com o botão direito do mouse em uma base de dados de conhecimento na tabela de bases de dados de conhecimento.  
  
4.  No menu de contexto, você pode fazer o seguinte:  
  
    1.  **Abrir**: clique para abrir a base de dados de conhecimento na atividade selecionada no painel **Selecionar atividade**.  
  
    2.  **Desbloquear**: Você pode desbloquear a base de conhecimento se você for o usuário que estava trabalhando na base de dados de conhecimento em uma das etapas de gerenciamento de domínio, descoberta de conhecimento e a atividade de política de correspondência e fechá-la. Se você descarregar a base de dados de conhecimento, outra pessoa poderá abri-la e trabalhar nela. Este comando não estará disponível se a base de dados de conhecimento não estiver no estado de uma atividade. Para obter mais informações, consulte [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    3.  **Descartar trabalho**: Clique quando a base de Conhecimento estiver em um estado que está sendo trabalhada, conforme mostrado com uma entrada no campo estado na tabela. Este comando não estará disponível se a base de dados de conhecimento não estiver no estado de uma atividade e se a base de dados de conhecimento estiver bloqueada. Para obter mais informações, consulte [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    4.  **Renomear**: Clique para tornar o campo de dados de Conhecimento da tabela editável para a base de dados de Conhecimento pequeno no. Altere o nome e clique nessa base de dados de conhecimento e em outra no campo p0ara aceitar a alteração do nome.  
  
    5.  **Excluir**: Clique para remover a base de conhecimento do banco de dados DQS_MAIN no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
    6.  **Propriedades**: Clique para exibir as propriedades para o banco de dados em uma exibição somente leitura.  
  
        1.  **Base de Dados de Conhecimento de Origem**: a base de dados de conhecimento na qual este banco de dados se baseia. Isso é opcional.  
  
        2.  **Estado**: indica se a base de dados de conhecimento está **Em Serviço** e se está em uma atividade de gerenciamento de conhecimento específica, conforme determinado quando ela foi fechada pela última vez. O estado pode ser **Em Serviço**, no qual a base de dados de conhecimento é aberta em uma sessão de gerenciamento de conhecimento, mas não em uma atividade específica, ou **Em Serviço** mais uma atividade de gerenciamento de conhecimento, na qual a base de dados de conhecimento é aberta em uma sessão de gerenciamento de conhecimento, e em uma atividade específica.  
  
        3.  **Está bloqueado**: **Verdadeiro** se a base de dados de conhecimento estava bloqueada, **Falso** caso contrário  
  
        4.  **Contém conteúdo não publicado**: True se a base de Conhecimento contiver algum conteúdo que não foi salvo durante a publicação, False se não  
  
        5.  **Bloqueado por**: o nome do usuário que fechou a base de dados de conhecimento, bloqueando-a  
  
        6.  **Data do Bloqueio**: data em que o bloqueio foi feito  
  
        7.  **Criado por**: o nome do usuário que criou a base de dados de conhecimento, com a rede à qual ele pertence  
  
        8.  **Data de Criação**: data em que a criação foi realizada  
  
##  <a name="FollowUp"></a> Acompanhamento: Após gerenciar uma Base de Conhecimento  
 Depois que você gerenciar uma base de dados de conhecimento, a próxima etapa dependerá da ação executada na base de dados de conhecimento:  
  
-   Se você abriu a base de dados de conhecimento, continuará na atividade que selecionou.  
  
-   Se você a desbloqueou, ela estará disponível para outra pessoa abrir e trabalhar nela, no estado indicado.  
  
-   Se você descartou o trabalho nela, a base de dados de conhecimento estará disponível em seu último estado publicado.  
  
-   Se você a renomeou, precisará abrir a base de dados de conhecimento renomeada para trabalhar nela.  
  
-   Se você a excluiu, precisará selecionar outra base de dados de conhecimento para trabalhar ou criar uma nova.  
  
  
