---
title: "Alterar as configurações do grupo de carga de trabalho | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- workload groups [SQL Server], alter
- Resource Governor, workload group alter
ms.assetid: 73b6109c-2ad0-4915-b11b-d40d5a0fdc25
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0b8cc44c1b1333143a36377b20e2467b1831cde3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="change-workload-group-settings"></a>Alterar as configurações de grupo de carga de trabalho
  Você pode alterar as configurações do grupo de cargas de trabalho usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   **Antes de começar:**  [Limitações e restrições](#LimitationsRestrictions), [Permissões](#Permissions)  
  
-   **Para alterar as configurações para um grupo de cargas de trabalho, usando:**  [SQL Server Management Studio](#ChgWGProp), [Transact-SQL](#ChgWGTSQL)  
  
## <a name="before-you-begin"></a>Antes de começar  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
 Você pode alterar as configurações do grupo de cargas de trabalho padrão e de grupos de cargas de trabalho definidos pelo usuário.  
  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 A memória consumida pela criação de índice na tabela particionada desalinhada é proporcional ao número de partições envolvidas. Se a memória total necessária exceder o limite por consulta (REQUEST_MAX_MEMORY_GRANT_PERCENT) imposto pela configuração de grupo de cargas de trabalho, poderá ocorrer uma falha na criação do índice. Como o grupo de cargas de trabalho padrão permite que uma consulta exceda o limite por consulta com o mínimo de memória requerida para iniciar, para compatibilidade com o SQL Server 2005, o usuário talvez possa executar a mesma criação de índice no grupo de cargas de trabalho padrão caso o pool de recursos padrão tenha memória total suficiente configurada para executar tal consulta.  
  
 A criação de índice pode usar mais espaço de trabalho de memória do que aquela inicialmente concedida a fim de melhorar o desempenho. Esse tratamento especial tem suporte do Administrador de Recursos. No entanto, a concessão inicial e qualquer concessão de memória adicional estão limitadas pelas configurações de pool de recursos e de grupo de cargas de trabalho.  
  
###  <a name="Permissions"></a> Permissões  
 Alterar as configurações de um grupo de cargas de trabalho exige permissão CONTROL SERVER.  
  
##  <a name="ChgWGProp"></a> Alterar as configurações do grupo de cargas de trabalho usando o SQL Server Management Studio  
 **Para alterar as configurações do grupo de cargas de trabalho usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  No Pesquisador de Objetos, expanda recursivamente o nó **Gerenciamento** para baixo e incluindo a pasta **Grupos de Cargas de Trabalho** que contém o grupo de carga de trabalho a ser modificado.  
  
2.  Clique com o botão direito do mouse no grupo de cargas de trabalho a ser modificado e clique em **Propriedades**.  
  
3.  Na página **Propriedades do Administrador de Recursos** selecione a linha para o grupo de cargas de trabalho na grade **Grupos de cargas de trabalho para o pool de recursos** caso não seja selecionada automaticamente.  
  
4.  Clique ou clique duas vezes nas células na linha a ser alterada e insira os novos valores.  
  
5.  Para salvar as alterações, clique em **OK**  
  
##  <a name="ChgWGTSQL"></a> Alterar configurações do grupo de cargas de trabalho usando Transact-SQL  
 **Para alterar as configurações do grupo de cargas de trabalho usando Transact-SQL**  
  
1.  Execute a instrução ALTER WORKLOAD GROUP que especifica os valores de propriedade a serem alterados.  
  
2.  Execute a instrução ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
### <a name="example-transact-sql"></a>Exemplo (Transact-SQL)  
 O exemplo a seguir altera a configuração percentual de concessão de memória máxima para o grupo de cargas de trabalho chamado `groupAdhoc`.  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
WITH (REQUEST_MAX_MEMORY_GRANT_PERCENT = 30);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Criar um grupo de carga de trabalho](../../relational-databases/resource-governor/create-a-workload-group.md)   
 [Criar um pool de recursos](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Alterar configurações do pool de recursos](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
