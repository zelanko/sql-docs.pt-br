---
title: Assinaturas controladas por dados | Microsoft Docs
ms.date: 05/20/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: ba009f62-0d4f-45e7-a27c-36fd5f0cd3a8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2791293f805f1e2c0d9bd39822bc3f452777c007
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66175605"
---
# <a name="data-driven-subscriptions"></a>assinaturas controladas por dados
  Uma assinatura controlada por dados fornece uma maneira de usar dados dinâmicos de assinatura recuperados de uma fonte de dados externa em tempo de execução. Uma assinatura controlada por dados também pode usar texto estático e valores padrão especificados pelo usuário quando a assinatura é definida. É possível usar assinaturas controladas por dados para fazer o seguinte:  
  
-    Distribuir um relatório a uma lista flutuante de assinantes. Por exemplo, é possível usar assinaturas controladas por dados para distribuir um relatório em uma grande organização na qual os assinantes variam de um mês para outro ou usar outros critérios que determinam a associação no grupo de um conjunto existente de usuários.  
  
-   Filtrar a saída do relatório usando valores de parâmetro de relatório recuperados em tempo de execução.  
  
-   Variar os formatos de saída de relatórios e as opções de entrega para cada entrega de relatório.  
  
 Uma assinatura controlada por dados é composta de várias partes. Os aspectos fixos de uma assinatura controlada por dados são definidos quando você cria a assinatura e esses aspectos incluem o seguinte:  
  
- O relatório para o qual a assinatura está definida (uma assinatura sempre está associada a um único relatório).  
  
- A extensão de entrega usada para distribuir o relatório. Você pode especificar a entrega por email do servidor de relatório, a entrega por compartilhamento de arquivo, o provedor de entrega nulo usado para pré-carregamento do cache ou uma extensão de entrega personalizada. Não é possível especificar várias extensões de entrega em uma única assinatura.  
  
- A fonte de dados do assinante. É necessário especificar uma cadeia de conexão à fonte de dados que contém dados de assinante ao definir a assinatura. Não é possível especificar dinamicamente a fonte de dados do assinante em tempo de execução.  
  
- A consulta usada para selecionar dados de assinante deve ser especificada ao definir a assinatura. Não é possível alterar a consulta em tempo de execução.  
  
 Os valores dinâmicos usados em uma assinatura controlada por dados são obtidos quando a assinatura é processada. Exemplos de dados de variável que podem ser usados em uma assinatura incluem o nome ou endereço de email do assinante, o formato preferencial de saída de relatório ou qualquer valor válido para um parâmetro de relatório. Para usar valores dinâmicos em uma assinatura controlada por dados, defina um mapeamento entre os campos retornados na consulta para as opções específicas de entrega e parâmetros do relatório. Os dados de variável são recuperados de uma fonte de dados do assinante sempre que a assinatura é processada.  
  
## <a name="requirements-for-using-data-driven-subscriptions"></a>Requisitos para usar assinaturas controladas por dados

 A funcionalidade de assinatura controlada por dados não está disponível em todas as edições. Também há limitações para os tipos de fontes de dados que podem ser usadas para recuperar dados de assinatura em tempo de execução. A lista a seguir fornece mais informações sobre os requisitos:  

- Para saber mais sobre as edições do SQL Server que dão suporte à funcionalidade de assinatura controlada por dados, confira [Recursos do SQL Server Reporting Services com suporte de suas edições](../reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).  

- Para obter dados de assinatura, escolha uma fonte de dados que possa fornecer informações de esquema para o servidor de relatório. Alguns exemplos de tipos de fonte de dados com suporte incluem dados relacionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Oracle, bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , pacotes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , fontes de dados ODBC e fontes de dados OLE DB. Para obter mais informações sobre requisitos de fonte de dados do assinante, consulte [Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
## <a name="working-with-data-driven-subscriptions"></a>Trabalhando com assinaturas controladas por dados  
 Os tópicos a seguir fornecem mais informações sobre assinaturas controladas por dados.  
  
|Tópicos|Descrição|  
|------------|-----------------|  
|[Criar, modificar e excluir assinaturas controladas por dados](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)|Explica como criar, modificar ou excluir uma assinatura controlada por dados.|  
|[Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)|Fornece informações sobre as fontes de dados que podem ser usadas para uma assinatura controlada por dados.|  
|[Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)|Fornece instruções passo a passo para aprender como criar uma assinatura controlada por dados.|  
|[Armazenando relatórios em cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)|Descreve como usar o Provedor de Entrega Nulo com uma assinatura controlada por dados para pré-carregamento do cache.|  
  
## <a name="see-also"></a>Confira também

 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
 [Pré-carregar o cache &#40;Portal da Web&#41;](../../reporting-services/report-server/preload-the-cache-report-manager.md)  
  
  
