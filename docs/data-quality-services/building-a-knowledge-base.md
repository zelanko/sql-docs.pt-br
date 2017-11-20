---
title: Criando uma base de dados de conhecimento | Microsoft Docs
ms.custom: 
ms.date: 07/31/2012
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 51eff161-6ecd-4ee4-8187-1dd8ef4814bd
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8fe15c5c9313fee10edbd7a9ebc3fd282dafa5f8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="building-a-knowledge-base"></a>Criando uma base de dados de conhecimento
  Uma base de dados de conhecimento no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) é um repositório de conhecimento sobre seus dados que lhe permitem compreender os dados e manter sua integridade. Uma base de dados de conhecimento consiste em domínios, cada um representando os dados em um campo de dados. A base de dados de conhecimento é usada pelo DQS para executar a limpeza e a eliminação de duplicação de dados em um banco de dados. Para preparar a base de dados de conhecimento para a limpeza de dados, você pode executar uma análise assistida por computador de um exemplo de dados e gerenciar interativamente valores nos domínios. O DQS lhe permite importar conhecimento, criar regras e relações, alterar valores de dados diretamente e aproveitar um banco de dados padrão.  
  
## <a name="in-this-section"></a>Nesta seção  
 É possível executar as seguintes operações em uma base de dados de conhecimento:  
  
|||  
|-|-|  
|Criar uma nova base de dados de conhecimento do zero, a partir de uma base de dados de conhecimento existente ou a partir de um arquivo de dados .dqs.|[Criar uma base de dados de conhecimento](../data-quality-services/create-a-knowledge-base.md)|  
|Abrir uma base de dados de conhecimento existente para executar a descoberta da base de dados de conhecimento, o gerenciamento de domínio, ou adicionar uma política de correspondência.|[Abrir uma base de dados de conhecimento](../data-quality-services/open-a-knowledge-base.md)|  
|Executar ações de gerenciamento em uma base de dados de conhecimento, inclusive abri-la, desbloqueá-la, descartar seu trabalho nela, renomeá-la, excluí-la ou exibir suas propriedades.|[Gerenciar uma base de dados de conhecimento](../data-quality-services/manage-a-knowledge-base.md)|  
|Adicionar conhecimento a uma base de dados de conhecimento através de descoberta de conhecimento; gerenciamento de valor de domínio; adicionando uma política de comparação; importando um conhecimento, domínio ou valores; ou usando a base de dados de conhecimento padrão, Dados do DQS.|[Adicionar conhecimento a uma base de dados de conhecimento](../data-quality-services/adding-knowledge-to-a-knowledge-base.md)|  
|Analisar um exemplo de dados para critérios de qualidade de dados.|[Executar descoberta de conhecimento](../data-quality-services/perform-knowledge-discovery.md)|  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Importar ou exportar conhecimento para/de uma base de dados de conhecimento.|[Importar e exportar conhecimento](../data-quality-services/importing-and-exporting-knowledge.md)|  
|Criar um domínio único e adicionar conhecimento ao domínio.|[Gerenciar um domínio](../data-quality-services/managing-a-domain.md)|  
|Criar um domínio composto e adicionar conhecimento ao domínio.|[Gerenciar um domínio de composição](../data-quality-services/managing-a-composite-domain.md)|  
  
  

