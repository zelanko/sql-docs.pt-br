---
title: Estendendo pacotes com objetos personalizados | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 26616eb8-9e80-434d-b22a-ece1b00f449d
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40903d65bfbd65c78951f0954d3e5bd7380afa98
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="extending-packages-with-custom-objects"></a>Estendendo pacotes com objetos personalizados
  Se os componentes fornecidos no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não atenderem às suas necessidades, você poderá ampliar a capacidade do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com a codificação de suas próprias extensões. Há duas opções distintas para estender seus pacotes: você pode escrever código dentro dos wrappers avançados fornecidos pela tarefa e o componente Script, ou pode criar extensões personalizadas do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a partir do zero com a derivação das classes base fornecidas pelo modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Essa seção explora a opção mais avançada – extensão de pacotes com objetos personalizados.  
  
 Quando sua solução personalizada do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necessita de maior flexibilidade do que a tarefa Script e o componente Script oferecem, ou quando você necessita de um componente que possa ser reutilizado em vários pacotes, o modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] possibilita a criação de tarefas personalizadas, componentes de fluxo de dados e outros objetos de pacote em código gerenciado do início ao fim.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Desenvolvendo objetos personalizados para o Integration Services](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Aborda os objetos personalizados que podem ser criados no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e resume as etapas e configurações essenciais.  
  
 [Persistência de objetos personalizados](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 Discute a persistência padrão de objetos personalizados e o processo de implementação da persistência personalizada.  
  
 [Compilando, implantando e depurando objetos personalizados](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Discute as abordagens comuns para criar, implantar e testar os diversos tipos de objetos personalizados.  
  
 [Desenvolver uma tarefa personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 Descreve o processo de codificação de uma tarefa personalizada.  
  
 [Desenvolver um gerenciador de conexões personalizado](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Descreve o processo de codificação de um gerenciador de conexões personalizado.  
  
 [Desenvolver um provedor de log personalizado](../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Descreve o processo de codificação de um provedor de logs personalizado.  
  
 [Desenvolver um enumerador ForEach personalizado](../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Descreve o processo de codificação de um enumerador personalizado.  
  
 [Desenvolver um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 Aborda como programar origens, transformações e destinos de fluxos de dados personalizados.  
  
## <a name="reference"></a>Referência  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
 Lista os códigos de erro predefinidos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com seus nomes simbólicos e descrições.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Estender pacotes com scripts](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 Discute como estender o fluxo de controle usando a tarefa Script ou estender o fluxo de dados usando o componente Script.  
  
 [Compilar Pacotes Programaticamente](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 Descreve como criar, configurar, executar, carregar, salvar e gerenciar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] programaticamente.  
  
## <a name="see-also"></a>Consulte também  
 [Comparar soluções de script e objetos personalizados](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
