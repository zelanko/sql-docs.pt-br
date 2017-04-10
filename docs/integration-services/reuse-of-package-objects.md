---
title: "Reutilizar objetos de pacote | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "regeneração do GUID [Integration Services]"
  - "reutilizando pacotes"
  - "modelos [Integration Services]"
  - "copiando pacotes"
  - "regenerando GUID do pacote"
ms.assetid: 08f723bf-15b5-44bd-9a46-04e8781bfbfb
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Reutilizar objetos de pacote
  Agrupa frequentemente as funcionalidades que você deseja usar. Por exemplo, se você criou um conjunto de tarefas, poderá reutilizar os itens juntos como um grupo ou como um único item, como um gerenciador de conexões que você criou em um projeto diferente do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## Copiar e colar  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer support copying e pasting package objects, which can include control flow items, data flow items, e connection managers. Você pode copiar e colar entre projetos e entre pacotes. Se a solução contiver múltiplos projetos, você poderá copiar entre projetos e os projetos podem ser de tipos diferentes.  
  
 Se uma solução contiver múltiplos pacotes, você poderá copiar e colar entre eles. Os pacotes podem estar nos mesmos projetos ou em projetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] diferentes. Entretanto, objetos de pacote podem ter dependências em outros objetos, sem os quais eles não são válidos. Por exemplo, uma tarefa Executar SQL usa um gerenciador de conexões, que você também deve copiar para que a tarefa funcione. Além disso, alguns objetos de pacote exigem que o pacote já contenha um determinado objeto, e sem esse objeto você não pode colar os objetos copiados com sucesso para um pacote. Por exemplo, você não pode colar um fluxo de dados em um pacote que não tenha, no mínimo, uma tarefa de Fluxo de Dados.  
  
 Você pode descobrir que pode copiar os mesmos pacotes repetidamente. Para evitar o processo de cópia, você pode designar estes pacotes como modelos e usá-los quando criar novos pacotes.  
  
 Quando você copia um objeto de pacote, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] automaticamente atribui uma nova GUID à propriedade de **ID** do novo objeto e atualiza a propriedade **Nome**.  
  
 Você não pode copiar variáveis. Se um objeto como uma tarefa usar variáveis, então você deve recriar as variáveis no pacote de destino. Por outro lado, se você copiar o pacote inteiro, as variáveis no pacote também serão copiadas.  
  
## Tarefas relacionadas  
  
-   [Copiar objetos de pacote](../integration-services/copy-package-objects.md)  
  
-   [Copiar itens do projeto](../Topic/Copy%20Project%20Items.md)  
  
-   [Salvar um pacote como um modelo de pacote](../Topic/Save%20a%20Package%20as%20a%20Package%20Template.md)  
  
  