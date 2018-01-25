---
title: Conecte-se ao Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 01/23/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: instances of Analysis Services, connections
ms.assetid: 73ee8171-3379-4384-bfc8-071b3eebbc8f
caps.latest.revision: "46"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7dbadb28b56be49197f530e735f68238d13bc101
ms.sourcegitcommit: 3206a31870f8febab7d1718fa59fe0590d4d45db
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="connect-to-analysis-services"></a>Conectar ao Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Use as informações desta seção para saber mais sobre as propriedades de cadeia de caracteres de conexão, as bibliotecas de cliente usadas para conexões, os métodos de autenticação são suportados pelo Analysis Services e como definir ou limpar conexões antes de colocar um servidor offline.  

Para obter informações sobre como se conectar ao Azure Analysis Services, consulte [conectar a um servidor](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect).
  
## <a name="analysis-services-connections"></a>Conexões do Analysis Services  
 O Analysis Services usa o TCP como protocolo de rede e o XMLA como protocolo de comunicação. No nível inferior, todas as bibliotecas de cliente fornecidas com o Analysis Services implementam o XMLA sobre TCP. Embora seja possível criar aplicativos com base no XMLA bruto, a maioria dos aplicativos e desenvolvedores de aplicativos usam bibliotecas de cliente para tirar proveito dos modelos de objeto e das eficiências de codificação que eles fornecem. Para conexões de cliente com o Analysis Services, é possível utilizar o IIS como uma conexão intermediária se não for possível utilizar o TCP em toda a pilha. Uma vantagem de utilizar o acesso HTTP por meio do IIS é a capacidade de conexão de aplicativos que passam credenciais na cadeia de conexão.  
  
 Qualquer discussão que envolva conectividade normalmente inclui a autenticação. Em comparação a outros recursos do SQL Server, o Analysis Services utiliza credencias exclusivamente do Windows. Não é possível utilizar o resumo, a autenticação de declarações, a autenticação baseada em formulários ou a autenticação de banco de dados do SQL Server na conexão back-end com o Analysis Services. Esta seção fornece mais informações sobre autenticação.  
  
##  <a name="bkmk_clientApps"></a> Tarefas de conexão  
  
|Link|Descrição da tarefa|  
|----------|----------------------|  
|[Conecte-se de aplicativos cliente &#40; Analysis Services &#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)|Se você é novato no Analysis Services, leia este tópico para conhecer as ferramentas e os aplicativos mais usados no Analysis Services.|  
|[Propriedades de cadeia de caracteres de Conexão &#40; Analysis Services &#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)|O Analysis Services inclui várias propriedades de servidor e de banco de dados, permitindo que você personalize a conexão de um aplicativo específico, independentemente de como a instância ou o banco de dados está configurado.|  
|[Metodologias de autenticação com suporte no Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)|Este tópico é uma breve introdução aos métodos de autenticação usados pelo Analysis Services.|  
|[Configurar o Analysis Services para delegação restringido de Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)|Muitas soluções de business intelligence exigem a representação garantir que apenas os dados autorizados sejam retornados a cada usuário. Neste tópico, você conhecerá os requisitos para o uso da representação. Este tópico também explica as etapas de configuração do Analysis Services para autenticação restrita de Kerberos.|  
|[Registro de SPN de uma instância do Analysis Services](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)|A autenticação Kerberos requer um nome de entidade de serviço (SPN) válido para os serviços que representam ou delegam identidades de usuário em soluções de vários servidores. Use as informações deste tópico para conhecer a construção e as etapas do registro de SPN do Analysis Services.|  
|[Configurar o acesso HTTP ao Analysis Services no Internet Information Services &#40; IIS &#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|A autenticação Básica ou os limites entre domínios são dois motivos importantes para configurar o Analysis Services para acesso HTTP.|  
|[Provedores de dados usados para conexões do Analysis Services](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)|O Analysis Services fornece três bibliotecas de cliente para acessar operações do servidor ou dados do Analysis Services. Este tópico oferece uma breve introdução ao ADOMD.NET, Analysis Services Management Objects (AMO) e provedor OLE DB do Analysis Services (MSOLAP).|  
|[Desconectar usuários e sessões no servidor do Analysis Services](../../analysis-services/instances/disconnect-users-and-sessions-on-analysis-services-server.md)|Limpe as conexões e sessões existentes antes de colocar um servidor offline ou de realizar testes de desempenho de linha de base.|  
  
## <a name="see-also"></a>Consulte também  
 [Configuração de pós-instalação &#40; Analysis Services &#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md)   
 [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
  
  
