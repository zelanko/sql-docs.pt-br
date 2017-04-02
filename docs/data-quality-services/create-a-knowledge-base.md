---
title: "Criar uma base de dados de conhecimento | Microsoft Docs"
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
  - "sql13.dqs.kb.selectkb.f1"
  - "sql13.dqs.kb.newkb.f1"
ms.assetid: 2733a284-975f-4650-abcc-cc2aad074cab
caps.latest.revision: 20
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# Criar uma base de dados de conhecimento
  Este tópico descreve como criar uma base de dados de conhecimento no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) e prepará-la para o gerenciamento de domínio, a descoberta de conhecimento ou a adição de uma política de correspondência.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para criar uma base de dados de conhecimento, você deve instalar o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para criar uma base de dados de conhecimento.  
  
##  <a name="Createaknowledgebase"></a> Criar uma base de dados de conhecimento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo de cliente de qualidade de dados](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Nova base de dados de conhecimento**.  
  
3.  Digite um nome e uma descrição para a nova base de dados de conhecimento.  
  
4.  Em **Criar base de dados de conhecimento de**, selecione a base da nova base de dados de conhecimento.  
  
    -   Selecione **Nenhum** se você não quiser basear a nova base de conhecimento em uma já existente ou em um arquivo de dados.  
  
    -   Selecione **Base de dados de conhecimento existente** para basear a nova base de dados de conhecimento em uma já criada no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]ou na base de dados de conhecimento padrão. Selecione a base de dados de conhecimento do **Selecione Knowledge Base** lista suspensa ou clique em **Procurar** para exibir o **Selecione uma Base de dados de Conhecimento** caixa de diálogo, selecione um conhecimento existente base para basear a nova base de dados de conhecimento em e, em seguida, clique em **OK**. Quando você seleciona uma base de dados de conhecimento no tablet, os domínios e as regras de correspondência da base de dados de conhecimento são exibidos no painel à direita da caixa de diálogo. Você também pode selecionar o **dados do DQS** knowledge base, que é a base de dados de Conhecimento padrão que contém domínios out-of-the-box comuns e conhecimento relacionado aos EUA da empresa, endereço e dados.  
  
    -   Selecione **Importar do Arquivo DQS** para basear a nova base de dados de conhecimento em um arquivo DQS no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Clique em **Procurar**, selecione um arquivo de dados do DQS com a extensão .dqs e clique em **OK**.  
  
5.  Em **Selecionar Atividade**, selecione a atividade que você deseja executar na nova base de dados de conhecimento:  
  
    -   Selecione **Gerenciamento de Domínio** para criar a base de dados de conhecimento e entrar nas telas que você usa para modificar os domínios na base de dados de conhecimento.  
  
    -   Selecione **Descoberta da Base de Dados de Conhecimento** para criar a base de dados de conhecimento e entrar no assistente que você usa para analisar um exemplo de dados e popular os domínios da base de dados de conhecimento com os resultados.  
  
    -   Selecione **Política de Correspondência** para criar uma política de correspondência e adicioná-la à base de dados de conhecimento.  
  
6.  Clique em **Criar**.  
  
##  <a name="FollowUp"></a> Acompanhamento: Após criar uma base de dados de conhecimento  
 Depois que você criar uma base de dados de conhecimento, verá um assistente para executar a descoberta da base de dados de conhecimento, um assistente para criar uma política de correspondência ou páginas para fazer o gerenciamento do domínio. Para obter mais informações sobre a descoberta de Conhecimento, gerenciamento de domínio ou política de correspondência, consulte [executar a descoberta de Conhecimento](../data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../data-quality-services/managing-a-domain.md), ou [criar uma política de correspondência](../data-quality-services/create-a-matching-policy.md).  
  
  