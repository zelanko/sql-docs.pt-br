---
title: Definir ou alterar o nível de proteção de pacotes | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services],security
- security [Integration Services],protection levels
- protection level for packages [Integration Services]
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e700eed316e9dce3e5d87f6014913505376f535f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62889263"
---
# <a name="set-or-change-the-protection-level-of-packages"></a>Definir ou alterar o nível de proteção de pacotes
  Para controlar o acesso ao conteúdo de pacotes e aos valores confidenciais que eles contêm, como senhas, defina o valor da propriedade `ProtectionLevel`. Os pacotes contidos em um projeto precisam ter o mesmo nível de proteção que o projeto, para criar o projeto. Se você alterou os parâmetros da propriedade `ProtectionLevel` no projeto, precisa atualizar manualmente os parâmetros de propriedade para os pacotes.  
  
 Para obter informações sobre como determinar a `ProtectionLevel` as configurações que são apropriadas para pacotes em diferentes fases no ciclo de vida do pacote, consulte [controle de acesso para dados confidenciais em pacotes](security/access-control-for-sensitive-data-in-packages.md). Para obter uma visão geral dos recursos de segurança no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], consulte [Visão geral de segurança &#40;Integration Services&#41;](security/security-overview-integration-services.md).  
  
 Os procedimentos deste tópico descrevem como usar o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ou o utilitário de prompt de comando dtutil para alterar a propriedade `ProtectionLevel`.  
  
> [!NOTE]  
>  Além dos procedimentos deste tópico, tipicamente você pode definir ou alterar a propriedade `ProtectionLevel` de um pacote ao importar ou exportar o pacote. Você também pode alterar a propriedade de `ProtectionLevel` de um pacote ao usar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para salvar um pacote.  
  
### <a name="to-set-or-change-the-protection-level-of-a-package-in-sql-server-data-tools"></a>Para definir ou alterar o nível de proteção de um pacote nas Ferramentas de Dados do SQL Server  
  
1.  Examine os valores disponíveis para o `ProtectionLevel` propriedade no tópico [definindo o nível de proteção de pacotes](security/access-control-for-sensitive-data-in-packages.md)e determine o valor apropriado para seu pacote.  
  
2.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote.  
  
3.  Abra o pacote no designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
4.  Se a janela Propriedades não mostrar as propriedades do pacote, clique na superfície de design.  
  
5.  Na janela Propriedades, nos **segurança** grupo, selecione o valor apropriado para o `ProtectionLevel` propriedade.  
  
     Se você selecionar um nível de proteção que exija uma senha, insira a senha como o valor da propriedade **PackagePassword** .  
  
6.  No menu **Arquivo** , selecione **Salvar Itens Selecionados** para salvar o pacote modificado.  
  
### <a name="to-set-or-change-the-protection-level-of-packages-at-the-command-prompt"></a>Para definir ou alterar o nível de proteção de pacotes no prompt de comando  
  
1.  Examine os valores disponíveis para o `ProtectionLevel` propriedade no tópico [definindo o nível de proteção de pacotes](security/access-control-for-sensitive-data-in-packages.md)e determine o valor apropriado para seu pacote.  
  
2.  Examine os mapeamentos para o `Encrypt` opção no tópico [dtutil Utility](dtutil-utility.md)e determine o inteiro apropriado a ser usado como o valor de selecionado `ProtectionLevel` propriedade.  
  
3.  Abra uma janela do prompt de comando.  
  
4.  No prompt de comando, navegue para a pasta que contém o pacote ou pacotes para os quais você deseja definir a propriedade `ProtectionLevel`.  
  
     Os exemplos de sintaxe mostrados na etapa a seguir assumem que essa é a pasta atual.  
  
5.  Defina ou altere o nível de proteção do pacote ou pacotes usando um comando semelhante ao dos seguintes exemplos:  
  
    -   O comando a seguir define a propriedade `ProtectionLevel` de um pacote individual no sistema de arquivos como nível 2, "Criptografar dados confidenciais com senha", com a senha, "senha forte":  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   O comando a seguir define a propriedade `ProtectionLevel` de todos os pacotes em uma pasta específica no sistema de arquivos como nível 2, "Criptografar dados confidenciais com senha", com a senha, "senha forte":  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         Se você usar um comando semelhante em um arquivo em lotes, digite o espaço reservado do arquivo, "%f", como "%%f" no arquivo em lotes.  
  
## <a name="see-also"></a>Consulte também  
 [dtutil Utility](dtutil-utility.md)  
  
  
