---
title: Configurar a opção de configuração de servidor cost threshold for parallelism | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cost threshold for parallelism option
ms.assetid: dad21bee-fe28-41f6-9d2f-e6ababfaf9db
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f318a0d82a2fc131554f12d0d15f049d588a3928
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-the-cost-threshold-for-parallelism-server-configuration-option"></a>Configurar a opção cost threshold for parallelism de configuração de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **cost threshold for parallelism** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **cost threshold for parallelism** especifica o limite no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria e executa planos paralelos para consultas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria e executa um plano paralelo para uma consulta somente quando o custo estimado para executar um plano serial para a mesma consulta é mais alto que o valor definido em **cost threshold for parallelism**. O custo refere-se a um custo estimado, exigido para a execução do plano serial em uma configuração de hardware específica, e não é uma unidade de tempo. A opção **cost threshold for parallelism** pode ser definida como qualquer valor de 0 a 32767. O valor padrão é 5.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção cost threshold for parallelism, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção cost threshold for parallelism](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O custo refere-se a uma unidade abstraída do custo, e não a uma unidade de tempo estimado. Defina apenas **cost threshold for parallelism** em multiprocessadores simétricos.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignora o valor do **cost threshold for parallelism** nas seguintes condições:  
  
    -   Seu computador só tem um processador lógico.  
  
    -   Só um único processador lógico está disponível para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devido à opção de configuração **máscara de afinidade** .  
  
    -   A opção **max degree of parallelism** está definida como 1.  
  
 Um processador lógico é a unidade básica de hardware de processador que permite que o sistema operacional despache uma tarefa ou execute um contexto de thread. Cada processador lógico pode executar somente um contexto de thread de cada vez. O núcleo do processador é o circuito que fornece capacidade para decodificar e executar instruções. O núcleo de um processador pode conter um ou mais processadores lógicos. A consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir pode ser usada para obter informações de CPU para o sistema.  
  
```  
SELECT (cpu_count / hyperthread_ratio) AS PhysicalCPUs,   
cpu_count AS logicalCPUs   
FROM sys.dm_os_sys_info  
```  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou por um profissional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado.  
  
-   Em certos casos, pode ser escolhido um plano paralelo, embora o plano de custo da consulta seja menor do que o valor atual do **cost threshold for parallelism** . Isso pode acontecer pois a decisão de usar um plano paralelo ou serial tem base em uma estimativa de custo fornecida antes que a otimização completa seja concluída  

-   Embora o valor padrão de 5 seja mantido para compatibilidade retroativa, é provável que um valor mais alto seja apropriado para os sistemas atuais. Muitos profissionais do SQL Server sugerem um valor de 25 ou 50 como ponto de partida, bem como executar testes de aplicativos com valores superiores e inferiores para otimizar o desempenho do aplicativo.
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-cost-threshold-for-parallelism-option"></a>Para configurar a opção cost threshold for parallelism  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Avançado** .  
  
3.  Em **Paralelismo**, altere a opção **CostThresholdForParallelism** para o valor desejado. Digite ou selecione um valor de 0 a 32767.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-cost-threshold-for-parallelism-option"></a>Para configurar a opção cost threshold for parallelism  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para definir o valor da opção `cost threshold for parallelism` como `10`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cost threshold for parallelism', 10 ;  
GO  
RECONFIGURE  
GO  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção cost threshold for parallelism  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [Opção affinity mask de configuração de servidor](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
