---
title: Configurar a opção de configuração de servidor min memory per query | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- memory [SQL Server], queries
- minimum query memory
- queries [SQL Server], memory
- min memory per query option
ms.assetid: ecd3fb79-b4a6-432f-9ef5-530e0d42d5a6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: dfee7265529419aecf2b05831503ed134b93f525
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62787027"
---
# <a name="configure-the-min-memory-per-query-server-configuration-option"></a>Configurar a opção min memory per query de configuração de servidor
  Este tópico descreve como configurar a opção `min memory per query` de configuração de servidor [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o. A `min memory per query` opção especifica a quantidade mínima de memória (em quilobytes) que será alocada para a execução de uma consulta. Por exemplo, se `min memory per query` for definido como 2.048 KB, a consulta será garantida para obter pelo menos essa quantidade total de memória. O valor padrão é 1.024 KB. O valor mínimo é de 512 KB e o valor máximo é 2.147.483.647 KB (2 GB).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção mín. de memória por consulta usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção mín. de memória por consulta](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A opção amount of min memory per query tem precedência sobre a [Opção index create memory](configure-the-index-create-memory-server-configuration-option.md). Quando ambas as opções são modificadas, e a index create memory é inferior à min memory per query, você recebe uma mensagem de aviso, mas o valor é definido. Durante a execução da consulta, você receberá um outro aviso semelhante.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   O processador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta determinar a quantidade ideal de memória a ser alocada para uma consulta. A opção min memory per query deixa o administrador especificar a quantia mínima de memória que qualquer consulta única recebe. As consultas geralmente receberão mais memória que isso, se tiverem operações hash e de classificação em um grande volume de dados. Aumentar o valor de min memory per query pode melhorar o desempenho para algumas consultas de tamanho pequeno a médio, mas fazer isso poderia conduzir a uma maior competição por recursos de memória. A opção min memory per query inclui a memória alocada para classificação.  
  
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
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para definir o valor da opção `min memory per query` como `3500` KB.  
  
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
  
##  <a name="FollowUp"></a>Acompanhamento: depois de configurar a opção mín. de memória por consulta  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Configurar a opção index create memory de configuração de servidor](configure-the-index-create-memory-server-configuration-option.md)  
  
  
