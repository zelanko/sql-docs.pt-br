---
title: "Op&#231;&#227;o de configura&#231;&#227;o de servidor com conformidade de crit&#233;rios comuns habilitada | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "common criteria compliance"
helpviewer_keywords: 
  - "CC (critérios comuns) [Mecanismo de Banco de Dados]"
  - "conformidade de critérios comuns [Mecanismo de Banco de Dados]"
  - "Residual Information Protection [Mecanismo de Banco de Dados]"
  - "RIP (Residual Information Protection)"
ms.assetid: 61766eea-c450-408d-af33-fbe7ef8c9ff2
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Op&#231;&#227;o de configura&#231;&#227;o de servidor com conformidade de crit&#233;rios comuns habilitada
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A opção conformidade de critérios comuns habilitada habilita os seguintes elementos necessários para os critérios comuns.  
  
|Critério|Descrição|  
|--------------|-----------------|  
|Proteção de Informação Residual (RIP)|O RIP requer alocação de memória para ser substituído por um padrão conhecido de bits antes que a memória seja realocada para um novo recurso. Atender ao padrão RIP pode contribuir para melhorar a segurança; entretanto, a substituição da alocação de memória pode diminuir o desempenho. Depois que a opção conformidade de critérios comuns habilitada estiver habilitada, ocorre a substituição.|  
|A habilidade para exibir estatísticas de logon|Depois que a opção conformidade de critérios comuns habilitada é ativada, a auditoria de logon é habilitada. Sempre que um usuário fizer um logon bem-sucedido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as informações sobre a hora do último logon com êxito e do último logon sem êxito e o número de tentativas entre o último logon bem-sucedido e o logon atual são disponibilizadas. Essas estatísticas de logon podem ser exibidas com uma consulta à exibição de gerenciamento dinâmico [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).|  
|A coluna GRANT não deve substituir a tabela DENY|Depois que a opção conformidade de critérios comuns habilitada é habilitada, um nível de tabela DENY precede um nível de coluna GRANT. Quando a opção não é habilitada, um nível de coluna GRANT precede um nível de tabela DENY.|  
  
 A opção habilitada para a conformidade de critérios comuns é uma opção avançada. Os critérios comuns somente são avaliados e certificados para as edições Enterprise e Datacenter. Para obter o status mais recente da certificação de critérios comuns, consulte o site da Web [Microsoft SQL Server Common Criteria (Critérios comuns do Microsoft SQL Server)](http://go.microsoft.com/fwlink/?LinkId=616319) .  
  
> [!IMPORTANT]  
>  Além de habilitar a opção common criteria compliance enabled, também é necessário baixar e executar um script que conclui a configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conformidade com o EAL4+ (nível de garantia de avaliação 4+) de Critérios Comuns. Você pode fazer download deste script no site [Microsoft SQL Server Common Criteria](http://go.microsoft.com/fwlink/?LinkId=616319) .  
  
 Se você estiver usando o procedimento armazenado do sistema sp_configure para alterar a definição, poderá alterar a opção conformidade de critérios comuns habilitada somente quando a opção mostrar opções avançadas estiver definida como 1. A configuração terá efeito depois que o servidor for reiniciado. Os valores possíveis são 0 e 1:  
  
-   0 indica que a conformidade dos critérios comuns não está habilitada. Esse é o padrão.  
  
-   1 indica que a conformidade dos critérios comuns está habilitada.  
  
## Exemplos  
 O exemplo a seguir habilita a conformidade dos critérios comuns.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'common criteria compliance enabled', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  