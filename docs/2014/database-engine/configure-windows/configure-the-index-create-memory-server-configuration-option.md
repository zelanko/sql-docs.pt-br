---
title: Configurar a opção de configuração de servidor index create memory | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- index create memory option
ms.assetid: 3d722d9b-bada-4bf5-a9d7-bfc556bb4915
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6cd0aeb93d3fb68089338335068fdaaae19919fa
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935682"
---
# <a name="configure-the-index-create-memory-server-configuration-option"></a>Configurar a opção de configuração de servidor index create memory
  Este tópico descreve como configurar a opção de configuração de servidor **index create memory** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **index create memory** controla a quantidade máxima de memória alocada inicialmente para criar índices. O valor padrão dessa opção é 0 (autoconfigurável). Se mais tarde for preciso mais memória para criação de índice e a memória estiver disponível, o servidor irá usá-la, excedendo assim a configuração dessa opção. Se a memória adicional não estiver disponível, a criação de índice continuará usando a memória já alocada.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção index create memory usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção index create memory](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   A configuração da opção **min memory per query** tem precedência sobre a opção **index create memory** . Quando ambas as opções são alteradas, e a **index create memory** é inferior à **min memory per query**, você recebe uma mensagem de aviso, mas o valor foi definido. Durante a execução de consulta, você recebe um aviso semelhante.  
  
-   Ao usar tabelas e índices particionados, os requisitos mínimos de memória para criação de índice podem aumentar significativamente se houver índices particionados não alinhados e um alto grau de paralelismo. Essa opção controla a quantidade inicial total de memória alocada para todas as partições de índice em uma única operação de criação de índice. A consulta terminará com uma mensagem de erro se a quantidade definida por essa opção for inferior ao mínimo exigido para a execução da consulta.  
  
-   O valor de execução para essa opção não excederá a quantidade real de memória que pode ser usada pelo sistema operacional e pela plataforma de hardware nas quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado. Em sistemas operacionais de 32 bits, o valor de execução será inferior a 3 GB (gigabytes).  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   A opção **memória de criação de índice** é autoconfigurável e, normalmente, opera sem necessidade de ajustes. Porém, se você tiver dificuldade para criar índices, considere aumentar o valor dessa opção a partir de seu valor de execução.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-index-create-memory-option"></a>Para configurar a opção index create memory  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Memória** .  
  
3.  Em **Memória de criação de índice**, digite ou selecione o valor desejado para a opção index create memory.  
  
     Use a opção **index create memory** para controlar a quantidade de memória usada por classificações de criação de índice. A opção **memória de criação de índice** é autoconfigurável e deve funcionar na maioria dos casos sem necessidade de ajustes. Porém, se você tiver dificuldade para criar índices, considere aumentar o valor dessa opção a partir de seu valor de execução. Classificações de consulta são controladas pela opção **min memory per query** .  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-index-create-memory-option"></a>Para configurar a opção index create memory  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para definir o valor da opção `index create memory` como `4096`.  
  
```sql  
USE AdventureWorks2012 ;  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
EXEC sp_configure 'index create memory', 4096  
GO  
RECONFIGURE;  
GO  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="follow-up-after-you-configure-the-index-create-memory-option"></a><a name="FollowUp"></a> Acompanhamento: depois de configurar a opção index create memory  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [sys.configurations &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-configurations-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração de servidor de memória do servidor](server-memory-server-configuration-options.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
