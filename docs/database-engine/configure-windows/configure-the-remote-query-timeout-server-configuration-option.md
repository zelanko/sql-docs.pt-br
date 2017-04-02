---
title: "Configurar a op&#231;&#227;o de configura&#231;&#227;o de servidor remote query timeout | Microsoft Docs"
ms.custom: ""
ms.date: "03/08/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "limite de tempo para consultas remotas [SQL Server]"
  - "opção remote query timeout"
ms.assetid: 888c8448-933b-41e3-8aa1-c206bc0cdb78
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Configurar a op&#231;&#227;o de configura&#231;&#227;o de servidor remote query timeout
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **remote query timeout** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **remote query timeout** especifica quanto tempo, em segundos, uma operação remota pode levar antes de o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exceder o tempo limite. O valor padrão para essa opção é 600, o que permite uma espera de 10 minutos. Esse valor é aplicado a uma conexão de saída iniciada pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] como uma consulta remota. Esse valor não tem nenhum efeito em consultas recebidas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para desabilitar o tempo limite, defina o valor como 0. A consulta aguardará até ser cancelada.  
  
 Para consultas heterogêneas, **remote query timeout** especifica o número de segundos (inicializado no objeto de comando usando a propriedade de conjunto de linhas DBPROP_COMMANDTIMEOUT) que um provedor remoto deve esperar para os conjuntos de resultados antes de a consulta exceder o tempo limite. Esse valor é usado também para definir o DBPROP_GENERALTIMEOUT se o provedor remoto oferecer suporte a ele. Isso fará com que qualquer outra operação exceda o tempo limite depois do número especificado de segundos.  
  
 Para procedimentos armazenados remotos, **remote query timeout** especifica o número de segundos que devem decorrer depois de enviar uma instrução remota `EXEC` antes de o procedimento armazenado remoto exceder o tempo limite.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção remote query timeout usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção remote query timeout](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Devem ser permitidas conexões de servidor remoto antes que este valor possa ser definido.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para configurar a opção remote query timeout  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Conexões** .  
  
3.  Em **Conexões do servidor remoto**, na caixa **Tempo limite de consulta remota** , digite ou selecione um valor de 0 a 2.147.483.647 para definir o número máximo de segundos que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve aguardar antes de o tempo limite ser excedido.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para configurar a opção remote query timeout  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para definir o valor da opção `remote query timeout` como `0` para desabilitar o tempo limite.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'remote query timeout', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 Para obter mais informações, consulte [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção remote query timeout  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## Consulte também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Propriedades e comportamentos do conjunto de linhas](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  