---
title: Restaurar chave de criptografia (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.restoreencryptionkey.F1
ms.assetid: 11ce51e5-f5d4-40b6-88d8-9360fb50e66c
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 111e44275922149949cd7e252e112d95cef65076
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952031"
---
# <a name="restore-encryption-key-ssrs-native-mode"></a>Restaurar chave de criptografia (modo nativo do SSRS)
  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa uma chave de criptografia para proteger dados confidenciais armazenados no banco de dados do servidor de relatório. Para assegurar-se de que tenha acesso contínuo aos dados criptografados, é importante criar um backup da chave da criptografia, caso seja necessário restaurá-la posteriormente devido a alterações na conta de serviço ou como parte de uma migração planejada. Este tópico é uma visão geral de como usar o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para restaurar chaves.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo.  
  
 Para restaurar a chave, você deve ter salvo anteriormente uma cópia de backup da chave para um arquivo protegido por senha. Durante a restauração da chave, o servidor de relatório substituirá uma chave existente pela chave localizada no arquivo protegido por senha. A chave que está dentro do arquivo deve ser idêntica à chave usada para criptografar e descriptografar os dados.  
  
 Para verificar se você restaurou uma chave válida, use o Gerenciador de Relatórios para exibir assinaturas ou qualquer relatório que tenha uma fonte de dados que use credenciais armazenadas. Se você receber o erro "O servidor de relatório não pode acessar dados criptografados" ao tentar abrir uma página de definição de assinatura ou se for solicitado a inserir credenciais ao abrir um relatório que anteriormente usava credenciais armazenadas para a fonte de dados do relatório, você restaurou uma chave inválida.  
  
 Se você restaurar uma chave inválida que seja diferente da usada para criptografar os dados, será impossível descriptografar os dados atualmente armazenados no banco de dados do servidor de relatório. Se você restaurar uma chave inválida, deverá imediatamente restaurar uma cópia de backup da chave correta, se estiver disponível. Se você não tiver uma cópia de backup da chave que foi usada para criptografar os dados, deverá excluir todos os dados criptografados. Clique no botão **Excluir** da página [Chaves de Criptografia](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md) para executar essa etapa. Depois de excluir o conteúdo criptografado, você deverá atualizar manualmente todas as assinaturas e especificar novamente todas as credenciais armazenadas definidas para relatórios e assinaturas controladas por dados no servidor de relatório.  
  
## <a name="restore-encryption-key-dialog"></a>Caixa de diálogo Restaurar Chave de Criptografia  
 Para obter informações sobre onde encontrar a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, consulte [Gerenciador de configurações do Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 Para abrir a caixa de diálogo Restaurar Chave de Criptografia, clique em **Chaves de Criptografia** no painel de navegação do Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique em **Restaurar**. Essa caixa de diálogo também é exibida quando você atualiza a conta de serviço usando a página Conta de Serviço no Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações sobre  
  
## <a name="options"></a>Opções  
 **Local do arquivo**  
 Selecione o arquivo protegido por senha que contém uma cópia da chave simétrica. A extensão padrão do arquivo é .snk.  
  
 **Senha**  
 Digite a senha que desbloqueia o arquivo. Somente os usuários que conhecem a senha podem restaurar a chave. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] impõe uma política de senha forte. A senha deve conter pelo menos 8 caracteres e incluir uma combinação de caracteres alfanuméricos maiúsculos e minúsculos e pelo menos um caractere de símbolo.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de Configurações do Reporting Services F1 tópicos de ajuda &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Fazer backup e restaurar as chave de criptografia do Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Excluir e recriar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Inicializar um servidor de relatório &#40;Configuration Manager SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Armazene dados criptografados do servidor de relatório &#40;Configuration Manager SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Chaves de criptografia &#40;o modo nativo do SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
