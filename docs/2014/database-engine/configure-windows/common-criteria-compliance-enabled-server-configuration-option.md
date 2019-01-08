---
title: Opção de configuração de servidor common criteria compliance enabled | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- common criteria compliance
helpviewer_keywords:
- CC (common criteria) [Database Engine]
- common criteria compliance [Database Engine]
- Risidual Information Protection [Database Engine]
- RIP (Residual Information Protection)
ms.assetid: 61766eea-c450-408d-af33-fbe7ef8c9ff2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8fef699da6e63c534d19e0d66bfa076f85348d29
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368978"
---
# <a name="common-criteria-compliance-enabled-server-configuration-option"></a>Opção de configuração de servidor com conformidade de critérios comuns habilitada
  A opção conformidade de critérios comuns habilitada habilita os seguintes elementos necessários para os critérios comuns.  
  
|Critérios|Descrição|  
|--------------|-----------------|  
|Proteção de Informação Residual (RIP)|O RIP requer alocação de memória para ser substituído por um padrão conhecido de bits antes que a memória seja realocada para um novo recurso. Atender ao padrão RIP pode contribuir para melhorar a segurança; entretanto, a substituição da alocação de memória pode diminuir o desempenho. Depois que a opção conformidade de critérios comuns habilitada estiver habilitada, ocorre a substituição.|  
|A habilidade para exibir estatísticas de logon|Depois que a opção conformidade de critérios comuns habilitada é ativada, a auditoria de logon é habilitada. Sempre que um usuário fizer um logon bem-sucedido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as informações sobre a hora do último logon com êxito e do último logon sem êxito e o número de tentativas entre o último logon bem-sucedido e o logon atual são disponibilizadas. Essas estatísticas de logon podem ser exibidas com uma consulta à exibição de gerenciamento dinâmico [sys.dm_exec_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql) .|  
|A coluna GRANT não deve substituir a tabela DENY|Depois que a opção conformidade de critérios comuns habilitada é habilitada, um nível de tabela DENY precede um nível de coluna GRANT. Quando a opção não é habilitada, um nível de coluna GRANT precede um nível de tabela DENY.|  
  
 A opção habilitada para a conformidade de critérios comuns é uma opção avançada. Os critérios comuns somente são avaliados e certificados para as edições Enterprise e Datacenter. Para obter o status mais recente da certificação de critérios comuns, consulte o site da Web [Microsoft SQL Server Common Criteria (Critérios comuns do Microsoft SQL Server)](https://go.microsoft.com/fwlink/?LinkId=616319) .  
  
> [!IMPORTANT]  
>  Além de habilitar a opção common criteria compliance enabled, também é necessário baixar e executar um script que conclui a configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conformidade com o EAL4+ (nível de garantia de avaliação 4+) de Critérios Comuns. Você pode fazer download deste script no site [Microsoft SQL Server Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319) .  
  
 Se você estiver usando o procedimento armazenado do sistema sp_configure para alterar a definição, poderá alterar a opção conformidade de critérios comuns habilitada somente quando a opção mostrar opções avançadas estiver definida como 1. A configuração terá efeito depois que o servidor for reiniciado. Os valores possíveis são 0 e 1:  
  
-   0 indica que a conformidade dos critérios comuns não está habilitada. Esse é o padrão.  
  
-   1 indica que a conformidade dos critérios comuns está habilitada.  
  
## <a name="examples"></a>Exemplos  
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
  
## <a name="see-also"></a>Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
