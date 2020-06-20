---
title: Chave de criptografia de backup (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.backupencryptionkey.F1
ms.assetid: eb8c82be-323b-4d86-ab10-c1bf69a4abe3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c8524cdc2c4efb03e2a285c815ca58391045062f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045505"
---
# <a name="backup-encryption-key-ssrs-native-mode"></a>Chave de Criptografia de Backup (modo nativo do SSRS)
  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa uma chave de criptografia para proteger dados confidenciais armazenados no banco de dados do servidor de relatório. Ter um backup dessa chave é essencial para assegurar acesso contínuo a cadeias de conexões criptografadas e credenciais. Você deve ter uma cópia de backup dessa chave caso mova o banco de dados do servidor de relatório para outro computador ou altere o nome de usuário ou a senha da conta de serviço do Servidor de Relatório. Ambas as operações requerem que você restaure a chave de uma cópia de backup previamente criada.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo.  
  
 Para abrir a caixa de diálogo Chave de Criptografia de Backup, clique em **Chaves de Criptografia** no painel de navegação do Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique em **Backup**. Essa caixa de diálogo também é exibida quando você atualiza a conta de serviço usando a página Conta de Serviço no Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações sobre o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, consulte [Gerenciador de configurações do Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opções  
 **Local do arquivo**  
 Especifique um nome de arquivo e um local para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para a chave simétrica. A chave simétrica nunca é armazenada em texto sem-formatação. Você deve digitar uma senha para proteger o arquivo.  
  
 **Senha**  
 Digite uma senha que proteja o arquivo contra acessos não autorizados. Somente os usuários que conhecem a senha poderão restaurar a chave bloqueada no arquivo protegido. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] impõe uma política de senha forte. A senha deve conter no mínimo 8 caracteres, incluir uma combinação de caracteres alfanuméricos maiúsculos e minúsculos e, pelo menos, um símbolo.  
  
 **Confirmar Senha**  
 Digite novamente a senha.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de Configurações do Reporting Services F1 tópicos de ajuda &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Fazer backup e restaurar Reporting Services chaves de criptografia](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Excluir e recriar chaves de criptografia &#40;Configuration Manager SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Inicializar um servidor de relatório &#40; Configuration Manager do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Armazenar dados criptografados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Chaves de criptografia &#40;o modo nativo do SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
