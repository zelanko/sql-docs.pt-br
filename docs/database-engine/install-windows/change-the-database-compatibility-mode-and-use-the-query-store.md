---
title: Alterar o modo de compatibilidade do banco de dados e usar o Repositório de Consultas | Microsoft Docs
ms.custom: ''
ms.date: 07/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0b7898f984d22ad6606bf84585aa6554c2290b29
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="change-the-database-compatibility-mode-and-use-the-query-store"></a>Alterar o modo de compatibilidade do banco de dados e usar o repositório de consultas

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], algumas alterações são habilitadas somente quando o [nível de compatibilidade do banco de dados](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) é alterado. Isso foi feito por vários motivos:  
  
- Uma vez que a atualização é uma operação unidirecional (não é possível fazer downgrade do formato de arquivo), há valor em separar a habilitação de novos recursos para uma operação separada dentro do banco de dados. É possível reverter uma configuração para um nível de compatibilidade do banco de dados anterior.  O novo modelo reduz o número de itens que devem ocorrer durante uma janela de interrupção.  
  
- Alterações no processador de consulta podem ter efeitos complexos. Até mesmo uma alteração “boa” para o sistema pode ser ótima para a maioria das cargas de trabalho – ela pode causar uma regressão inaceitável em uma consulta importante para outros. Separar essa lógica do processo de atualização permite que determinados recursos, assim como o Repositório de Consultas, façam rapidamente a mitigação das escolhas de plano ou até mesmo evitem-nas completamente em servidores de produção.  
  
> [!IMPORTANT]  
> Se o nível de compatibilidade de um banco de dados de usuário era 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização.    
> Se o nível de compatibilidade de um banco de dados do usuário era 90 antes da atualização, no banco de dados atualizado esse nível será definido como 100, que é o mais baixo com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].    
> Os níveis de compatibilidade dos bancos de dados tempdb, model, msdb e Resource são definidos para o nível de compatibilidade atual após o upgrade.   
> O banco de dados do sistema mestre retém o nível de compatibilidade anterior ao upgrade.    
  
O processo de atualização para habilitar a nova funcionalidade do processador de consulta está relacionado ao modelo de manutenção pós-lançamento do produto.  Algumas dessas correções são liberadas sob o [sinalizador de rastreamento 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199).  Clientes que precisam de correções podem optar por aceitar essas correções sem causar regressões inesperadas para outros clientes. O modelo de manutenção pós-lançamento para hotfixes do processador de consulta é documentado [aqui](http://support.microsoft.com/kb/974006). Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a mudança para um novo nível de compatibilidade implica no sinalizador de rastreamento 4199 não ser mais necessário, porque essas correções agora estão habilitadas por padrão no último modo de compatibilidade. Portanto, como parte do processo de atualização, é importante validar que o 4199 não está habilitado quando o processo de atualização for concluído.  

> [!NOTE]
> No entanto, o sinalizador de rastreamento 4199 ainda é necessário para habilitar qualquer nova correção de processador de consulta lançada após o RTM, se aplicável.
  
O fluxo de trabalho recomendado para atualizar o processador de consulta para a versão mais recente do código está documentado em [Manter a estabilidade do desempenho durante a atualização para a seção do SQL Server mais recente de Cenários de uso do repositório de consultas](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade), conforme mostrado abaixo.  
  
![query-store-usage-5](../../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5") 
 
## <a name="see-also"></a>Consulte Também  
 [Exibir ou alterar o nível de compatibilidade de um banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)  
 [Cenários de uso do Repositório de Consultas](../../relational-databases/performance/query-store-usage-scenarios.md) 
  
