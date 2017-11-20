---
title: "Página geral da integração de serviços Designers opções | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Business_Intelligence_Designers.Data_Transformation_Designers.General
ms.assetid: d695690a-923b-4036-945e-7621e8651deb
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 599665d49b8512ec772ac5ca522cb4e0b7a521ec
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="general-page-of-integration-services-designers-options"></a>Página geral da opções dos Designers do Integration Services
  Use a página **Geral** da página **Designers do Integration Services** na caixa de diálogo **Opções** para especificar as opções de carregamento, exibição e atualização de pacotes.  
  
 Para abrir a página **Geral** , em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no menu **Ferramentas** , clique em **Opções**, expanda **Designers do Business Intelligence**e selecione **Designers do Integration Services**.  
  
## <a name="options"></a>Opções  
 **Verificar assinatura digital ao carregar um pacote**  
 Selecione para que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] verifique a assinatura digital ao carregar um pacote. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]apenas verificará se a assinatura digital está presente, é válida e é de uma fonte confiável. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]não verificará se o pacote foi alterado desde que o pacote foi assinado.  
  
 Se você definir o valor de registro **BlockedSignatureStates** , esse valor de registro substituirá a opção **Verificar assinatura digital ao carregar um pacote** . Para obter mais informações, consulte [Como implementar uma política de assinatura definindo um valor do Registro](../integration-services/packages/implement-a-signing-policy-by-setting-a-registry-value.md).  
  
 Para obter mais informações sobre certificados e pacotes digitais, consulte [Identificar a origem de pacotes com assinaturas digitais](../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md).  
  
 **Mostrar aviso se o pacote não estiver assinado**  
 Selecione para exibir um aviso ao carregar um pacote que não está assinado.  
  
 **Mostrar rótulos de restrição de precedência**  
 Selecione qual rótulo—Êxito, Falha ou Conclusão—será exibido em restrições de precedência ao exibir pacotes em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 **Idioma do script**  
 Selecione o idioma padrão de scripts para novas tarefas e componentes de Script.  
  
 **Atualizar cadeias de conexão para usar novos nomes de provedor**  
 Ao abrir ou atualizar [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] pacotes, atualize as cadeias de conexão para usar os nomes para os seguintes provedores, para a versão atual do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   Provedor OLE DB do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 O Assistente de Atualização de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] só atualiza cadeias de conexão armazenadas em gerenciadores de conexões. O assistente não atualiza cadeias de conexão construídas dinamicamente com a linguagem de expressão do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ou o código de uma tarefa Script.  
  
 **Criar nova ID de pacote**  
 Ao atualizar os pacotes de [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] , crie novas IDs de pacote para as versões atualizadas dos pacotes.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de segurança &#40; Integration Services &#41;](../integration-services/security/security-overview-integration-services.md)   
 [Estendendo pacotes com scripts](../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  

