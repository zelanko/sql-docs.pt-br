---
title: Identificar a origem dos pacotes com assinaturas digitais | Microsoft Docs
ms.custom: security
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.digitalsigning.f1
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 84922b21e074cbef8afe233e41746a51dfd13d20
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922027"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>Identificar a origem dos pacotes com assinaturas digitais

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode ser assinado com um certificado digital para identificar sua origem. Depois que o pacote for assinado com um certificado digital, você poderá configurar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para verificar a assinatura digital antes de carregar o pacote. Para que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verifique a assinatura, defina uma opção no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou no utilitário **dtexec** (dtexec.exe) ou defina um valor opcional do Registro.  
  
## <a name="sign-a-package-with-a-digital-certificate"></a>Assinar um pacote com um certificado digital  
 Antes de assinar um pacote com um certificado digital, você tem que obter ou criar o certificado primeiro. Depois que você tiver o certificado, poderá usar este certificado para assinar o pacote. Para obter mais informações sobre como obter um certificado e assinar um pacote com esse certificado, consulte [Assinar um pacote por meio de um certificado digital](#cert).  
  
## <a name="set-an-option-to-check-the-package-signature"></a>Definir uma opção para verificar a assinatura do pacote  
 Ambos o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e o utilitário **dtexec** têm uma opção que configura o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para verificar a assinatura digital de um pacote assinado. O uso do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou do utilitário **dtexec** dependerá da ação desejada, ou seja, se você deseja verificar todos os pacotes ou apenas alguns específicos:  
  
-   Para verificar a assinatura digital de todos os pacotes antes de carregá-los no momento da criação, defina a opção **Verificar assinatura digital ao carregar um pacote** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Esta opção é uma configuração global para todos os pacotes no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].
  
-   Para verificar a assinatura digital de um pacote individual, especifique a opção **/VerifyS[igned]** quando usar o utilitário **dtexec** para executar o pacote. Para saber mais, veja [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
## <a name="set-a-registry-value-to-check-package-signature"></a>Definir um valor de Registro para verificar a assinatura do pacote  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também dá suporte a um valor opcional do Registro, **BlockedSignatureStates**, que pode ser usado para gerenciar a política de uma organização para carregar pacotes assinados e não assinados. O valor do Registro pode impedir que os pacotes sejam carregados se eles não estiverem assinados, se forem inválidos ou se as assinaturas não forem confiáveis. Para obter mais informações sobre como definir esse valor do Registro, consulte [Implementar uma política de assinatura por meio da configuração de um valor do Registro](#registry).  
  
> **OBSERVAÇÃO:** o valor opcional do registro **BlockedSignatureStates** pode especificar uma configuração mais restritiva do que a opção de assinatura digital definida no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou na linha de comando do **dtexec** . Nesta situação, a configuração de Registro mais restritiva substitui as outras configurações.  

## <a name="implement-a-signing-policy-by-setting-a-registry-value"></a><a name="registry"></a> Implementar uma política de assinatura por meio da configuração de um valor do Registro
  Você pode usar um valor opcional do Registro para gerenciar uma política da organização para carregar pacotes assinados ou não assinados. Se você usar o valor do Registro, será preciso criar esse valor em cada computador em que os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] serão executados e no qual deseja aplicar a política. Depois que o valor do Registro tiver sido definido, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verificará as assinaturas antes de carregar pacotes.  
  
 Esse procedimento deste tópico descreve como adicionar o valor opcional **BlockedSignatureStates** DWORD para a chave do Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS. Os valores de dados no **BlockedSignatureStates** determinam se um pacote deverá ser bloqueado se tiver uma assinatura não confiável, uma assinatura inválida ou não esteja assinado. Com relação ao status das assinaturas usadas para assinar os pacotes, o valor do Registro **BlockedSignatureStates** usa as seguintes definições:  
  
-   Uma *assinatura válida* é aquela que pode ser lida com êxito.  
  
-   Uma *assinatura inválida* é aquela em que a soma de verificação descriptografada (o hash unidirecional do código de pacote criptografado por uma chave privada) não corresponde à soma de verificação descriptografada calculada como parte do processo de carregamento de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   Uma *assinatura confiável* é aquela criada usando um certificado digital assinado por uma Autoridade de Certificação Raiz Confiável. Essa configuração não exige que o signatário esteja na lista do usuário de Fornecedores Confiáveis.  
  
-   Uma *assinatura não confiável* é aquela que não é possível verificar se foi emitida por uma Autoridade de Certificação Raiz Confiável ou é uma assinatura que não é atual.  
  
 A tabela a seguir lista os valores válidos dos dados de DWORD e sua política associada.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|0|Nenhuma restrição administrativa.|  
|1|Bloquear assinaturas inválidas.<br /><br /> Essa configuração não bloqueia pacotes não assinados.|  
|2|Bloquear assinaturas inválidas e não confiáveis.<br /><br /> Essa configuração não bloqueia pacotes não assinados, mas bloqueia assinaturas geradas automaticamente.|  
|3|Bloquear assinaturas inválidas e não confiáveis e pacotes não assinados<br /><br /> Essa configuração também bloqueia assinaturas geradas automaticamente.|  
  
> [!NOTE]  
>  A configuração recomendada para **BlockedSignatureStates** é 3. Essa configuração fornece maior proteção contra pacotes não assinados ou assinaturas que não são válidas nem confiáveis. Porém, a configuração recomendada talvez não seja apropriada em todas as circunstâncias. Para obter mais informações sobre como assinar ativos digitais, consulte o tópico "[Introdução à assinatura de código](https://go.microsoft.com/fwlink/?LinkId=51414)", na biblioteca do MSDN.  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>Para implementar uma política de assinatura para pacotes  
  
1.  No menu **Iniciar** , clique em **Executar**.  
  
2.  Na caixa de diálogo Executar, digite **Regedit**e clique em **OK**.  
  
3.  Localize a chave do Registro, HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS.  
  
4.  Clique com o botão direito do mouse em **MSDTS**, aponte para **Novo**e clique em **Valor DWORD**.  
  
5.  Atualize o nome do valor novo para **BlockedSignatureStates**.  
  
6.  Clique com o botão direito do mouse em **BlockedSignatureStates** e clique em **Modificar**.  
  
7.  Na caixa de diálogo **Editar valor DWORD** , digite o valor 0, 1, 2 ou 3.  
  
8.  Clique em **OK**.  
  
9. No menu **Arquivo** , clique em **Sair**.    

## <a name="sign-a-package-by-using-a-digital-certificate"></a><a name="cert"></a> Assinar um pacote por meio de um certificado digital
  Este tópico descreve como assinar um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com um certificado digital. Você pode usar uma assinatura digital, junto com outras configurações, para evitar o carregamento e a execução de um pacote inválido.  
  
 Antes de poder assinar um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , você deve realizar as seguintes tarefas:  
  
-   Criar ou obter uma chave privada a ser associada ao certificado e armazenar esta chave no computador local.  
  
-   Obter um certificado com a finalidade de assinatura de código de uma autoridade de certificação confiável. Você pode usar um dos métodos a seguir para obter ou criar um certificado:  
  
    -   Obtenha um certificado de uma autoridade de certificação comercial pública que emite certificados.  
  
    -   Obtenha um certificado de um servidor de certificados, que permita que uma organização emita certificados internamente. É necessário adicionar o certificado raiz usado para assinar o certificado ao armazenamento **Autoridades de Certificação Raiz Confiáveis** . Para adicionar o certificado raiz, você pode usar o snap-in de Certificados para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC). Para obter mais informações, consulte o tópico “[Serviços de certificado](https://go.microsoft.com/fwlink/?LinkId=100755)” na biblioteca do MSDN.  
  
    -   Crie seu próprio certificado somente para teste. A Ferramenta de Criação de Certificado (Makecert.exe) gera certificados X.509 para teste. Para obter mais informações, consulte o tópico “[Ferramenta de Criação de Certificado (Makecert.exe)](https://go.microsoft.com/fwlink/?LinkId=100756)” na Biblioteca MSDN.  
  
     Para obter mais informações sobre certificados, consulte a Ajuda online do snap-in de Certificados. Para obter mais informações sobre como assinar ativos digitais, consulte o tópico “[Assinando e verificando o código com o Authenticode](https://go.microsoft.com/fwlink/?LinkId=78100)” na biblioteca do MSDN.  
  
-   Verifique se o certificado foi habilitado para assinatura de código. Para saber se um certificado está habilitado para assinatura de código, revise as propriedades do certificado no snap-in de Certificados.  
  
-   Armazene o certificado no armazenamento Pessoal.  
  
 Depois de concluir as tarefas anteriores, realize o procedimento a seguir para assinar um pacote.  
  
### <a name="to-sign-a-package"></a>Para assinar um pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote a ser assinado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, no menu **SSIS** , clique em **Assinatura Digital**.  
  
4.  Na caixa de diálogo **Assinatura Digital** , clique em **Assinar**.  
  
5.  Na caixa de diálogo **Selecionar um Certificado** , selecione um certificado.  
  
6.  (Opcional) Clique em **Exibir Certificado**para exibir informações do certificado.  
  
7.  Clique em **OK** para fechar a caixa de diálogo **Selecionar um Certificado** .  
  
8.  Clique em **OK** para fechar a caixa de diálogo **Assinatura Digital** .  
  
9. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
     Embora o pacote tenha sido assinado, é necessário configurar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para verificar a assinatura digital antes de carregar o pacote.  

## <a name="digital-signing-dialog-box-ui-reference"></a><a name="signing_dialog"></a> Referência da interface do usuário da caixa de diálogo Assinatura Digital
  Use a caixa de diálogo **Assinatura Digital** para assinar um pacote com uma assinatura digital ou remover a assinatura. A caixa de diálogo **Assinatura Digital** está disponível na opção **Assinatura Digital** do menu **SSIS** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Para saber mais, veja [Assinar um pacote por meio de um certificado digital](#cert).  
  
### <a name="options"></a>Opções  
 **Assinar**  
 Clique para abrir a caixa de diálogo **Selecionar Certificado** e selecione o certificado a ser usado.  
  
 **Remover**  
 Clique para remover a assinatura digital.  

## <a name="see-also"></a>Confira também  
 [Pacotes do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md)   
 [Visão geral de segurança &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
  
  
