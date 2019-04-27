---
title: Opção de configuração de servidor c2 audit mode | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], C2 Audit Mode option
- C2 auditing
- C2 Audit Mode option
- recording attempts
ms.assetid: 5a8d73a6-c4f6-4967-ba11-ecbcfc90b9cc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0233f6c40e15fd4f612002854477d98068901b15
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786665"
---
# <a name="c2-audit-mode-server-configuration-option"></a>Opção c2 audit mode de configuração de servidor
  O modo de auditoria C2 pode ser configurado pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou com a opção **modo de auditoria c2** no **sp_configure**. Selecionar esta opção configurará o servidor para registrar tentativas com falha e com êxito ao acessar instruções e objetos. Essas informações podem ajudá-lo a determinar o perfil da atividade do sistema e rastrear possíveis violações na política de segurança.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] O padrão de segurança C2 foi substituído pela Certificação de Critérios Comuns. Consulte [Opção de configuração de servidor com conformidade de critérios comuns habilitada](common-criteria-compliance-enabled-server-configuration-option.md).  
  
## <a name="audit-log-file"></a>Arquivo de auditoria de log  
 Os dados do modo de auditoria C2 são salvados no diretório de dados padrão da instância. Se o arquivo de log de auditoria atingir seu limite de tamanho de 200 MB, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criará um novo arquivo, fechará o arquivo antigo e gravará todos os novos registros de auditoria no novo arquivo. Esse processo continuará até que o diretório de dados de auditoria atinja seu limite ou a auditoria seja desativada. Para determinar o estado de um rastreamento de C2, consulte a exibição do catálogo sys.traces.  
  
> [!IMPORTANT]  
>  O modo de auditoria C2 salva uma grande quantidade de informações de eventos no arquivo de log, que pode aumentar rapidamente. Se o diretório de dados no qual os logs estão sendo salvos atingir seu limite de espaço, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será encerrado. Se a auditoria for definida para iniciar automaticamente, você deverá reiniciar a instância com o sinalizador **-f** (que passa pela auditoria) ou liberar espaço em disco adicional para o log de auditoria.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ativa o modo de auditoria C2.  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
sp_configure 'c2 audit mode', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
