---
title: Assinar um pacote usando um certificado Digital | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- digital signatures [Integration Services]
- signing packages [Integration Services]
- signatures [Integration Services]
ms.assetid: 182b115e-0fe2-4717-8dff-183f9eb6e397
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c6da9652c18bd6e8093a38d337b61171bc448341
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766598"
---
# <a name="sign-a-package-by-using-a-digital-certificate"></a>Assinar um pacote por meio de um certificado digital
  Este tópico descreve como assinar um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] com um certificado digital. Você pode usar uma assinatura digital, junto com outras configurações, para evitar o carregamento e a execução de um pacote inválido.  
  
 Antes de poder assinar um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , você deve realizar as seguintes tarefas:  
  
-   Criar ou obter uma chave privada a ser associada ao certificado e armazenar esta chave no computador local.  
  
-   Obter um certificado com a finalidade de assinatura de código de uma autoridade de certificação confiável. Você pode usar um dos métodos a seguir para obter ou criar um certificado:  
  
    -   Obtenha um certificado de uma autoridade de certificação comercial pública que emite certificados.  
  
    -   Obtenha um certificado de um servidor de certificados, que permita que uma organização emita certificados internamente. É necessário adicionar o certificado raiz usado para assinar o certificado ao armazenamento **Autoridades de Certificação Raiz Confiáveis** . Para adicionar o certificado raiz, você pode usar o snap-in de Certificados para o [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console (MMC). Para obter mais informações, consulte o tópico “[Serviços de certificado](https://go.microsoft.com/fwlink/?LinkId=100755)” na biblioteca do MSDN.  
  
    -   Crie seu próprio certificado somente para teste. A Ferramenta de Criação de Certificado (Makecert.exe) gera certificados X.509 para teste. Para obter mais informações, consulte o tópico “[Ferramenta de Criação de Certificado (Makecert.exe)](https://go.microsoft.com/fwlink/?LinkId=100756)” na Biblioteca MSDN.  
  
     Para obter mais informações sobre certificados, consulte a Ajuda online do snap-in de Certificados. Para obter mais informações sobre como assinar ativos digitais, consulte o tópico “[Assinando e verificando o código com o Authenticode](https://go.microsoft.com/fwlink/?LinkId=78100)” na biblioteca do MSDN.  
  
-   Verifique se o certificado foi habilitado para assinatura de código. Para saber se um certificado está habilitado para assinatura de código, revise as propriedades do certificado no snap-in de Certificados.  
  
-   Armazene o certificado no armazenamento Pessoal.  
  
 Depois de concluir as tarefas anteriores, realize o procedimento a seguir para assinar um pacote.  
  
### <a name="to-sign-a-package"></a>Para assinar um pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote a ser assinado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer, no menu **SSIS** , clique em **Assinatura Digital**.  
  
4.  Na caixa de diálogo **Assinatura Digital** , clique em **Assinar**.  
  
5.  Na caixa de diálogo **Selecionar um Certificado** , selecione um certificado.  
  
6.  (Opcional) Clique em **Exibir Certificado**para exibir informações do certificado.  
  
7.  Clique em **OK** para fechar a caixa de diálogo **Selecionar um Certificado** .  
  
8.  Clique em **OK** para fechar a caixa de diálogo **Assinatura Digital** .  
  
9. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
     Embora o pacote tenha sido assinado, é necessário configurar o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para verificar a assinatura digital antes de carregar o pacote. Para obter mais informações, consulte [Identificar a origem de pacotes com assinaturas digitais](security/identify-the-source-of-packages-with-digital-signatures.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de segurança &#40;Integration Services&#41;](security/security-overview-integration-services.md)  
  
  
