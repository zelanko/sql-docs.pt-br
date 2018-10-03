---
title: Usar relações de valor em um domínio de composição | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.cdvaluerelations.f1
ms.assetid: 5ee468f0-8538-4620-90e8-63f466c9000e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d26836ca62c4a86cfbfde5b7f29920911ac6efdf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48081856"
---
# <a name="use-value-relations-in-a-composite-domain"></a>Usar relações de valor em um domínio composto
  Este tópico descreve como exibir combinações de valores encontradas para o domínio composto durante o processo de descoberta de conhecimento no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Esta página mostra o número de ocorrências das combinações de valores. O gerenciamento de valores não tem suporte para domínios compostos; portanto, você não pode executar operações nesses valores.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para exibir relações de valor, é preciso criar e abrir um domínio composto.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para exibir relações de valor em um domínio composto.  
  
##  <a name="Use"></a> Exibir relações de valor  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra ou crie uma base de dados de conhecimento. Selecione **Gerenciamento de Domínio** como a atividade e, depois, clique em **Abrir** ou **Criar**. Para obter mais informações, consulte [Criar uma base de dados de conhecimento](../../2014/data-quality-services/create-a-knowledge-base.md) ou [Abrir uma base de dados de conhecimento](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
3.  Na **Lista de domínios** na página **Gerenciamento de Domínio** , selecione o domínio composto para o qual você deseja criar uma regra de domínio ou crie um novo domínio composto. Se você precisa criar um novo domínio, consulte [criar um domínio composto](../../2014/data-quality-services/create-a-composite-domain.md).  
  
4.  Clique na guia **Relações de Valor** .  
  
5.  Exiba as frequências exibidas para cada combinação de valor.  
  
    > [!NOTE]  
    >  A tabela **Value** mostra cada combinação de valores que existe no domínio composto. Cada valor é mostrado no único domínio ao qual ele se aplica. A classificação padrão da tabela de relações de valor é por frequência, mas você pode clicar em outra coluna para classificar por essa coluna. Somente esses valores com uma frequência maior que ou igual a 20 são exibidos.  
  
6.  Você não pode alterar os valores na tabela. Se você executou outras operações, clique em **Concluir** para concluir a atividade de gerenciamento de domínio. Caso contrário, clique em **Cancelar**.  
  
##  <a name="FollowUp"></a> Acompanhamento: após exibir relações de valor  
 Depois de exibir relações de valor, você poderá executar outras tarefas de gerenciamento de domínio, executar a descoberta da base de dados de conhecimento para adicionar conhecimento ao domínio ou adicionar uma política de correspondência ao domínio. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../../2014/data-quality-services/managing-a-domain.md) ou [Criar uma política de conciliação](../../2014/data-quality-services/create-a-matching-policy.md).  
  
  
