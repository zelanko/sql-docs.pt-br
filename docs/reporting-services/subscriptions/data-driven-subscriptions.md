---
title: As assinaturas controladas por dados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: ba009f62-0d4f-45e7-a27c-36fd5f0cd3a8
caps.latest.revision: 56
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e4ffac2b4342d0f8b3c30a9d76cdc7b0ecf098c
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="data-driven-subscriptions"></a>assinaturas controladas por dados
  Uma assinatura controlada por dados fornece uma maneira de usar dados dinâmicos de assinatura recuperados de uma fonte de dados externa em tempo de execução. Uma assinatura controlada por dados também pode usar texto estático e valores padrão especificados pelo usuário quando a assinatura é definida. É possível usar assinaturas controladas por dados para fazer o seguinte:  
  
-   Distribuir um relatório a uma lista flutuante de assinantes. Por exemplo, é possível usar assinaturas controladas por dados para distribuir um relatório em uma grande organização na qual os assinantes variam de um mês para outro ou usar outros critérios que determinam a associação no grupo de um conjunto existente de usuários.  
  
-   Filtrar a saída do relatório usando valores de parâmetro de relatório recuperados em tempo de execução.  
  
-   Variar os formatos de saída de relatórios e as opções de entrega para cada entrega de relatório.  
  
 Uma assinatura controlada por dados é composta de várias partes. Os aspectos fixos de uma assinatura controlada por dados são definidos quando você cria a assinatura e esses aspectos incluem o seguinte:  
  
-   O relatório para o qual a assinatura está definida (uma assinatura sempre está associada a um único relatório).  
  
-   A extensão de entrega usada para distribuir o relatório. Você pode especificar a entrega por email do servidor de relatório, a entrega por compartilhamento de arquivo, o provedor de entrega nulo usado para pré-carregamento do cache ou uma extensão de entrega personalizada. Não é possível especificar várias extensões de entrega em uma única assinatura.  
  
-   A fonte de dados do assinante. É necessário especificar uma cadeia de conexão à fonte de dados que contém dados de assinante ao definir a assinatura. Não é possível especificar dinamicamente a fonte de dados do assinante em tempo de execução.  
  
-   A consulta usada para selecionar dados de assinante deve ser especificada ao definir a assinatura. Não é possível alterar a consulta em tempo de execução.  
  
 Os valores dinâmicos usados em uma assinatura controlada por dados são obtidos quando a assinatura é processada. Exemplos de dados de variável que podem ser usados em uma assinatura incluem o nome ou endereço de email do assinante, o formato preferencial de saída de relatório ou qualquer valor válido para um parâmetro de relatório. Para usar valores dinâmicos em uma assinatura controlada por dados, defina um mapeamento entre os campos retornados na consulta para as opções específicas de entrega e parâmetros do relatório. Os dados de variável são recuperados de uma fonte de dados do assinante sempre que a assinatura é processada.  
  
## <a name="requirements-for-using-data-driven-subscriptions"></a>Requisitos para usar assinaturas controladas por dados  
 A funcionalidade de assinatura controlada por dados não está disponível em todas as edições. Também há limitações para os tipos de fontes de dados que podem ser usadas para recuperar dados de assinatura em tempo de execução. A lista a seguir fornece mais informações sobre os requisitos:  
  
-   Para obter mais informações sobre as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que dão suporte à funcionalidade de assinatura controlada por dados, consulte [Recursos compatíveis com as edições do SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
-   Para obter dados de assinatura, escolha uma fonte de dados que possa fornecer informações de esquema para o servidor de relatório. Alguns exemplos de tipos de fonte de dados com suporte incluem dados relacionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Oracle, bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , pacotes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , fontes de dados ODBC e fontes de dados OLE DB. Para obter mais informações sobre requisitos de fonte de dados do assinante, consulte [Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
## <a name="working-with-data-driven-subscriptions"></a>Trabalhando com assinaturas controladas por dados  
 Os tópicos a seguir fornecem mais informações sobre assinaturas controladas por dados.  
  
|Tópicos|Description|  
|------------|-----------------|  
|[Criar, modificar e excluir assinaturas controladas por dados](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)|Explica como criar, modificar ou excluir uma assinatura controlada por dados.|  
|[Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)|Fornece informações sobre as fontes de dados que podem ser usadas para uma assinatura controlada por dados.|  
|[Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)|Fornece instruções passo a passo para aprender como criar uma assinatura controlada por dados.|  
|[Armazenando relatórios em cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)|Descreve como usar o Provedor de Entrega Nulo com uma assinatura controlada por dados para pré-carregamento do cache.|  
  
## <a name="see-also"></a>Consulte também  
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Página Criar Assinatura Controlada por Dados &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/814b4653-572a-48c7-847f-b310ba0f3046)   
 [Pré-carregar o cache &#40;Gerenciador de Relatórios&#41;](../../reporting-services/report-server/preload-the-cache-report-manager.md)  
  
  
