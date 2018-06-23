---
title: Definir ou alterar o nível de proteção de pacotes | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services],security
- security [Integration Services],protection levels
- protection level for packages [Integration Services]
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 695667f3ba50b6cde3d2b9629e7116fecf7c4b16
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119555"
---
# <a name="set-or-change-the-protection-level-of-packages"></a>Definir ou alterar o nível de proteção de pacotes
  Para controlar o acesso ao conteúdo de pacotes e aos valores confidenciais que eles contêm, como senhas, defina o valor da propriedade `ProtectionLevel`. Os pacotes contidos em um projeto precisam ter o mesmo nível de proteção que o projeto, para criar o projeto. Se você alterou os parâmetros da propriedade `ProtectionLevel` no projeto, precisa atualizar manualmente os parâmetros de propriedade para os pacotes.  
  
 Para obter informações sobre como determinar a `ProtectionLevel` configurações que são apropriadas para seus pacotes em diferentes estágios no ciclo de vida do pacote, consulte [controle de acesso de dados confidenciais em pacotes](security/access-control-for-sensitive-data-in-packages.md). Para obter uma visão geral dos recursos de segurança no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], consulte [Visão geral de segurança &#40;Integration Services&#41;](security/security-overview-integration-services.md).  
  
 Os procedimentos neste tópico descrevem como usar o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ou o utilitário de prompt de comando dtutil para alterar o `ProtectionLevel` propriedade.  
  
> [!NOTE]  
>  Além dos procedimentos neste tópico, tipicamente você pode definir ou alterar o `ProtectionLevel` propriedade de um pacote ao importar ou exportar o pacote. Você também pode alterar a propriedade de `ProtectionLevel` de um pacote ao usar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para salvar um pacote.  
  
### <a name="to-set-or-change-the-protection-level-of-a-package-in-sql-server-data-tools"></a>Para definir ou alterar o nível de proteção de um pacote nas Ferramentas de Dados do SQL Server  
  
1.  Examine os valores disponíveis para o `ProtectionLevel` propriedade no tópico [definindo o nível de proteção de pacotes](security/access-control-for-sensitive-data-in-packages.md)e determinar o valor apropriado para seu pacote.  
  
2.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote.  
  
3.  Abra o pacote no designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
4.  Se a janela Propriedades não mostrar as propriedades do pacote, clique na superfície de design.  
  
5.  Na janela Propriedades, no **segurança** de grupo, selecione o valor apropriado para o `ProtectionLevel` propriedade.  
  
     Se você selecionar um nível de proteção que exija uma senha, insira a senha como o valor da propriedade **PackagePassword** .  
  
6.  No menu **Arquivo** , selecione **Salvar Itens Selecionados** para salvar o pacote modificado.  
  
### <a name="to-set-or-change-the-protection-level-of-packages-at-the-command-prompt"></a>Para definir ou alterar o nível de proteção de pacotes no prompt de comando  
  
1.  Examine os valores disponíveis para o `ProtectionLevel` propriedade no tópico [definindo o nível de proteção de pacotes](security/access-control-for-sensitive-data-in-packages.md)e determinar o valor apropriado para seu pacote.  
  
2.  Examine os mapeamentos para o `Encrypt` opção no tópico [utilitário dtutil](dtutil-utility.md)e determine o inteiro apropriado a ser usado como o valor selecionado `ProtectionLevel` propriedade.  
  
3.  Abra uma janela do prompt de comando.  
  
4.  No prompt de comando, navegue até a pasta que contém o pacote ou pacotes para o qual você deseja definir o `ProtectionLevel` propriedade.  
  
     Os exemplos de sintaxe mostrados na etapa a seguir assumem que essa é a pasta atual.  
  
5.  Defina ou altere o nível de proteção do pacote ou pacotes usando um comando semelhante ao dos seguintes exemplos:  
  
    -   O comando a seguir define o `ProtectionLevel` propriedade de um pacote individual no sistema de arquivos como nível 2, "Criptografar dados confidenciais com senha", com a senha, "senha forte":  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   O comando a seguir define a propriedade `ProtectionLevel` de todos os pacotes em uma pasta específica no sistema de arquivos como nível 2, "Criptografar dados confidenciais com senha", com a senha, "senha forte":  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         Se você usar um comando semelhante em um arquivo em lotes, digite o espaço reservado do arquivo, "%f", como "%%f" no arquivo em lotes.  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário dtutil](dtutil-utility.md)  
  
  