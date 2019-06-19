---
title: Reutilização de objetos do pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- GUID regenerating [Integration Services]
- reusing packages
- templates [Integration Services]
- copying packages
- regenerating package GUID
ms.assetid: 08f723bf-15b5-44bd-9a46-04e8781bfbfb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6844adf38e6139a050cf1f97200323704f8a8ff2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65719336"
---
# <a name="reuse-of-package-objects"></a>Reutilizar objetos de pacote

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Agrupa frequentemente as funcionalidades que você deseja usar. Por exemplo, se você criou um conjunto de tarefas, poderá reutilizar os itens juntos como um grupo ou como um único item, como um gerenciador de conexões que você criou em um projeto diferente do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="copy-and-paste"></a>Copiar e colar  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer support copying e pasting package objects, which can include control flow items, data flow items, e connection managers. Você pode copiar e colar entre projetos e entre pacotes. Se a solução contiver múltiplos projetos, você poderá copiar entre projetos e os projetos podem ser de tipos diferentes.  
  
 Se uma solução contiver múltiplos pacotes, você poderá copiar e colar entre eles. Os pacotes podem estar nos mesmos projetos ou em projetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] diferentes. Entretanto, objetos de pacote podem ter dependências em outros objetos, sem os quais eles não são válidos. Por exemplo, uma tarefa Executar SQL usa um gerenciador de conexões, que você também deve copiar para que a tarefa funcione. Além disso, alguns objetos de pacote exigem que o pacote já contenha um determinado objeto, e sem esse objeto você não pode colar os objetos copiados com sucesso para um pacote. Por exemplo, você não pode colar um fluxo de dados em um pacote que não tenha, no mínimo, uma tarefa de Fluxo de Dados.  
  
 Você pode descobrir que pode copiar os mesmos pacotes repetidamente. Para evitar o processo de cópia, você pode designar estes pacotes como modelos e usá-los quando criar novos pacotes.  
  
 Quando você copia um objeto de pacote, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] automaticamente atribui uma nova GUID à propriedade de **ID** do novo objeto e atualiza a propriedade **Nome** .  
  
 Você não pode copiar variáveis. Se um objeto como uma tarefa usar variáveis, então você deve recriar as variáveis no pacote de destino. Por outro lado, se você copiar o pacote inteiro, as variáveis no pacote também serão copiadas.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Copiar objetos de pacote](../integration-services/copy-package-objects.md)  
  
-   [Copiar itens do projeto](https://msdn.microsoft.com/library/1606c54d-20f9-49f3-a4ef-caad83a772aa)  
  
-   [Salvar um pacote como um modelo de pacote](https://msdn.microsoft.com/library/efe66cec-3933-4f6e-8d35-fe3d300de66c)  
  
  
