---
title: Estendendo pacotes com objetos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 26616eb8-9e80-434d-b22a-ece1b00f449d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d7384fd52f28f52647c310f7c76eec994b8c8141
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896204"
---
# <a name="extending-packages-with-custom-objects"></a>Estendendo pacotes com objetos personalizados
  Se os componentes fornecidos no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não atenderem às suas necessidades, você poderá ampliar a capacidade do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com a codificação de suas próprias extensões. Há duas opções distintas para estender seus pacotes: você pode escrever código dentro dos wrappers avançados fornecidos pela tarefa e o componente Script, ou pode criar extensões personalizadas do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a partir do zero com a derivação das classes base fornecidas pelo modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Essa seção explora a opção mais avançada – extensão de pacotes com objetos personalizados.  
  
 Quando sua solução personalizada do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necessita de maior flexibilidade do que a tarefa Script e o componente Script oferecem, ou quando você necessita de um componente que possa ser reutilizado em vários pacotes, o modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] possibilita a criação de tarefas personalizadas, componentes de fluxo de dados e outros objetos de pacote em código gerenciado do início ao fim.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Desenvolvendo objetos personalizados para o Integration Services](developing-custom-objects-for-integration-services.md)  
 Aborda os objetos personalizados que podem ser criados no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e resume as etapas e configurações essenciais.  
  
 [Persistência de objetos personalizados](persisting-custom-objects.md)  
 Discute a persistência padrão de objetos personalizados e o processo de implementação da persistência personalizada.  
  
 [Compilando, implantando e depurando objetos personalizados](building-deploying-and-debugging-custom-objects.md)  
 Discute as abordagens comuns para criar, implantar e testar os diversos tipos de objetos personalizados.  
  
 [Desenvolver uma tarefa personalizada](task/developing-a-custom-task.md)  
 Descreve o processo de codificação de uma tarefa personalizada.  
  
 [Desenvolver um gerenciador de conexões personalizado](connection-manager/developing-a-custom-connection-manager.md)  
 Descreve o processo de codificação de um gerenciador de conexões personalizado.  
  
 [Desenvolver um provedor de log personalizado](log-provider/developing-a-custom-log-provider.md)  
 Descreve o processo de codificação de um provedor de logs personalizado.  
  
 [Desenvolver um enumerador ForEach personalizado](foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Descreve o processo de codificação de um enumerador personalizado.  
  
 [Desenvolver um componente de fluxo de dados personalizado](data-flow/developing-a-custom-data-flow-component.md)  
 Aborda como programar origens, transformações e destinos de fluxos de dados personalizados.  
  
## <a name="reference"></a>Referência  
 [Referência de mensagens e erros do Integration Services](../integration-services-error-and-message-reference.md)  
 Lista os códigos de erro predefinidos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com seus nomes simbólicos e descrições.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Estender pacotes com scripts](../extending-packages-scripting/extending-packages-with-scripting.md)  
 Discute como estender o fluxo de controle usando a tarefa Script ou estender o fluxo de dados usando o componente Script.  
  
 [Compilar Pacotes Programaticamente](../building-packages-programmatically/building-packages-programmatically.md)  
 Descreve como criar, configurar, executar, carregar, salvar e gerenciar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] programaticamente.  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Comparar soluções de script e objetos personalizados](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
