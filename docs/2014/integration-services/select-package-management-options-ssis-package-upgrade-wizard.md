---
title: Selecione as opções de gerenciamento de pacote (Assistente de atualização da pacotes SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.is.upgradewizard.selectpackagemgtoptions.f1
ms.assetid: 810fc020-51cd-43ed-9f35-af99b4f35947
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a1a05db41d0e82b931f51a7f3c0e80f8d33de79c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120849"
---
# <a name="select-package-management-options-ssis-package-upgrade-wizard"></a>Selecionar Opções de Gerenciamento de Pacotes (Assistente de Atualização de Pacotes SSIS)
  Use a página **Selecionar Opções de Gerenciamento de Pacote** para especificar opções para atualizar pacotes.  
  
 **Para executar o Assistente de Atualização de Pacotes SSIS**  
  
-   [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="options"></a>Opções  
 **Atualizar cadeias de conexão para usar novos nomes de provedor**  
 Atualize as cadeias de conexão para usar os nomes dos seguintes provedores da versão atual do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   Provedor OLE DB para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 O Assistente de Atualização de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] só atualiza cadeias de conexão armazenadas em gerenciadores de conexões. O assistente não atualiza cadeias de conexão construídas dinamicamente com a linguagem de expressão do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ou o código de uma tarefa Script.  
  
 **Validar pacotes de atualização**  
 Valide os pacotes de atualização e salve só os pacotes aprovados na validação.  
  
 Se você não selecionar essa opção, o assistente não validará pacotes de atualização. Portanto, o assistente salvará todos os pacotes de atualização, independentemente de sua validez. O assistente salva os pacotes de atualização no destino especificado na página **Selecionar Local de Destino** do assistente.  
  
 A validação prolonga o processo de atualização. Recomendamos que você não selecione essa opção para pacotes grandes que provavelmente serão atualizados com êxito.  
  
 **Criar novas IDs de pacote**  
 Crie novas IDs para os pacotes de atualização.  
  
 **Continuar o processo de upgrade quando um upgrade de pacote falhar**  
 Especifique que o Assistente de Atualização de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] deve continuar atualizando os pacotes restantes quando não for possível atualizar um pacote.  
  
 **Conflitos de nome de pacote**  
 Especifique como o assistente deve manipular pacotes que têm o mesmo nome. Os valores dessa opção estão relacionados na tabela a seguir.  
  
 **Substituir arquivos de pacote existentes**  
 Substitui o pacote existente pelo pacote de atualização do mesmo nome.  
  
 **Adicionar sufixos numéricos para fazer upgrade de nomes de pacote**  
 Adiciona um sufixo numérico ao nome do pacote de atualização.  
  
 **Não fazer upgrade de pacotes**  
 Interrompe a atualização dos pacotes e exibe um erro quando o assistente é concluído.  
  
 Essas opções não estão disponíveis quando a opção **Salvar no local de origem** é selecionada na página **Selecionar Local de Destino** do assistente.  
  
 **Ignorar configurações**  
 Não carrega configurações de pacotes durante a atualização de pacotes. A seleção dessa opção reduz o tempo necessário para atualizar o pacote.  
  
 **Fazer backup dos pacotes originais**  
 Configure o assistente para fazer backup dos pacotes originais em uma pasta **SSISBackupFolder** . O assistente cria a pasta **SSISBackupFolder** como uma subpasta da pasta que contém os pacotes originais e os pacotes atualizados.  
  
> [!NOTE]  
>  Essa opção só está disponível quando você especifica que os pacotes originais e os pacotes atualizados estão armazenados no sistema de arquivos e na mesma pasta.  
  
 Para obter mais informações, consulte [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar pacotes do Integration Services](install-windows/upgrade-integration-services-packages.md)  
  
  