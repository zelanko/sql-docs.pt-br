---
title: Configurar a opção de configuração de servidor min memory per query | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- memory [SQL Server], queries
- minimum query memory
- queries [SQL Server], memory
- min memory per query option
- min memory grant
ms.assetid: ecd3fb79-b4a6-432f-9ef5-530e0d42d5a6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9e7a08defb9ff222ac1699c924691c923a7f2c2e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68012508"
---
# <a name="configure-the-min-memory-per-query-server-configuration-option"></a>Configurar a opção min memory per query de configuração de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **min memory per query** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **min memory per query** especifica a quantidade mínima de memória (em quilobytes) que será alocada para a execução de uma consulta. Isso também é conhecido como a concessão de memória mínima. Por exemplo, se **min memory per query** for definida como 2.048 KB, a consulta terá a garantia de obter no mínimo esse total de memória. O valor padrão é 1.024 KB. O valor mínimo é de 512 KB e o valor máximo é 2.147.483.647 KB (2 GB).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção min memory per query usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção min memory per query](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A quantidade mínima de memória por consulta tem precedência sobre a opção [index create memory](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md). Quando ambas as opções são modificadas, e a index create memory é inferior à min memory per query, você recebe uma mensagem de aviso, mas o valor é definido. Durante a execução da consulta, você receberá um outro aviso semelhante.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou por um profissional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado.  
  
-   O processador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta determinar a quantidade ideal de memória a ser alocada para uma consulta. A opção min memory per query deixa o administrador especificar a quantia mínima de memória que qualquer consulta única recebe. As consultas geralmente receberão mais memória que isso se tiverem operações hash e de classificação em um grande volume de dados. Aumentar o valor de min memory per query pode melhorar o desempenho para algumas consultas de tamanho pequeno a médio, mas fazer isso poderia conduzir a uma maior competição por recursos de memória. A opção min memory per query inclui a memória alocada para as operações de classificação.  

-    Não defina a opção de configuração do servidor min memory per query com um valor alto demais, especialmente em sistemas muito ativos, pois, nesse caso, a consulta tem que esperar<sup>1</sup> até que possa assegurar a memória mínima solicitada ou até que o valor especificado na opção de configuração do servidor query wait seja excedido. Se houver mais memória disponível do que o valor mínimo necessário especificado para executar a consulta, será permitido que a consulta use a memória adicional, desde que essa memória possa ser usada com eficiência pela consulta.     

<sup>1</sup> Nesse cenário, o tipo de espera costuma ser RESOURCE_SEMAPHORE. Para obter mais informações, confira [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).

###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>Para configurar a opção min memory per query  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Memória** .  
  
3.  Na caixa **Memória mínima por consulta** , insira a quantidade mínima de memória (em quilobytes) que será alocada para a execução de uma consulta.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>Para configurar a opção min memory per query  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para definir o valor da opção `min memory per query` como `3500` KB.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'min memory per query', 3500 ;  
GO  
RECONFIGURE;  
GO    
```  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção min memory per query  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Configurar a opção de configuração do servidor de memória de criação de índice](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)     
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)
  
  
