---
title: Configuração de conformidade de critérios comuns habilitada | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2018
ms.prod: sql
ms.prod_service: high-availability
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
author: craigg-msft
ms.author: craigg
ms.openlocfilehash: f072ed3e73b7dacd10254c04aaa34e5466b582b8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68262221"
---
# <a name="common-criteria-compliance-enabled-server-configuration"></a>Configuração de servidor de conformidade de critérios comuns habilitada
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A opção de conformidade de critérios comuns habilita os seguintes elementos necessários para os [critérios comuns para avaliação de segurança da tecnologia da informação](https://www.commoncriteriaportal.org/).  
  
|Critérios|DESCRIÇÃO|  
|--------------|-----------------|  
|Proteção de Informação Residual (RIP)|O RIP requer alocação de memória para ser substituído por um padrão conhecido de bits antes que a memória seja realocada para um novo recurso. Atender ao padrão RIP pode contribuir para melhorar a segurança; entretanto, a substituição da alocação de memória pode diminuir o desempenho. Depois que a opção conformidade de critérios comuns habilitada estiver habilitada, ocorre a substituição.|  
|A habilidade para exibir estatísticas de logon|Depois que a opção conformidade de critérios comuns habilitada é ativada, a auditoria de logon é habilitada. Sempre que um usuário fizer um logon bem-sucedido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as informações sobre a hora do último logon com êxito e do último logon sem êxito e o número de tentativas entre o último logon bem-sucedido e o logon atual são disponibilizadas. Essas estatísticas de logon podem ser exibidas com uma consulta à exibição de gerenciamento dinâmico [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) .|  
|Essa coluna `GRANT` não deve substituir a tabela `DENY`|Depois que a opção common criteria compliance enabled for habilitada, um nível de tabela `DENY` terá precedência sobre um nível de coluna `GRANT`. Quando a opção não for habilitada, um nível de coluna `GRANT` terá precedência sobre um nível de tabela `DENY`.|  
  
 A opção habilitada para a conformidade de critérios comuns é uma opção avançada. Os critérios comuns somente são avaliados e certificados para as edições Enterprise e Datacenter. Para obter o status mais recente da certificação de critérios comuns, consulte o site da Web [Microsoft SQL Server Common Criteria (Critérios comuns do Microsoft SQL Server)](https://go.microsoft.com/fwlink/?LinkId=616319) .  
  
> [!IMPORTANT]  
>  Além de habilitar a opção common criteria compliance enabled, também é necessário baixar e executar um script que conclui a configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conformidade com o EAL4+ (nível de garantia de avaliação 4+) de Critérios Comuns. Você pode fazer download deste script no site [Microsoft SQL Server Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319) .  
  
 Se você estiver usando o procedimento armazenado do sistema `sp_configure` para alterar a configuração, poderá alterar a opção common criteria compliance enabled somente quando a opção show advanced options for definida como 1. A configuração terá efeito depois que o servidor for reiniciado. Os valores possíveis são 0 e 1:  
  
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
RECONFIGURE WITH OVERRIDE; 
GO  
```  

Reinicie o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
