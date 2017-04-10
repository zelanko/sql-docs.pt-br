---
title: "Identificar a origem dos pacotes com assinaturas digitais | Microsoft Docs"
ms.custom: ""
ms.date: "08/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assinando pacotes [Integration Services]"
  - "certificados [Integration Services]"
  - "pacotes [Integration Services], segurança"
  - "segurança [Integration Services], certificados"
  - "políticas de assinatura [Integration Services]"
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 46
---
# Identificar a origem dos pacotes com assinaturas digitais
  Um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode ser assinado com um certificado digital para identificar sua origem. Depois que o pacote for assinado com um certificado digital, você poderá configurar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para verificar a assinatura digital antes de carregar o pacote. Para que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verifique a assinatura, defina uma opção no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou no utilitário **dtexec** (dtexec.exe) ou defina um valor opcional do Registro.  
  
## Assinar um pacote com um certificado digital  
 Antes de assinar um pacote com um certificado digital, você tem que obter ou criar o certificado primeiro. Depois que você tiver o certificado, poderá usar este certificado para assinar o pacote. Para obter mais informações sobre como obter um certificado e assinar um pacote com esse certificado, consulte [Assinar um pacote por meio de um certificado digital](../../integration-services/packages/sign-a-package-by-using-a-digital-certificate.md).  
  
## Definir uma opção para verificar a assinatura do pacote  
 Ambos o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e o utilitário **dtexec** têm uma opção que configura o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para verificar a assinatura digital de um pacote assinado. O uso do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou do utilitário **dtexec** dependerá da ação desejada, ou seja, se você deseja verificar todos os pacotes ou apenas alguns específicos:  
  
-   Para verificar a assinatura digital de todos os pacotes antes de carregá-los no momento da criação, defina a opção **Verificar assinatura digital ao carregar um pacote** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Esta opção é uma configuração global para todos os pacotes no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].
  
-   Para verificar a assinatura digital de um pacote individual, especifique a opção **/VerifyS[igned]** quando usar o utilitário **dtexec** para executar o pacote. Para saber mais, veja [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
## Definir um valor de Registro para verificar a assinatura do pacote  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também dá suporte a um valor opcional do Registro, **BlockedSignatureStates**, que pode ser usado para gerenciar a política de uma organização para carregar pacotes assinados e não assinados. O valor do Registro pode impedir que os pacotes sejam carregados se eles não estiverem assinados, se forem inválidos ou se as assinaturas não forem confiáveis. Para obter mais informações sobre como definir esse valor do Registro, consulte [Implementar uma política de assinatura por meio da configuração de um valor do Registro](../../integration-services/packages/implement-a-signing-policy-by-setting-a-registry-value.md).  
  
> **OBSERVAÇÃO:** o valor opcional do registro **BlockedSignatureStates** pode especificar uma configuração mais restritiva do que a opção de assinatura digital definida no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou na linha de comando do **dtexec**. Nesta situação, a configuração de Registro mais restritiva substitui as outras configurações.  
  
## Consulte também  
 [Pacotes do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md)   
 [Visão geral de segurança &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
  
  