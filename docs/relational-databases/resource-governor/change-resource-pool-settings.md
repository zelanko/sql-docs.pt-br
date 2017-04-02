---
title: "Alterar configura&#231;&#245;es do pool de recursos | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Administrador de recursos, alteração do pool de recursos"
  - "pools de recursos [SQL Server], alterar"
ms.assetid: 49438285-a011-4dac-bd4f-f35cd90fda61
caps.latest.revision: 15
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 15
---
# Alterar configura&#231;&#245;es do pool de recursos
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  É possível alterar as configurações de um pool de recursos usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Antes de começar:**  [Limitações e restrições](#LimitationsRestrictions), [Permissões](#Permissions)  
  
-   **Para alterar as configurações para um pool de recursos, usando:** [SQL Server Management Studio](#ChgRPProp), [Transact-SQL](#ChgRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
 O percentual máximo de CPU deve ser igual a ou maior que o percentual mínimo de CPU. O percentual máximo de memória deve ser igual a ou maior que o percentual mínimo de memória.  
  
 A soma dos percentuais mínimos de CPU e dos percentuais mínimos de memória de todos os pools de recursos não deve exceder 100.  
  
###  <a name="Permissions"></a> Permissões  
 Alterar as configurações do pool de recursos exige permissão CONTROL SERVER.  
  
##  <a name="ChgRPProp"></a> Alterar as configurações do pool de recursos usando o SQL Server Management Studio  
 **Para alterar as configurações de um pool de recursos usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o Pesquisador de Objetos e expanda recursivamente o nó **Gerenciamento** para baixo e inclua **Pools de Recursos**.  
  
2.  Clique com o botão direito do mouse no pool de recursos a ser modificado e clique em **Propriedades**.  
  
3.  Na página **Propriedades do Administrador de Recursos** selecione a linha para o pool de recursos na grade **Pools de Recursos** caso ela não seja selecionada automaticamente.  
  
4.  Clique ou clique duas vezes nas células na linha a ser alterada e insira os novos valores.  
  
5.  Para salvar as alterações, clique em **OK**  
  
##  <a name="ChgRPTSQL"></a> Alterar o pool de recursos usando Transact-SQL  
 **Para alterar as configurações de um pool de recursos usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Execute a instrução **ALTER RESOURCE POOL** ou **ALTER EXTERNAL RESOURCE POOL** que especifica os valores de propriedade a serem alterados.  
  
2.  Execute a instrução **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### Exemplo (Transact-SQL)  
 O exemplo a seguir altera a configuração do percentual máximo de CPU para o pool de recursos chamada `poolAdhoc`.  
  
```  
ALTER RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## Consulte também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar Administrador de Recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Criar um pool de recursos](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Excluir um pool de recursos](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Função de classificação do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  