---
title: "Caixa de di&#225;logo Converter em Modelo de Implanta&#231;&#227;o de Pacote | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.bids.converttolegacydeployment.f1"
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Caixa de di&#225;logo Converter em Modelo de Implanta&#231;&#227;o de Pacote
  A caixa de diálogo **Converter em Modelo de Implantação de Pacote** permite converter um pacote para o modelo de implantação de pacote depois de verificar se o projeto e cada pacote do projeto são compatíveis com esse modelo. Se um pacote usar recursos exclusivos para o modelo de implantação de projeto, como parâmetros, o pacote não poderá ser convertido.  
  
## Lista de Tarefas  
 Converter um pacote para o modelo de implantação de pacote exige duas etapas.  
  
1.  Quando você seleciona o comando **Converter em Modelo de Implantação de Pacote** no menu **Project** , o projeto e cada pacote do projeto terão a compatibilidade verificada com esse modelo. Os resultados são exibidos na tabela **Resultados** .  
  
     Se o projeto ou pacote falhar no teste de compatibilidade, clique em **Falha** na coluna **Resultado** para obter mais informações. Clique em **Salvar Relatório** para salvar uma cópia destas informações em um arquivo de texto.  
  
2.  Se o projeto e todos os pacotes passarem no teste de compatibilidade, clique em **OK** para converter o pacote.  
  
> **OBSERVAÇÃO:** para converter um projeto no modelo de implantação de projeto, use o **Assistente de Conversão de Projeto do Integration Services**. Para obter mais informações, consulte [Integration Services Project Conversion Wizard](https://msdn.microsoft.com/library/hh213290.aspx).  
  
## Consulte também  
 [Implantação de pacote herdado &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)   
 [Assistente de Conversão de Projeto do Integration Services](../../integration-services/packages/integration-services-project-conversion-wizard.md)  
  
  