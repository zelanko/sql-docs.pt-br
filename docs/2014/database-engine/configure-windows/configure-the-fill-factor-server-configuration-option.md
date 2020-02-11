---
title: Configurar a opção de configuração de servidor fill factor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- fill factor option [SQL Server]
ms.assetid: b920ec34-ba8b-4bb8-af53-a3ffd06bafa6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 558218b4cff8e9d4ce100a92135f0fee4e0e09c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62786764"
---
# <a name="configure-the-fill-factor-server-configuration-option"></a>Configurar a opção fill factor de configuração de servidor
  Este tópico descreve como configurar a opção de configuração de servidor **fill factor** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. O fator de preenchimento é fornecido para ajustar o armazenamento e o desempenho de dados de índice. Quando um índice é criado ou recriado, o valor de fator de preenchimento determina a porcentagem de espaço em cada página de nível folha a ser preenchida com dados, reservando o restante como espaço livre para futuro crescimento. Para obter mais informações, veja [Especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção fill factor, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção fill factor option](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-fill-factor-option"></a>Para configurar a opção fill factor  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Configurações de Banco de Dados** .  
  
3.  Na caixa **Fator de preenchimento padrão do índice** , digite ou selecione o fator de preenchimento do índice desejado.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-fill-factor-option"></a>Para configurar a opção fill factor  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para definir o valor da opção `fill factor` como `100`.  
  
```sql  
Use AdventureWorks2012;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'fill factor', 100;  
GO  
RECONFIGURE;  
GO  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção fill factor option  
 O servidor deve ser reiniciado para que a configuração entre em vigor.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [Especificar o fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)  
  
  
