---
title: Documentação do desenvolvedor do Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 067b1f69-84eb-4a13-b220-120cd63704b4
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 18f13cbe1c5d7c3a281ee3c3ad542b2f5281a74f
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488337"
---
# <a name="master-data-services-developer-documentation"></a>Documentação do desenvolvedor do Master Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Localize informações sobre como gravar código para personalizar o modo como você e seus usuários interagem com o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Saiba como:  
  
-   Escreva um programa que acesse o serviço Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . O serviço Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] é um serviço WCF (Windows Communication Foundation) que os desenvolvedores usam para controlar recursos do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] por meio de código.  
  
-   Incorpore recursos do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] nos aplicativos existentes.  
  
-   Escreva código para executar ações repetitivas ou complexas que são difíceis ou impossíveis de realizar com a interface de usuário do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
-   Crie um fluxo de trabalho personalizado que seja executado em resposta a uma regra de negócio especificada por você. Um fluxo de trabalho personalizado chama o código que você escreve, que pode executar qualquer em ação necessária para processar o fluxo de trabalho.  
  
## <a name="master-data-manager-web-service"></a>Serviço Web Master Data Manager  
 O serviço Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] permite a você fazer uso programático dos recursos do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] de qualquer computador que possa acessar seu site do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . Antes de começar a gravar código para acessar o serviço Web, você deve gerar classes proxy, que estão contidas em um namespace que você especifica. Esta documentação usa <xref:Microsoft.MasterDataServices> como o namespace de proxy. A classe proxy principal que você usa para executar operações de serviço Web é a classe <xref:Microsoft.MasterDataServices.ServiceClient>, que implementa a interface <xref:Microsoft.MasterDataServices.IService>. De seu código, chame métodos da classe <xref:Microsoft.MasterDataServices.ServiceClient> para acessar o serviço Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. O restante das classes no namespace é usado pelas operações de serviço Web.  
  
### <a name="web-service-content"></a>Conteúdo do serviço Web  
 [Criar classes proxy do serviço Web do Master Data Manager](../../master-data-services/develop/create-master-data-manager-web-service-proxy-classes.md)  
 Descreve como habilitar a publicação de metadados do site do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e como criar classes proxy que podem ser usadas para acessar programaticamente as operações do serviço Web.  
  
 [Operações de serviço Web categorizadas &#40;Master Data Services&#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
 Uma lista categorizada das operações de serviço Web da classe <xref:Microsoft.MasterDataServices.ServiceClient>.  
  
## <a name="custom-workflows"></a>Fluxos de trabalho personalizados  
 O [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] usa regras de negócios para criar soluções de fluxo de trabalho básicas. Você pode atualizar e validar dados automaticamente e pode configurar o envio de notificações por email com base nas condições especificadas. As regras de negócios no [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] devem gerenciar os cenários de fluxo de trabalho mais comuns. Se seu fluxo de trabalho exigir o processamento de eventos mais complexos, como aprovações em várias camadas ou árvores de decisão complexas, você poderá configurar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para enviar dados a um assembly personalizado criado por você. Para tratar fluxos de trabalho personalizados, você deve configurar e iniciar o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server no computador do aplicativo Web e criar um assembly que implementa a interface <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>.  
  
### <a name="custom-workflow-content"></a>Conteúdo de fluxo de trabalho personalizado  
 [Criar um fluxo de trabalho personalizado &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
 Instruções sobre como criar um assembly de manipulador de fluxo de trabalho, como configurar e iniciar o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server e como criar uma regra de negócio no [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] que inicia um fluxo de trabalho personalizado.  
  
## <a name="web-server-namespaces"></a>Namespaces do servidor Web  
 O [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] instala um conjunto de assemblies no computador do servidor Web. Esses assemblies contêm namespaces que podem ser usados para cenários avançados que personalizam o comportamento do computador do servidor Web. A tabela a seguir descreve esses namespaces.  
  
|Namespace|Descrição|  
|---------------|-----------------|  
|<xref:Microsoft.MasterDataServices.Deployment>|Contém classes que podem ser usadas para criar um pacote de implantação de um modelo e para implantar um pacote em um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|  
|<xref:Microsoft.MasterDataServices.Services>|Contém uma classe que recebe e processa operações de serviço Web feitas no computador do servidor Web por meio do aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .|  
|<xref:Microsoft.MasterDataServices.Services.DataContracts>|Contém classes que definem como os dados são transmitidos do computador cliente por meio do aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] para o computador do servidor Web.|  
|<xref:Microsoft.MasterDataServices.Services.MessageContracts>|Contém classes que definem como as solicitações e as respostas são transmitidas do computador cliente por meio do aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] para o computador do servidor Web.|  
|<xref:Microsoft.MasterDataServices.Services.ServiceContracts>|Contém a interface que define as operações que podem ser chamadas por meio do serviço Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .|  
  
  
