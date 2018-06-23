---
title: Restaurar a chave de criptografia (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.rsconfigtool.restoreencryptionkey.F1
ms.assetid: 11ce51e5-f5d4-40b6-88d8-9360fb50e66c
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 2fd845eb3bbc64f43b499e6761b4acc5aa84ae0f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115578"
---
# <a name="restore-encryption-key-ssrs-native-mode"></a>Restaurar chave de criptografia (modo nativo do SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa uma chave de criptografia para proteger dados confidenciais armazenados no banco de dados de servidor de relatório. Para assegurar-se de que tenha acesso contínuo aos dados criptografados, é importante criar um backup da chave da criptografia, caso seja necessário restaurá-la posteriormente devido a alterações na conta de serviço ou como parte de uma migração planejada. Este tópico é uma visão geral de como usar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager para restaurar as chaves.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para restaurar a chave, você deve ter salvo anteriormente uma cópia de backup da chave para um arquivo protegido por senha. Durante a restauração da chave, o servidor de relatório substituirá uma chave existente pela chave localizada no arquivo protegido por senha. A chave que está dentro do arquivo deve ser idêntica à chave usada para criptografar e descriptografar os dados.  
  
 Para verificar se você restaurou uma chave válida, use o Gerenciador de Relatórios para exibir assinaturas ou qualquer relatório que tenha uma fonte de dados que use credenciais armazenadas. Se você receber o erro "O servidor de relatório não pode acessar dados criptografados" ao tentar abrir uma página de definição de assinatura ou se for solicitado a inserir credenciais ao abrir um relatório que anteriormente usava credenciais armazenadas para a fonte de dados do relatório, você restaurou uma chave inválida.  
  
 Se você restaurar uma chave inválida que seja diferente da usada para criptografar os dados, será impossível descriptografar os dados atualmente armazenados no banco de dados do servidor de relatório. Se você restaurar uma chave inválida, deverá imediatamente restaurar uma cópia de backup da chave correta, se estiver disponível. Se você não tiver uma cópia de backup da chave que foi usada para criptografar os dados, deverá excluir todos os dados criptografados. Clique o **excluir** botão o [chaves de criptografia](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md) página para executar essa etapa. Depois de excluir o conteúdo criptografado, você deverá atualizar manualmente todas as assinaturas e especificar novamente todas as credenciais armazenadas definidas para relatórios e assinaturas controladas por dados no servidor de relatório.  
  
## <a name="restore-encryption-key-dialog"></a>Caixa de diálogo Restaurar Chave de Criptografia  
 Para obter informações sobre onde encontrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, consulte [Reporting Services Configuration Manager &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 Para abrir a caixa de diálogo Restaurar chave de criptografia, clique em **chaves de criptografia** no painel de navegação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do Configuration Manager e depois clique em **restauração**. Essa caixa de diálogo também é exibida quando você atualizar a conta de serviço usando a página conta de serviço a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do Configuration Manager. Para obter mais informações sobre  
  
## <a name="options"></a>Opções  
 **Local do arquivo**  
 Selecione o arquivo protegido por senha que contém uma cópia da chave simétrica. A extensão padrão do arquivo é .snk.  
  
 **Senha**  
 Digite a senha que desbloqueia o arquivo. Somente os usuários que conhecem a senha podem restaurar a chave. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] impõe uma política de senha forte. A senha deve conter pelo menos 8 caracteres e incluir uma combinação de caracteres alfanuméricos maiúsculos e minúsculos e pelo menos um caractere de símbolo.  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos de Ajuda F1 do Configuration Manager do Reporting Services &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Fazer backup e restaurar as chave de criptografia do Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Excluir e recriar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Inicializar um servidor de relatório &#40; Configuration Manager do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Armazenar dados criptografados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Chaves de criptografia &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  