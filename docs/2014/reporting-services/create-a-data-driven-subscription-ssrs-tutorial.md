---
title: Criar uma assinatura controlada por dados (Tutorial do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a6e1399c97e77a2b7b0bb68a8022effefb1d4814
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59964102"
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>Criar uma assinatura controlada por dados (Tutorial do SSRS)
  O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece assinaturas controladas por dados de forma que você pode personalizar a distribuição de um relatório baseado em dados de assinante dinâmicos. As assinaturas controladas por dados foram desenvolvidas para os seguintes tipos de cenário:  
  
-   Distribuição de relatórios em um grande pool de destinatários cuja associação pode ser alterada de uma distribuição para a outra. Por exemplo, distribua um relatório mensal a todos os clientes atuais.  
  
-   Distribuição de relatórios para um grupo específico de destinatários baseado em critérios predefinidos. Por exemplo, envie um relatório de desempenho de vendas para os dez principais gerentes de vendas em uma organização.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Este tutorial mostra como usar assinaturas controladas por dados usando um exemplo simples para ilustrar os conceitos.  
  
 Este tutorial divide-se em três lições:  
  
 [Lição 1: Criando um banco de dados de assinante de exemplo](lesson-1-creating-a-sample-subscriber-database.md)  
 Nesta lição, você aprenderá a criar um banco de dados local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que contém informações de assinante.  
  
 [Lição 2: Modificar as propriedades de fonte de dados de relatório](lesson-2-modifying-the-report-data-source-properties.md)  
 Nesta lição, você aprenderá a modificar propriedades da fonte de dados de relatório de forma que o relatório possa ser executado de forma autônoma. O processamento autônomo exige credenciais armazenadas. Você também modificará o conjunto de dados de relatório para incluir um parâmetro que é fornecido pelos dados do assinante.  
  
 [Lição 3: Definindo uma assinatura controlada por dados](lesson-3-defining-a-data-driven-subscription.md)  
 Nesta lição, você aprenderá a definir uma assinatura controlada por dados. Esta lição o guia por cada página do Assistente de Assinatura Controlada por Dados.  
  
## <a name="requirements"></a>Requisitos  
 As assinaturas controladas por dados normalmente são criadas e mantidas por administradores de servidor de relatórios. A capacidade de criar assinaturas controladas por dados requer experiência em criação de consultas, conhecimento das fontes de dados que contêm dados de assinante e permissões elevadas em um servidor de relatório.  
  
 O tutorial usará o relatório criado no tutorial [criar um relatório de tabela básico &#40;Tutorial do SSRS&#41; ](create-a-basic-table-report-ssrs-tutorial.md) e os dados de [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]  
  
 Para que você possa usar o tutorial, os itens a seguir devem estar instalados no sistema:  
  
-   Uma edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que dá suporte a assinaturas controladas por dados. Para obter mais informações, consulte [edições e componentes do SQL Server 2014](../sql-server/editions-and-components-of-sql-server-2016.md).  
  
-   É necessário que o servidor de relatório esteja sendo executado no modo nativo. A interface do usuário descrita neste tutorial é baseada em um servidor de relatório de modo nativo. As assinaturas têm suporte em servidores de relatórios do modo do SharePoint, mas a interface do usuário será diferente do que está descrito neste tutorial.  
  
-   O serviço do SQL Server Agent deve estar em execução.  
  
-   Um relatório que inclui parâmetros. Este tutorial presume o uso do relatório de exemplo, `Sales Orders` , criado por meio do tutorial [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md).  
  
-   O banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)], que fornece dados ao relatório de amostra.  
  
-   Uma atribuição de função que inclua a tarefa Gerenciar todas as assinaturas no relatório de amostra. Esta tarefa é obrigatória para definir uma assinatura controlada por dados. Se você for administrador no computador, a atribuição de função padrão para administradores locais fornecerá as permissões necessárias para criar assinaturas controladas por dados. Para obter mais informações, consulte [Granting Permissions on a Native Mode Report Server](security/granting-permissions-on-a-native-mode-report-server.md).  
  
-   Uma pasta compartilhada na qual você tenha permissões de gravação. A pasta compartilhada deve ser acessada por uma conexão de rede.  
  
 **Tempo estimado para conclusão do tutorial:** 30 minutos. Mais 30 minutos se você não concluiu o tutorial de relatório básico.  
  
## <a name="see-also"></a>Consulte também  
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
