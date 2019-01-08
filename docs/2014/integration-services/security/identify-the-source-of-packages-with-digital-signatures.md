---
title: Identificar a origem dos pacotes com assinaturas digitais | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8e1bf17207e57f8488e10c6b37cc7fa876d511b4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52798908"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>Identificar a origem dos pacotes com assinaturas digitais
  Um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode ser assinado com um certificado digital para identificar sua origem. Depois que o pacote for assinado com um certificado digital, você poderá configurar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para verificar a assinatura digital antes de carregar o pacote. Para que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verifique a assinatura, defina uma opção no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou no utilitário **dtexec** (dtexec.exe) ou defina um valor opcional do Registro.  
  
## <a name="signing-a-package-with-a-digital-certificate"></a>Assinando um pacote com um certificado digital  
 Antes de assinar um pacote com um certificado digital, você tem que obter ou criar o certificado primeiro. Depois que você tiver o certificado, poderá usar este certificado para assinar o pacote. Para obter mais informações sobre como obter um certificado e assinar um pacote com esse certificado, consulte [Assinar um pacote por meio de um certificado digital](../sign-a-package-by-using-a-digital-certificate.md).  
  
## <a name="setting-an-option-to-check-the-package-signature"></a>Definindo uma opção para verificar a assinatura do pacote  
 Ambos o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e o utilitário **dtexec** têm uma opção que configura o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para verificar a assinatura digital de um pacote assinado. O uso do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou do utilitário **dtexec** dependerá da ação desejada, ou seja, se você deseja verificar todos os pacotes ou apenas alguns específicos:  
  
-   Para verificar a assinatura digital de todos os pacotes antes de carregá-los no momento da criação, defina a opção **Verificar assinatura digital ao carregar um pacote** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Esta opção é uma configuração global para todos os pacotes no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obter mais informações, consulte [General Page](../general-page-of-integration-services-designers-options.md).  
  
-   Para verificar a assinatura digital de um pacote individual, especifique o `/VerifyS[igned]` opção quando você usa o **dtexec** utilitário para executar o pacote. Para saber mais, veja [dtexec Utility](../packages/dtexec-utility.md).  
  
## <a name="setting-a-registry-value-to-check-the-package-signature"></a>Definindo um valor do Registro para verificar a assinatura do pacote  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também dá suporte a um valor opcional do Registro, **BlockedSignatureStates**, que pode ser usado para gerenciar a política de uma organização para carregar pacotes assinados e não assinados. O valor do Registro pode impedir que os pacotes sejam carregados se eles não estiverem assinados, se forem inválidos ou se as assinaturas não forem confiáveis. Para obter mais informações sobre como definir esse valor do Registro, consulte [Implementar uma política de assinatura por meio da configuração de um valor do Registro](../implement-a-signing-policy-by-setting-a-registry-value.md).  
  
> [!NOTE]  
>  O valor opcional do Registro **BlockedSignatureStates** pode especificar uma configuração mais restritiva do que a opção de assinatura digital definida no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou na linha de comando do **dtexec** . Nesta situação, a configuração de Registro mais restritiva substitui as outras configurações.  
  
## <a name="see-also"></a>Consulte também  
 [Pacotes do Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md)   
 [Visão geral de segurança &#40;Integration Services&#41;](security-overview-integration-services.md)  
  
  
