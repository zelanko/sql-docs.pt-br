---
title: Criar uma base de dados de conhecimento | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.selectkb.f1
- sql13.dqs.kb.newkb.f1
ms.assetid: 2733a284-975f-4650-abcc-cc2aad074cab
author: lrtoyou1223
ms.author: lle
manager: jroth
ms.openlocfilehash: a56193f453781bf25dc34079c9845a7d0566f820
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66785700"
---
# <a name="create-a-knowledge-base"></a>Criar uma base de dados de conhecimento

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve como criar uma base de dados de conhecimento no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) e prepará-la para o gerenciamento de domínio, a descoberta de conhecimento ou a adição de uma política de correspondência.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para criar uma base de dados de conhecimento, você deve instalar o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para criar uma base de dados de conhecimento.  
  
##  <a name="Createaknowledgebase"></a> Create a knowledge base  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Nova base de dados de conhecimento**.  
  
3.  Digite um nome e uma descrição para a nova base de dados de conhecimento.  
  
4.  Em **Criar base de dados de conhecimento de**, selecione a base da nova base de dados de conhecimento.  
  
    -   Selecione **Nenhum** se você não quiser basear a nova base de conhecimento em uma já existente ou em um arquivo de dados.  
  
    -   Selecione **Base de dados de conhecimento existente** para basear a nova base de dados de conhecimento em uma já criada no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]ou na base de dados de conhecimento padrão. Selecione a base de dados de conhecimento na lista suspensa **Selecionar Base de Dados de Conhecimento** ou clique em **Procurar** para exibir a caixa de diálogo **Selecionar uma Base de Dados de Conhecimento** , selecione uma base de dados de conhecimento existente para basear a nova base de dados de conhecimento e clique em **OK**. Quando você seleciona uma base de dados de conhecimento no tablet, os domínios e as regras de correspondência da base de dados de conhecimento são exibidos no painel à direita da caixa de diálogo. Você também pode selecionar a base de dados de conhecimento **Dados do DQS** , que é a base de dados de conhecimento padrão que contém domínios e conhecimento comuns predefinidos, relacionados a dados de empresas, endereços e participantes nos EUA.  
  
    -   Selecione **Importar do Arquivo DQS** para basear a nova base de dados de conhecimento em um arquivo DQS no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Clique em **Procurar**, selecione um arquivo de dados do DQS com a extensão .dqs e clique em **OK**.  
  
5.  Em **Selecionar Atividade**, selecione a atividade que você deseja executar na nova base de dados de conhecimento:  
  
    -   Selecione **Gerenciamento de Domínio** para criar a base de dados de conhecimento e entrar nas telas que você usa para modificar os domínios na base de dados de conhecimento.  
  
    -   Selecione **Descoberta da Base de Dados de Conhecimento** para criar a base de dados de conhecimento e entrar no assistente que você usa para analisar um exemplo de dados e popular os domínios da base de dados de conhecimento com os resultados.  
  
    -   Selecione **Política de Correspondência** para criar uma política de correspondência e adicioná-la à base de dados de conhecimento.  
  
6.  Clique em **Criar**.  
  
##  <a name="FollowUp"></a> Acompanhamento: após criar uma base de dados de conhecimento  
 Depois que você criar uma base de dados de conhecimento, verá um assistente para executar a descoberta da base de dados de conhecimento, um assistente para criar uma política de correspondência ou páginas para fazer o gerenciamento do domínio. Para obter mais informações sobre a descoberta de conhecimento, o gerenciamento de domínio ou a política de conciliação, consulte [Executar a descoberta de conhecimento](../data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../data-quality-services/managing-a-domain.md) ou [Criar uma política de conciliação](../data-quality-services/create-a-matching-policy.md).  
  
  
