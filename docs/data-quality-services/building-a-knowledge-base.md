---
title: Criando uma base de dados de conhecimento
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 51eff161-6ecd-4ee4-8187-1dd8ef4814bd
author: swinarko
ms.author: sawinark
ms.openlocfilehash: ae84775172f7595adcb3e5de612ed74f4ccf45d9
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812563"
---
# <a name="building-a-knowledge-base"></a>Criando uma base de dados de conhecimento

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Uma base de dados de conhecimento no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) é um repositório de conhecimento sobre seus dados que lhe permitem compreender os dados e manter sua integridade. Uma base de dados de conhecimento consiste em domínios, cada um representando os dados em um campo de dados. A base de dados de conhecimento é usada pelo DQS para executar a limpeza e a eliminação de duplicação de dados em um banco de dados. Para preparar a base de dados de conhecimento para a limpeza de dados, você pode executar uma análise assistida por computador de um exemplo de dados e gerenciar interativamente valores nos domínios. O DQS lhe permite importar conhecimento, criar regras e relações, alterar valores de dados diretamente e aproveitar um banco de dados padrão.  
  
## <a name="in-this-section"></a>Nesta seção  
 É possível executar as seguintes operações em uma base de dados de conhecimento:  
  
|||  
|-|-|  
|Criar uma nova base de dados de conhecimento do zero, a partir de uma base de dados de conhecimento existente ou a partir de um arquivo de dados .dqs.|[Criar uma base de dados de conhecimento](../data-quality-services/create-a-knowledge-base.md)|  
|Abrir uma base de dados de conhecimento existente para executar a descoberta da base de dados de conhecimento, o gerenciamento de domínio, ou adicionar uma política de correspondência.|[Abrir uma base de dados de conhecimento](../data-quality-services/open-a-knowledge-base.md)|  
|Executar ações de gerenciamento em uma base de dados de conhecimento, inclusive abri-la, desbloqueá-la, descartar seu trabalho nela, renomeá-la, excluí-la ou exibir suas propriedades.|[Gerenciar uma base de dados de conhecimento](../data-quality-services/manage-a-knowledge-base.md)|  
|Adicionar conhecimento a uma base de dados de conhecimento através de descoberta de conhecimento; gerenciamento de valor de domínio; adicionando uma política de comparação; importando um conhecimento, domínio ou valores; ou usando a base de dados de conhecimento padrão, Dados do DQS.|[Adicionando conhecimento a uma base de dados de conhecimento](../data-quality-services/adding-knowledge-to-a-knowledge-base.md)|  
|Analisar um exemplo de dados para critérios de qualidade de dados.|[Executar a descoberta da base de dados de conhecimento](../data-quality-services/perform-knowledge-discovery.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Importar ou exportar conhecimento para/de uma base de dados de conhecimento.|[Importando e exportando conhecimento](../data-quality-services/importing-and-exporting-knowledge.md)|  
|Criar um domínio único e adicionar conhecimento ao domínio.|[Gerenciando um domínio](../data-quality-services/managing-a-domain.md)|  
|Criar um domínio composto e adicionar conhecimento ao domínio.|[Gerenciando um domínio composto](../data-quality-services/managing-a-composite-domain.md)|  
  
  
