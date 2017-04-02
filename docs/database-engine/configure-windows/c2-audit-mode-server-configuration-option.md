---
title: "Op&#231;&#227;o c2 audit mode de configura&#231;&#227;o de servidor | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "auditando [SQL Server]"
  - "auditorias [SQL Server], opção de Modo de Auditoria C2"
  - "auditoria de C2"
  - "opção C2 Audit Mode"
  - "tentativas de registro"
ms.assetid: 5a8d73a6-c4f6-4967-ba11-ecbcfc90b9cc
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Op&#231;&#227;o c2 audit mode de configura&#231;&#227;o de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O modo de auditoria C2 pode ser configurado pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou com a opção **modo de auditoria c2** no **sp_configure**. Selecionar esta opção configurará o servidor para registrar tentativas com falha e com êxito ao acessar instruções e objetos. Essas informações podem ajudá-lo a determinar o perfil da atividade do sistema e rastrear possíveis violações na política de segurança.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] O padrão de segurança de C2 foi substituído pela Certificação de Critério Comum. Consulte [Opção de configuração de servidor com conformidade de critérios comuns habilitada](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md).  
  
## Arquivo de auditoria de log  
 Os dados do modo de auditoria C2 são salvados no diretório de dados padrão da instância. Se o arquivo de log de auditoria atingir seu limite de tamanho de 200 MB, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criará um novo arquivo, fechará o arquivo antigo e gravará todos os novos registros de auditoria no novo arquivo. Esse processo continuará até que o diretório de dados de auditoria atinja seu limite ou a auditoria seja desativada. Para determinar o estado de um rastreamento de C2, consulte a exibição do catálogo sys.traces.  
  
> [!IMPORTANT]  
>  O modo de auditoria C2 salva uma grande quantidade de informações de eventos no arquivo de log, que pode aumentar rapidamente. Se o diretório de dados no qual os logs estão sendo salvos atingir seu limite de espaço, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será encerrado. Se a auditoria for definida para iniciar automaticamente, você deverá reiniciar a instância com o sinalizador **-f** (que passa pela auditoria) ou liberar espaço em disco adicional para o log de auditoria.  
  
## Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## Exemplo  
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
  
## Consulte também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  