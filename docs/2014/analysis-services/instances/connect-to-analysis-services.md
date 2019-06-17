---
title: Conectar-se ao Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- instances of Analysis Services, connections
ms.assetid: 73ee8171-3379-4384-bfc8-071b3eebbc8f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 654d659900d01ae9d5caf5188b9146510de483ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080117"
---
# <a name="connect-to-analysis-services"></a>Conectar ao Analysis Services
  Utilize as informações desta seção para saber mais sobre as propriedades de cadeia de conexão, as bibliotecas de cliente utilizadas para conexões, os métodos de autenticação com suporte pelo Analysis Services e como definir ou limpar conexões antes de colocar um servidor offline.  
  
## <a name="analysis-services-connections"></a>Conexões do Analysis Services  
 O Analysis Services usa o TCP como protocolo de rede e o XMLA como protocolo de comunicação. No nível inferior, todas as bibliotecas de cliente fornecidas com o Analysis Services implementam o XMLA sobre TCP. Embora seja possível criar aplicativos com base no XMLA bruto, a maioria dos aplicativos e desenvolvedores de aplicativos usam bibliotecas de cliente para tirar proveito dos modelos de objeto e das eficiências de codificação que eles fornecem. Para conexões de cliente com o Analysis Services, é possível utilizar o IIS como uma conexão intermediária se não for possível utilizar o TCP em toda a pilha. Uma vantagem de utilizar o acesso HTTP por meio do IIS é a capacidade de conexão de aplicativos que passam credenciais na cadeia de conexão.  
  
 Qualquer discussão que envolva conectividade normalmente inclui a autenticação. Em comparação a outros recursos do SQL Server, o Analysis Services utiliza credencias exclusivamente do Windows. Não é possível utilizar o resumo, a autenticação de declarações, a autenticação baseada em formulários ou a autenticação de banco de dados do SQL Server na conexão back-end com o Analysis Services. Esta seção fornece mais informações sobre autenticação.  
  
##  <a name="bkmk_clientApps"></a> Tarefas de conexão  
  
|Link|Descrição da tarefa|  
|----------|----------------------|  
|[Conectar-se de aplicativos cliente &#40;Analysis Services&#41;](connect-from-client-applications-analysis-services.md)|Se você é novato no Analysis Services, leia este tópico para conhecer as ferramentas e os aplicativos mais usados no Analysis Services.|  
|[Propriedades de cadeia de conexão &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md)|O Analysis Services inclui várias propriedades de servidor e de banco de dados, permitindo que você personalize a conexão de um aplicativo específico, independentemente de como a instância ou o banco de dados está configurado.|  
|[Metodologias de autenticação com suporte no Analysis Services](authentication-methodologies-supported-by-analysis-services.md)|Este tópico é uma breve introdução aos métodos de autenticação usados pelo Analysis Services.|  
|[Configurar o Analysis Services para delegação restrita de Kerberos](configure-analysis-services-for-kerberos-constrained-delegation.md)|Muitas soluções de business intelligence exigem a representação garantir que apenas os dados autorizados sejam retornados a cada usuário. Neste tópico, você conhecerá os requisitos para o uso da representação. Este tópico também explica as etapas de configuração do Analysis Services para autenticação restrita de Kerberos.|  
|[Registro de SPN de uma instância do Analysis Services](spn-registration-for-an-analysis-services-instance.md)|A autenticação Kerberos requer um nome de entidade de serviço (SPN) válido para os serviços que representam ou delegam identidades de usuário em soluções de vários servidores. Use as informações deste tópico para conhecer a construção e as etapas do registro de SPN do Analysis Services.|  
|[Configurar o acesso HTTP ao Analysis Services no IIS &#40;(Serviços de Informações da Internet)&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md)|A autenticação Básica ou os limites entre domínios são dois motivos importantes para configurar o Analysis Services para acesso HTTP.|  
|[Provedores de dados usados em conexões do Analysis Services](data-providers-used-for-analysis-services-connections.md)|O Analysis Services fornece três bibliotecas de cliente para acessar operações do servidor ou dados do Analysis Services. Este tópico oferece uma breve introdução ao ADOMD.NET, Analysis Services Management Objects (AMO) e provedor OLE DB do Analysis Services (MSOLAP).|  
|[Desconectar usuários e sessões no Analysis Services Server](disconnect-users-and-sessions-on-analysis-services-server.md)|Limpe as conexões e sessões existentes antes de colocar um servidor offline ou de realizar testes de desempenho de linha de base.|  
  
## <a name="see-also"></a>Consulte também  
 [Configuração de pós-instalação &#40;Analysis Services&#41;](post-install-configuration-analysis-services.md)   
 [Configurar propriedades de servidor no Analysis Services](../server-properties/server-properties-in-analysis-services.md)   
 [Script de tarefas administrativas no Analysis Services](../script-administrative-tasks-in-analysis-services.md)  
  
  
