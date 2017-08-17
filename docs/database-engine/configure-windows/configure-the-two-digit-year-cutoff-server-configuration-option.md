---
title: "Configurar a opção de configuração de servidor two digit year cutoff | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- two digit year cutoff option
- four-digit years [SQL Server]
ms.assetid: d94e81b6-f2e6-47ef-b497-ec3d827a1646
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 89f836cc68e58573e4e05da71f1081542406cd49
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="configure-the-two-digit-year-cutoff-server-configuration-option"></a>Configurar a opção two digit year cutoff de configuração de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **two digit year cutoff** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **two digit year cutoff** especifica um número inteiro de 1753 até 9999 que representa o ano de corte para interpretar anos com dois dígitos como anos com quatro dígitos. O tempo padrão abrangido para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é 1950-2049, que representa um ano de corte de 2049. Isso significa que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta um ano de dois dígitos de 49 como 2049, um ano de dois dígitos 50 como 1950 e um ano de dois dígitos 99 como 1999. Para manter a compatibilidade com versões anteriores, deixe a configuração no valor padrão.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção two-digit year cutoff, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [após configurar a opção two-digit year cutoff](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Objetos de automação OLE usam 2030 como o ano de corte de dois dígitos. Você pode usar a opção **two digit year cutoff** para proporcionar consistência em valores de data entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aplicativos cliente. Porém, para evitar ambiguidade de datas, use anos de quatro dígitos em seus dados.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-two-digit-year-cutoff-option"></a>Para configurar a opção two-digit year cutoff  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Configuração de servidores diversos** .  
  
3.  Em **Suporte a ano de dois dígitos**, na caixa **Quando um ano de dois dígitos é inserido**, **interprete como um ano intermediário** , digite ou selecione um valor que é o ano final do tempo abrangido.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-configure-the-two-digit-year-cutoff-option"></a>Para configurar a opção two-digit year cutoff  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para definir o valor da opção `two digit year cutoff` como `2030`.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'two digit year cutoff', 2030 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Para obter mais informações, consulte [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: após configurar a opção two-digit year cutoff  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  

