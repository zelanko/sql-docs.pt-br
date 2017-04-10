---
title: "Abrir uma base de dados de conhecimento | Microsoft Docs"
ms.custom: ""
ms.date: "06/04/2013"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.kb.openkb.f1"
ms.assetid: a5f010a5-b762-41c9-881b-bf0c192dca83
caps.latest.revision: 20
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# Abrir uma base de dados de conhecimento
  Este tópico descreve como abrir uma base de dados de conhecimento existente no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) e prepará-la para o gerenciamento de domínio, a descoberta de conhecimento ou a adição de uma política de correspondência.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para abrir uma base de dados de conhecimento, essa base já deve ter sido criada e publicada (caso outra pessoa a tenha criado) ou fechada (se você a criou).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para abrir uma base de dados de conhecimento.  
  
##  <a name="Open"></a> Abrir uma base de dados de conhecimento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo de cliente de qualidade de dados](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Abrir base de dados de conhecimento**.  
  
3.  Selecione uma base de dados de conhecimento na tabela. Os domínios e as regras correspondentes na base de dados de conhecimento serão exibidos no painel à direita da página.  
  
    > [!NOTE]  
    >  É possível executar operações em uma base de dados de conhecimento clicando com o botão direito do mouse na tabela. Você pode abrir a base de dados de conhecimento, salvá-la com outro nome, desbloqueá-la, descartar o trabalho, renomeá-la ou exibir suas propriedades.  
  
4.  Em **Selecionar Atividade**, selecione a atividade que você deseja executar na base de dados de conhecimento:  
  
    -   Selecione **Gerenciamento de Domínio** para entrar nas telas usadas para modificar os domínios da base de dados de conhecimento.  
  
    -   Selecione **Descoberta da Base de Dados de Conhecimento** para entrar no assistente que você usa para analisar um exemplo de dados e popular os domínios da base de conhecimento com os resultados.  
  
    -   Selecione **Política de Correspondência** para criar uma política de correspondência e adicioná-la à base de dados de conhecimento.  
  
5.  Clique em **Abrir**.  
  
    > [!NOTE]  
    >  Também é possível abrir a base de dados de conhecimento clicando com o botão direito do mouse nela e depois clicando em Abrir. Outros comandos no menu de contexto permitem a você salvá-la com outro nome, desbloqueá-la, descartar o trabalho, renomeá-la ou exibir suas propriedades.  
  
    > [!NOTE]  
    >  Se você não conseguir abrir a base de dados de conhecimento porque ela está bloqueada, consulte a seção abaixo.  
  
## Abrir uma base de dados de conhecimento recente  
 As cinco bases de dados de conhecimento abertas mais recentemente são exibidas na lista **Base de Dados de Conhecimento Recente** na página inicial do DQS. Isso permite a você abrir uma base de dados de conhecimento aberta recentemente sem passar pela página **Abrir Base de Dados de Conhecimento** .  
  
-   Para abrir uma base de dados de conhecimento na lista Recente que não estiver bloqueada, clique na seta para direita da base de dados de conhecimento e depois selecione a atividade na qual você deseja abrir a base de dados de conhecimento.  
  
-   Para abrir uma base de dados de conhecimento na lista Recente que você bloqueou, clique na base de dados de conhecimento e isso abrirá a atividade e a página indicada entre parênteses.  
  
-   Para abrir uma base de dados de conhecimento na lista Recente que foi bloqueada por outra pessoa, contate essa pessoa e peça a ela para desbloquear a base de dados de conhecimento.  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de abrir uma base de dados de conhecimento  
 Depois que você abrir uma base de dados de conhecimento, ela será colocada no estado indicado na coluna Estado da tabela Base de Dados de Conhecimento. Para as atividades de descoberta da base de dados de conhecimento e política de correspondência, a base de dados de conhecimento será aberta em uma página de assistente específica. Para a atividade de gerenciamento de domínio, a base de dados de conhecimento será aberta na página de gerenciamento de domínio. Para obter mais informações sobre os estados, consulte [executar a descoberta de Conhecimento](../data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../data-quality-services/managing-a-domain.md), ou [criar uma política de correspondência](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Locked"></a> Se a base de dados de conhecimento estiver bloqueada  
 O ícone de bloqueio na primeira coluna mostra se a base de conhecimento está bloqueada. O nome de uma base de dados de conhecimento bloqueada estará em fonte vermelha. Uma base de dados de conhecimento que estiver sendo modificada por um usuário específico por meio de uma atividade de base de dados de conhecimento estará marcada como Bloqueada. Uma base de dados de conhecimento bloqueda não pode ser trabalhada por um segundo usuário. O usuário que está trabalhando na base de dados de conhecimento pode desbloqueá-la clicando duas vezes a base de dados de Conhecimento na tabela na página abrir Base de dados de conhecimento e, em seguida, clicando em **Unlock**, ou publicando-o. Quando o cursor estiver posicionado em uma base de dados de conhecimento bloqueada, o DQS exibirá uma dica mostrando quem bloqueou a base de dados de conhecimento e quando ela foi bloqueada.  
  
##  <a name="State"></a> Estado de uma base de dados de conhecimento  
 O campo Estado indica em qual estágio de uma atividade a base de dados de conhecimento está. Se você abrir a base de dados de conhecimento, ela será aberta nesse estágio.  
  
-   **\< vazio>**: O campo estado estará vazio para uma base de conhecimento se a base de Conhecimento tiver sido publicada, clicando em **publicar** na atividade de gerenciamento de domínio e clicando em **Sim – publique a base de conhecimento e saia**.  
  
-   **Em Serviço**: O trabalho na base de conhecimento foi salvo com um clique em **Publicar** na atividade Gerenciamento de Domínio e com um clique em **Não – Salve o trabalho na base de dados de conhecimento e saia**.  
  
-   **Gerenciamento de Domínio**: Os dados foram inseridos em um domínio na base de conhecimento, mas a base de conhecimento não foi publicada e o trabalho permanece na atividade Gerenciamento de Domínio. A atividade Descoberta da Base de Dados de Conhecimento não está disponível. Isso ocorre quando você clica em **Fechar** na tela **Gerenciamento de Domínio** .  
  
-   **Descoberta - mapeamento**: A base de dados de conhecimento foi fechada na **Gerenciamento da Base de dados de Conhecimento: mapeamento** página. A base de dados de conhecimento está bloqueada e as atividades Gerenciamento de Domínio e Correspondência não estão disponíveis.  
  
-   **Descoberta - descobrir**: A base de dados de conhecimento foi fechada na **Gerenciamento da Base de dados de Conhecimento: analisar** página. A base de dados de conhecimento está bloqueada e a atividade Gerenciamento de Domínio não está disponível.  
  
-   **Descoberta - Gerenciamento de Valor**: a base de dados de conhecimento foi fechada na página **Gerenciamento da Base de Dados de Conhecimento: Gerenciar Termos do Domínio** . A base de dados de conhecimento está bloqueada e a atividade Gerenciamento de Domínio não está disponível.  
  
-   **Política de Correspondência – Política de Correspondência**: a base de dados de conhecimento foi fechada na página **Política de Correspondência – Política de Correspondência** . A base de dados de conhecimento está bloqueada e as atividades Descoberta da Base de Dados de Conhecimento e Gerenciamento de Domínio e Correspondência não estão disponíveis.  
  
-   **Política de Correspondência – Resultados Correspondentes**: a base de dados de conhecimento foi fechada na página **Política de Correspondência – Resultados de Correspondência** . A base de dados de conhecimento está bloqueada e as atividades Descoberta da Base de Dados de Conhecimento e Gerenciamento de Domínio e Correspondência não estão disponíveis.  
  
  