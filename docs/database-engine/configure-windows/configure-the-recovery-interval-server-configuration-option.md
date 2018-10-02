---
title: Configurar a opção de configuração de servidor recovery interval | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- restoring recovery interval [SQL Server]
- checkpoints [SQL Server]
- recovery interval option [SQL Server]
- default recovery interval option
- time [SQL Server], recovery interval
- interval for recovery [SQL Server]
- maximum number of minutes per database recovery
- recovery [SQL Server], recovery interval option
ms.assetid: e4734b3b-8fbe-4b65-9c48-91b5a3dd18e1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b0604d33ec26d959d4f319f05fa625951e69c4a6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764994"
---
# <a name="configure-the-recovery-interval-server-configuration-option"></a>Configurar a opção recovery interval de configuração de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **recovery interval** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **recovery interval** define um limite superior em relação ao tempo que deve levar a recuperação de um banco de dados. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa o valor especificado para esta opção para determinar a frequência aproximada de emissão de [pontos de verificação automáticos](../../relational-databases/logs/database-checkpoints-sql-server.md) em um determinado banco de dados.  
  
 O valor do intervalo de recuperação padrão é 0, o que permite que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] configure automaticamente o intervalo de recuperação. Normalmente, o intervalo de recuperação padrão resulta em pontos de verificação automáticos que ocorrem aproximadamente uma vez por minuto para bancos de dados ativos e em um tempo de recuperação inferior a um minuto. Valores mais altos indicam o tempo de recuperação máximo aproximado, em minutos. Por exemplo, a definição do intervalo de recuperação como 3 indica o tempo máximo de recuperação de aproximadamente três minutos.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção de configuração de servidor recovery interval usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção recovery interval](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O intervalo de recuperação afeta apenas bancos de dados que usam o tempo de recuperação de destino padrão (0). Para anular o intervalo de recuperação de servidor em um banco de dados, configure um tempo de recuperação de destino não padrão no banco de dados. Para obter mais informações, veja [Alterar o tempo de recuperação de destino de um banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou por um profissional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado.  
  
-   Normalmente, é recomendável manter o intervalo de recuperação em 0, a menos que você tenha problemas de desempenho. Se você decidir aumentar a configuração de intervalo de recuperação, é recomendável fazer isso gradativamente, em pequenos incrementos, e avaliar o efeito de cada aumento incremental no desempenho da recuperação.  
  
-   Se você usar **sp_configure** para alterar o valor da opção **recovery interval** para mais de 60 (minutos), especifique RECONFIGURE WITH OVERRIDE. WITH OVERRIDE desabilita a verificação do valor da configuração (para valores que não são válidos ou não são recomendados).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para definir o intervalo de recuperação**  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na instância de servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Configurações de Banco de Dados** .  
  
3.  Em **Recuperação**, na caixa **Intervalo de recuperação (minutos)** , digite ou selecione um valor de 0 a 32767 para definir o intervalo máximo de tempo, em minutos, que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deveria gastar recuperando cada banco de dados na inicialização. O padrão é 0, que indica configuração automática pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Na prática, isso significa um tempo de recuperação inferior a um minuto e um ponto de verificação a cada um minuto aproximadamente para bancos de dados ativos.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-set-the-recovery-interval"></a>Para definir o intervalo de recuperação  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para definir o valor da opção `recovery interval` como `3` minutos.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'recovery interval', 3 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção recovery interval  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Alterar o tempo de recuperação de destino de um banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)   
 [Pontos de verificação de banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opção de configuração de servidor show advanced options](../../database-engine/configure-windows/show-advanced-options-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
