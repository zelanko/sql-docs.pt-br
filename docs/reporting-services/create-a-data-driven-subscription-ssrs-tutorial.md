---
title: Criar uma assinatura controlada por dados (Tutorial do SSRS) | Microsoft Docs
description: Saiba mais sobre as assinaturas controladas por dados por meio de um exemplo simples que cria uma assinatura controlada por dados para gerar e salvar a saída do relatório filtrado em um compartilhamento de arquivo.
ms.date: 05/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2f4843c02d12c08cac8efa8b453999f4484ab084
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246328"
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>Criar uma assinatura controlada por dados (Tutorial do SSRS)
Este tutorial do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ensina os conceitos de assinaturas controladas por dados, apresentando um exemplo simples que cria uma assinatura controlada por dados para gerar e salvar a saída do relatório filtrado em um compartilhamento de arquivos. 
[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] As assinaturas controladas por dados permitem personalizar e automatizar a distribuição de um relatório baseado em dados de assinante dinâmicos. As assinaturas controladas por dados foram desenvolvidas para os seguintes tipos de cenário:  
  
-   Distribuição de relatórios em um grande pool de destinatários cuja associação pode ser alterada de uma distribuição para a outra. Por exemplo, enviar por email um relatório mensal a todos os clientes atuais.  
  
-   Distribuição de relatórios para um grupo específico de destinatários baseado em critérios predefinidos. Por exemplo, enviar um relatório de desempenho de vendas para todos os gerentes de vendas de uma organização.
+ Automatize a geração de relatórios em uma ampla variedade de formatos, por exemplo, .xlsx e .pdf.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Este tutorial divide-se em três lições:  

| Lição | Comentários |
| ------ | -------- |
| [Lição 1: Criar um banco de dados do assinante de exemplo](../reporting-services/lesson-1-creating-a-sample-subscriber-database.md) | Nesta lição, você aprenderá a criar um banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] local de tabela que contém informações do assinante. as informações de Números da Order a serem usadas para filtragem e formatos de arquivo de saída. |
| [Lição 2: Configurar propriedades da fonte de dados do relatório](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md) | Nesta lição, você aprenderá a configurar uma fonte de dados do relatório para que o relatório possa ser executado de forma autônoma em um agendamento. O processamento autônomo exige credenciais armazenadas. Você também modificará o conjunto de dados de relatório para incluir um parâmetro que é fornecido pelos dados do assinante. Esse parâmetro é usado para filtrar os dados de relatório com base no número do pedido. |
| [Lição 3: Definir uma assinatura controlada por dados](../reporting-services/lesson-3-defining-a-data-driven-subscription.md) | Nessa lição, você aprenderá a criar uma assinatura controlada por dados. Esta lição o guia por cada página do Assistente de Assinatura Controlada por Dados. |

O diagrama a seguir ilustra o fluxo de trabalho básico do tutorial:

| Etapa    | Descrição |
| --------|------------ |
| (1)     | A configuração de assinatura anota o relatório de origem, o agendamento e o mapeamento de campo para o Banco de dados do assinante. |
| (2)     | A tabela OrderInfo contém quatro números de pedido a serem usados para filtragem, um por arquivo. A tabela também contém os formatos de arquivo para os relatórios gerados. |
| (3)     | As informações do banco de dados Adventureworks são filtradas e retornadas no relatório. |
| (4)     | Os relatórios são criados nos formatos de arquivo especificados na tabela Orderinfo. |



   ![ssrs_tutorial_datadriven_flow](../reporting-services/media/ssrs-tutorial-datadriven-flow.png) 
  
## <a name="requirements"></a>Requisitos  
As assinaturas controladas por dados normalmente são criadas e mantidas por administradores de servidor de relatórios. As etapas para criar assinaturas controladas por dados exige a criação de consultas, o conhecimento das fontes de dados que contêm dados do assinante e permissões elevadas em um servidor de relatório.  
  
O tutorial usa o relatório *Pedido de vendas* criado no tutorial [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) e dados do banco de dados de exemplo **AdventureWorks2014**.  
  
Para usar este tutorial, seu computador deve ter os seguintes itens instalados:  
  
-   Uma edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que dá suporte a assinaturas controladas por dados. Para obter mais informações, confira [Edições e recursos do SQL Server 2017](../sql-server/editions-and-components-of-sql-server-2017.md).  
  
-   É necessário que o servidor de relatório esteja sendo executado no modo nativo. A interface do usuário descrita neste tutorial é baseada em um servidor de relatório de modo nativo. As assinaturas têm suporte em servidores de relatórios do modo do SharePoint, mas a interface do usuário será diferente do que está descrito neste tutorial.  
  
-   O serviço do SQL Server Agent deve estar em execução.  
  
-   Um relatório que inclui parâmetros. Este tutorial presume o uso do relatório de exemplo, `Sales Orders` , criado por meio do tutorial [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md).  
  
-   O banco de dados de exemplo **AdventureWorks2014** , que fornece dados ao relatório de exemplo.  
  
-   Uma atribuição de função [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] que inclui a tarefa Gerenciar todas as assinaturas no relatório de exemplo. Esta tarefa é obrigatória para definir uma assinatura controlada por dados. Se você for administrador no computador, a atribuição de função padrão para administradores locais fornecerá as permissões necessárias para criar assinaturas controladas por dados. Para obter mais informações, consulte [Concedendo permissões em um servidor de relatório no modo nativo](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).  
  
-   Uma pasta compartilhada na qual você tenha permissões de gravação. A pasta compartilhada deve ser acessada por uma conexão de rede.  
  
**Tempo estimado para a conclusão do tutorial:** 30 minutos. Mais 30 minutos se você não concluiu o tutorial de relatório básico.  
  
## <a name="see-also"></a>Consulte Também  
[Assinaturas controladas por dados](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)
 

