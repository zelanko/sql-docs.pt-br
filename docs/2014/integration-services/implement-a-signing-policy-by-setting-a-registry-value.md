---
title: Implementar uma política de assinatura definindo um valor de registro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing policies [Integration Services]
ms.assetid: 64f6966f-2292-401f-acb1-2ccb5aee484a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 776a8319750721f3b489df1a3a4466c7dc36f15e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968316"
---
# <a name="implement-a-signing-policy-by-setting-a-registry-value"></a>Implementar uma política de assinatura por meio da configuração de um valor do Registro
  Você pode usar um valor opcional do Registro para gerenciar uma política da organização para carregar pacotes assinados ou não assinados. Se você usar o valor do Registro, será preciso criar esse valor em cada computador em que os pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] serão executados e no qual deseja aplicar a política. Depois que o valor do Registro tiver sido definido, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] verificará as assinaturas antes de carregar pacotes.  
  
 O procedimento deste tópico descreve como adicionar o valor opcional DWORD de `BlockedSignatureStates` para a chave do Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS. Os valores de dados no `BlockedSignatureStates` determinam se um pacote deve ser bloqueado se possuir uma assinatura não confiável, uma assinatura inválida ou não esteja assinado. Com relação ao status das assinaturas usadas para assinar os pacotes, o valor do Registro `BlockedSignatureStates` usa as seguintes definições:  
  
-   Uma *assinatura válida* é aquela que pode ser lida com êxito.  
  
-   Uma *assinatura inválida* é aquela em que a soma de verificação descriptografada (o hash unidirecional do código de pacote criptografado por uma chave privada) não corresponde à soma de verificação descriptografada calculada como parte do processo de carregamento de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
-   Uma *assinatura confiável* é aquela criada usando um certificado digital assinado por uma Autoridade de Certificação Raiz Confiável. Essa configuração não exige que o signatário esteja na lista do usuário de Fornecedores Confiáveis.  
  
-   Uma *assinatura não confiável* é aquela que não é possível verificar se foi emitida por uma Autoridade de Certificação Raiz Confiável ou é uma assinatura que não é atual.  
  
 A tabela a seguir lista os valores válidos dos dados de DWORD e sua política associada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Nenhuma restrição administrativa.|  
|1|Bloquear assinaturas inválidas.<br /><br /> Essa configuração não bloqueia pacotes não assinados.|  
|2|Bloquear assinaturas inválidas e não confiáveis.<br /><br /> Essa configuração não bloqueia pacotes não assinados, mas bloqueia assinaturas geradas automaticamente.|  
|3|Bloquear assinaturas inválidas e não confiáveis e pacotes não assinados<br /><br /> Essa configuração também bloqueia assinaturas geradas automaticamente.|  
  
> [!NOTE]  
>  A configuração recomendada para é `BlockedSignatureStates` é 3. Essa configuração fornece maior proteção contra pacotes não assinados ou assinaturas que não são válidas nem confiáveis. Porém, a configuração recomendada talvez não seja apropriada em todas as circunstâncias. Para obter mais informações sobre como assinar ativos digitais, consulte o tópico "[Introdução à assinatura de código](https://go.microsoft.com/fwlink/?LinkId=51414)", na biblioteca do MSDN.  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>Para implementar uma política de assinatura para pacotes  
  
1.  No menu **Iniciar**, clique em **Executar**.  
  
2.  Na caixa de diálogo Executar, digite `Regedit` e clique em **OK**.  
  
3.  Localize a chave do Registro, HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS.  
  
4.  Clique com o botão direito do mouse em **MSDTS**, aponte para **Novo**e clique em **Valor DWORD**.  
  
5.  Atualize o nome do valor novo para `BlockedSignatureStates`.  
  
6.  Clique com o botão direito do mouse `BlockedSignatureStates` e clique em **Modificar**.  
  
7.  Na caixa de diálogo **Editar valor DWORD** , digite o valor 0, 1, 2 ou 3.  
  
8.  Clique em **OK**.  
  
9. No menu **Arquivo** , clique em **Sair**.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral de segurança &#40;Integration Services&#41;](security/security-overview-integration-services.md)   
 [Identificar a origem dos pacotes com assinaturas digitais](security/identify-the-source-of-packages-with-digital-signatures.md)  
  
  
