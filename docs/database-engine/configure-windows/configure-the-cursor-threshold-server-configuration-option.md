---
title: Configurar a opção de configuração de servidor cursor threshold | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cursor threshold option
ms.assetid: 189f2067-c6c4-48bd-9bd9-65f6b2021c12
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 1a3610cddb39db4930bfb401fc9be7351f4f7223
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66761763"
---
# <a name="configure-the-cursor-threshold-server-configuration-option"></a>Configurar a opção de configuração de servidor cursor threshold
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **cursor threshold** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **cursor threshold** especifica o número de linhas no conjunto de cursores em que os conjuntos de chaves de cursor são gerados de forma assíncrona. Quando os cursores geram um conjunto de chaves para um conjunto de resultados, o otimizador de consulta calcula o número de linhas que serão retornadas para aquele conjunto de resultados. Se o otimizador de consulta calcular que o número de linhas retornadas é maior do que esse limite, o cursor será gerado de forma assíncrona, permitindo que o usuário busque linhas do cursor enquanto o cursor continua sendo populado. Caso contrário, o cursor é gerado de forma síncrona e a consulta aguarda até que todas as linhas sejam retornadas.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção cursor threshold usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção cursor threshold](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte à geração de cursores [!INCLUDE[tsql](../../includes/tsql-md.md)] controlados por conjunto de chaves ou estáticos de forma assíncrona. [!INCLUDE[tsql](../../includes/tsql-md.md)] , como OPEN ou FETCH, são em lote, de modo que não é preciso gerar cursores [!INCLUDE[tsql](../../includes/tsql-md.md)] assincronamente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] continua a dar suporte a cursores de servidor de API (interface de programação de aplicativo) estáticos ou controlados por conjunto de chaves assíncronos nos quais OPEN de baixa latência é uma preocupação devido às viagens de ida e volta do cliente para cada operação de cursor.  
  
-   A exatidão do otimizador de consulta para determinar uma estimativa do número de linhas em um conjunto de chaves depende da moeda das estatísticas para cada tabela no cursor.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou por um profissional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado.  
  
-   Se você definir o **cursor threshold** como -1, todos os conjuntos de chaves serão gerados de forma síncrona, o que beneficiará pequenos conjuntos de cursores. Se você definir o **cursor threshold** como 0, todos os conjuntos de chaves serão gerados de forma assíncrona. Com outros valores, o otimizador de consulta irá comparar o número de linhas previstas no cursor definido e criará o conjunto de chaves de forma assíncrona se ele exceder o número definido em **cursor threshold**. Não defina **cursor threshold** com um valor muito baixo, pois conjuntos de resultados pequenos são criados melhor de forma síncrona.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>Para configurar a opção cursor threshold  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Avançado** .  
  
3.  Em **Diversos**, altere a opção **Limite do Cursor** para o valor desejado.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>Para configurar a opção cursor threshold  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para definir a opção `cursor threshold` como `0` para que os conjuntos de chaves dos cursores sejam gerados de forma assíncrona.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cursor threshold', 0 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção cursor threshold  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)  
  
  
