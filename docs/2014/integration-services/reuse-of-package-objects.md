---
title: Reutilização de objetos do pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: ab572e7c0793f9d3a673698bf54a0109ad42551c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379984"
---
# <a name="reuse-of-package-objects"></a>Reutilizar objetos de pacote
  Agrupa frequentemente as funcionalidades que você deseja usar. Por exemplo, se você criou um conjunto de tarefas, poderá reutilizar os itens juntos como um grupo ou como um único item, como um gerenciador de conexões que você criou em um projeto diferente do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="copy-and-paste"></a>Copiar e colar  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer support copying e pasting package objects, which can include control flow items, data flow items, e connection managers. Você pode copiar e colar entre projetos e entre pacotes. Se a solução contiver múltiplos projetos, você poderá copiar entre projetos e os projetos podem ser de tipos diferentes.  
  
 Se uma solução contiver múltiplos pacotes, você poderá copiar e colar entre eles. Os pacotes podem estar nos mesmos projetos ou em projetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] diferentes. Entretanto, objetos de pacote podem ter dependências em outros objetos, sem os quais eles não são válidos. Por exemplo, uma tarefa Executar SQL usa um gerenciador de conexões, que você também deve copiar para que a tarefa funcione. Além disso, alguns objetos de pacote exigem que o pacote já contenha um determinado objeto, e sem esse objeto você não pode colar os objetos copiados com sucesso para um pacote. Por exemplo, você não pode colar um fluxo de dados em um pacote que não tenha, no mínimo, uma tarefa de Fluxo de Dados.  
  
 Você pode descobrir que pode copiar os mesmos pacotes repetidamente. Para evitar o processo de cópia, você pode designar estes pacotes como modelos e usá-los quando criar novos pacotes.  
  
 Quando você copia um objeto de pacote, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] automaticamente atribui uma nova GUID para a propriedade `ID` do novo objeto e atualiza a propriedade `Name`.  
  
 Você não pode copiar variáveis. Se um objeto como uma tarefa usar variáveis, então você deve recriar as variáveis no pacote de destino. Por outro lado, se você copiar o pacote inteiro, as variáveis no pacote também serão copiadas.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Copiar objetos de pacote](../../2014/integration-services/copy-package-objects.md)  
  
-   [Copiar itens do projeto](../../2014/integration-services/copy-project-items.md)  
  
-   [Salvar um pacote como um modelo de pacote](../../2014/integration-services/save-a-package-as-a-package-template.md)  
  
  
