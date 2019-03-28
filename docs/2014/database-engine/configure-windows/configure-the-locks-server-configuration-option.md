---
title: Configurar a opção de configuração de servidor locks | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- locks option [SQL Server]
ms.assetid: b0cf0f86-7652-4574-a9fb-908e10d03973
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 22f47a80a73efc8d462ef8f26f2e6b0fb5b3f3c7
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530543"
---
# <a name="configure-the-locks-server-configuration-option"></a>Configurar a opção locks de configuração de servidor
  Este tópico descreve como configurar a opção de configuração de servidor **locks** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **locks** define o número máximo de bloqueios disponíveis, limitando a quantidade de memória que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa para eles. A configuração padrão é 0, a qual permite que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] aloque e desaloque as estruturas de bloqueio de forma dinâmica, baseado nas alterações de requisitos de sistema.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção locks, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [Depois de configurar a opção locks](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Quando o servidor é iniciado com **bloqueios** definido como 0, o gerenciador de bloqueio adquire memória suficiente do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para um pool inicial de 2.500 estruturas de bloqueio. Conforme o pool de bloqueio é esgotado, memória adicional é adquirida para o pool.  
  
     Geralmente, se for necessária mais memória para o pool de bloqueio do que a que está disponível no pool de memória do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , e se mais memória do computador estiver disponível (o limite de **memória máxima do servidor** não foi atingido), o [!INCLUDE[ssDE](../../includes/ssde-md.md)] alocará memória dinamicamente para satisfazer a solicitação de bloqueios. No entanto, se a alocação dessa memória provocar paginação no nível do sistema operacional (por exemplo, se outro aplicativo estiver executando no mesmo computador como uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usando essa memória), mais espaço de bloqueio não será alocado. O pool de bloqueios dinâmico não adquire mais que 60 por cento da memória alocada para o [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Depois que o pool de bloqueios atingiu 60 por cento da memória adquirida por uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]ou quando não houver mais memória disponível no computador as solicitações de bloqueios adicionais gerarão um erro.  
  
     Recomenda-se permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use bloqueios dinamicamente. No entanto, você pode definir **bloqueios** e substituir a capacidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de alocar recursos de bloqueio dinamicamente. Quando a opção **bloqueios** está definida com um valor diferente de 0, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não pode alocar mais bloqueios do que o valor especificado em **bloqueios**. Aumente esse valor se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibir uma mensagem de que você excedeu o número de bloqueios disponíveis. Como cada bloqueio consome memória (96 bytes por bloqueio), aumentar esse valor pode exigir o aumento da quantidade de memória dedicada para o servidor.  
  
-   A opção **bloqueios** também é afetada quando ocorre escalonamento de bloqueio. Quando a opção **bloqueios** está definida como 0, o escalonamento de bloqueio ocorre quando a memória usada pelas estruturas de bloqueio atuais atingir 40 por cento do pool de memória do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Quando a opção **bloqueios** não está definida como 0, o escalonamento de bloqueio ocorre quando o número de bloqueios atinge 40 por cento do valor especificado para **bloqueios**.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-locks-option"></a>Para configurar a opção locks  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Avançado** .  
  
3.  No item **Paralelismo**, digite o valor desejado para a opção **locks** .  
  
     Use a opção **locks** para definir o número máximo de bloqueios disponíveis, limitando a quantidade de memória que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para eles.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-locks-option"></a>Para configurar a opção locks  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para definir o valor da opção `locks` para definir o número de bloqueios disponíveis para todos os usuários como `20000`.  
  
```sql  
Use AdventureWorks2012 ;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'locks', 20000;  
GO  
RECONFIGURE;  
GO  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: Depois de configurar a opção locks  
 O servidor deve ser reiniciado para que a configuração entre em vigor.  
  
## <a name="see-also"></a>Consulte também  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
