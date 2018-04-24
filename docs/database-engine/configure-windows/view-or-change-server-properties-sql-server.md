---
title: Exibir ou alterar propriedades do servidor (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.connectionproperties.f1
helpviewer_keywords:
- viewing server properties
- server properties [SQL Server]
- displaying server properties
- servers [SQL Server], viewing
- Connection Properties dialog box
ms.assetid: 55f3ac04-5626-4ad2-96bd-a1f1b079659d
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4a0df8ff3a0758558e38607e4895b7552bb12d00
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="view-or-change-server-properties-sql-server"></a>Exibir ou alterar propriedades de servidor (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como exibir ou alterar as propriedades de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou SQL Server Configuration Manager.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para exibir ou alterar propriedades de servidor, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SQL Server Configuration Manager](#PowerShellProcedure)  
  
-   **Acompanhamento:**  [depois que você altera as propriedades de servidor](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Ao usar sp_configure, você deve executar RECONFIGURE ou RECONFIGURE WITH OVERRIDE depois de definir uma opção de configuração. A instrução RECONFIGURE WITH OVERRIDE normalmente é reservada para opções de configuração que devem ser usadas com extrema cautela. Entretanto, RECONFIGURE WITH OVERRIDE funciona com todas as opções de configuração e você pode usá-la em vez de RECONFIGURE.  
  
    > [!NOTE]  
    >  RECONFIGURE é executada em uma transação. Se ocorrer falha de alguma operação de reconfiguração, nenhuma das operações de reconfiguração entrará em vigor.  
  
-   Algumas páginas de propriedades apresentam informações obtidas através da WMI (Instrumentação de Gerenciamento do Windows). Para exibir essas páginas, a WMI deve ser instalada no computador que está executando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para obter mais informações, veja [Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md).  
  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-or-change-server-properties"></a>Para exibir ou alterar propriedades de servidor  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades do Servidor** , clique em uma página para exibir ou alterar informações de servidor sobre ela. Algumas propriedades são somente leitura.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-server-properties-by-using-the-serverproperty-built-in-function"></a>Para exibir propriedades de servidor usando a função interna SERVERPROPERTY  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo usa a função [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md) em uma função interna em uma instrução `SELECT` para retornar informações sobre o servidor atual. Essa situação é útil quando existem diversas instâncias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas no servidor Windows e o cliente deve abrir outra conexão à mesma instância usada pela conexão atual.  
  
    ```sql  
    SELECT CONVERT( sysname, SERVERPROPERTY('servername'));  
    GO  
    ```  
  
#### <a name="to-view-server-properties-by-using-the-sysservers-catalog-view"></a>Para exibir propriedades de servidor usando a exibição do catálogo sys.servers  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo consulta a exibição de catálogo [sys.servers](../../relational-databases/system-catalog-views/sys-servers-transact-sql.md) para retornar o nome (`name`) e a ID (`server_id`) do servidor atual e o nome do provedor OLE DB (`provider`) para conectar a um servidor vinculado.  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    SELECT name, server_id, provider  
    FROM sys.servers ;   
    GO  
  
    ```  
  
#### <a name="to-view-server-properties-by-using-the-sysconfigurations-catalog-view"></a>Para exibir propriedades de servidor usando a exibição do catálogo sys.configurations  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo consulta a exibição do catálogo [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para retornar informações sobre cada opção de configuração de servidor no servidor atual. O exemplo retorna o nome (`name`) e a descrição (`description`) da opção e se a opção é uma opção avançada (`is_advanced`).  
  
    ```wmimof  
    USE AdventureWorks2012;   
    GO  
    SELECT name, description, is_advanced  
    FROM sys.configurations ;   
    GO  
  
    ```  
  
#### <a name="to-change-a-server-property-by-using-spconfigure"></a>Para alterar uma propriedade de servidor usando sp_configure  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para alterar a propriedade de um servidor. O exemplo altera o valor da opção `fill factor` para `100`. O servidor deve ser reiniciado para que a alteração entre em vigor.  
  
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
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="PowerShellProcedure"></a> Usando o SQL Server Configuration Manager  
 Algumas propriedades de servidor podem ser exibidas ou alteradas usando o SQL Server Configuration Manager Por exemplo, você pode exibir a versão e a edição da instância de SQL Server ou alterar o local onde os arquivos do log de erros estão armazenados. Estas propriedades também podem ser exibidas consultando [Funções e exibições de gerenciamento dinâmico relacionadas ao servidor](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md).  
  
#### <a name="to-view-or-change-server-properties"></a>Para exibir ou alterar propriedades de servidor  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
2.  No **SQL Server Configuration Manager**, clique em **Serviços do SQL Server**.  
  
3.  No painel de detalhes, clique com o botão direito do mouse em **SQL Server (\<***instancename***>)** e, depois, clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades do SQL Server (\<***instancename***>)**, altere as propriedades do servidor na guia **Serviço** ou na guia **Avançado** e, depois, clique em **OK**.  
  
##  <a name="FollowUp"></a> Acompanhamento: depois que você altera as propriedades de servidor  
 Para algumas propriedades, o servidor terá que ser reiniciado antes de a alteração entrar em vigor.  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Configurar o WMI para mostrar o status do servidor nas Ferramentas do SQL Server](http://msdn.microsoft.com/library/7e97197b-ed4d-40d1-9a52-9ab1d92401d7)   
 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)   
 [Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Exibições e funções de gerenciamento dinâmico relacionadas ao servidor &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
