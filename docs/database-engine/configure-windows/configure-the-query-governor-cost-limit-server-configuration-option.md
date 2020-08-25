---
title: Configurar a opção de configuração de servidor query governor cost limit | Microsoft Docs
description: Saiba mais sobre a opção query governor cost limit. Confira como usá-la para limitar a execução de consultas.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], time to execute
- query governor cost limit option [SQL Server]
- time [SQL Server], query run time
ms.assetid: e7b8f084-1052-4133-959b-cebf4add790f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 02b34ab8d3c0a3efd79d7d136bf26401ba92fdf4
ms.sourcegitcommit: bf8cf755896a8c964774a438f2bd461a2a648c22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2020
ms.locfileid: "88216734"
---
# <a name="configure-the-query-governor-cost-limit-server-configuration-option"></a>Configurar a opção query governor cost limit de configuração de servidor
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este tópico descreve como configurar a opção de configuração de servidor **query governor cost limit** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção de limite de custo especifica um limite superior de custo estimado permitido para a execução de determinada consulta. O custo da consulta é um número abstrato determinado pelo otimizador de consulta com base em requisitos de execução estimados, como tempo de CPU, memória e E/S de disco. Ele se refere a um tempo decorrido estimado, em segundos, que seria necessário para concluir uma consulta em uma configuração de hardware específica. Esse número abstrato não equivale ao tempo necessário para concluir uma consulta na instância em execução. Ele deve ser tratado como uma medida relativa. O valor padrão para esta opção é 0, que define o administrador de consultas como desativado. Definir o valor como 0 permite que todas as consultas sejam executadas sem limite de tempo. Se você especificar um valor que não seja zero nem negativo, o administrador de consultas proibirá a execução de qualquer consulta com um custo estimado que exceda esse valor.   
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção query governor cost limit, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção query governor cost limit](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou por um profissional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado.  
  
-   Para alterar o valor de query governor cost limit com base na conexão, use a instrução [SET QUERY_GOVERNOR_COST_LIMIT](../../t-sql/statements/set-query-governor-cost-limit-transact-sql.md) .  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-query-governor-cost-limit-option"></a>Para configurar a opção query governor cost limit  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique na página **Conexões** .  
  
3.  Marque ou desmarque a caixa de seleção **Usar administrador de consultas para evitar consultas demoradas** .  
  
     Se você marcar essa caixa de seleção, na caixa abaixo, insira um valor positivo a ser usado pelo administrador de consultas para impedir a execução de qualquer consulta com um custo estimado que ultrapasse esse valor.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-query-governor-cost-limit-option"></a>Para configurar a opção query governor cost limit  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para definir o valor da opção `query governor cost limit` como um limite superior de custo de consulta estimado de `120`.
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'query governor cost limit', 120 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="follow-up-after-you-configure-the-query-governor-cost-limit-option"></a><a name="FollowUp"></a> Acompanhamento: depois de configurar a opção query governor cost limit  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](../../t-sql/statements/set-query-governor-cost-limit-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
