---
title: "Definir as configurações da propriedade FailureConditionLevel | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 513dd179-9a46-46da-9fdd-7632cf6d0816
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 46e7f2aca995373d14ce0096a4dba4204cc69ece
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="configure-failureconditionlevel-property-settings"></a>Definir as configurações da propriedade FailureConditionLevel
  Use a propriedade FailureConditionLevel para definir as condições da FCI (Instância de Cluster de Failover) AlwaysOn para failover ou reinicialização. As alterações feitas nessa propriedade são aplicadas imediatamente, sem a necessidade de uma reinicialização do serviço WSFC (Windows Server Failover Cluster) ou do recurso FCI.  
  
-   **Before you begin:**  [FailureConditionLevel Property Settings](#Restrictions), [Security](#Security)  
  
-   **To configure the FailureConditionLevel property settings using,** [PowerShell](#PowerShellProcedure), [Failover Cluster Manager](#WSFC), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Configurações da propriedade FailureConditionLevel  
 As condições de falha são definidas em uma escala crescente. Para os níveis 1-5, cada um deles deve incluir todas as condições dos níveis anteriores, além de suas próprias condições. Isso significa que, a cada nível, há uma probabilidade crescente de failover ou reinicialização.  Para obter mais informações, consulte a seção "Determinando falhas" do tópico [Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md) .  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer as permissões ALTER SETTINGS e VIEW SERVER STATE.  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
  
##### <a name="to-configure-failureconditionlevel-settings"></a>Para configurar a propriedade FailureConditionLevel  
  
1.  Inicie um Windows PowerShell elevado via **Executar como Administrador**.  
  
2.  Importe o módulo **FailoverClusters** para habilitar cmdlets de cluster.  
  
3.  Use o cmdlet **Get-ClusterResource** para encontrar o recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Em seguida, use o cmdlet **Set-ClusterParameter** para definir a propriedade **FailureConditionLevel** de uma Instância de Cluster de Failover.  
  
> [!TIP]  
>  Sempre que você abrir uma nova janela do PowerShell, deverá importar o módulo **FailoverClusters** .  
  
### <a name="example-powershell"></a>Exemplo (PowerShell)  
 O exemplo a seguir altera a configuração FailureConditionLevel no recurso " [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] " do`SQL Server (INST1)`para fazer failover ou reiniciar em erros de servidor críticos.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter FailureConditionLevel 3  
  
```  
  
### <a name="related-content-powershell"></a>Conteúdo relacionado (PowerShell)  
  
-   [Clustering e alta disponibilidade](http://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (Blog da equipe de Clustering de Failover e Balanceamento de Carga de Rede)  
  
-   [Guia de Introdução ao Windows PowerShell em um cluster de failover](http://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandos de recursos de cluster e cmdlets equivalentes no Windows PowerShell](http://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a> Usando o snap-in Gerenciador de Cluster de Failover  
 **Para definir as configurações da propriedade FailureConditionLevel:**  
  
1.  Abra o snap-in Gerenciador de Cluster de Failover.  
  
2.  Expanda **Serviços e Aplicativos** e selecione a FCI.  
  
3.  Clique com o botão direito do mouse em **Recurso do SQL Server** em **Outros Recursos**e selecione **Propriedades** no menu de atalho. A caixa de diálogo **Propriedades** do recurso do SQL Server é aberta.  
  
4.  Selecione a guia **Propriedades** , insira o valor desejado para a propriedade **FaliureConditionLevel** propriedade e clique em **OK** para aplicar a alteração.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para definir as configurações da propriedade FailureConditionLevel:**  
  
 Usando a instrução [ALTER SERVER CONFIGURATION](../../../t-sql/statements/alter-server-configuration-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] , você pode especificar o valor da propriedade FailureConditionLevel.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir define a propriedade FailureConditionLevel como 0, indicando que nenhum failover ou reinicialização será disparado automaticamente em nenhuma condição de falha.  
  
```  
ALTER SERVER CONFIGURATION SET FAILOVER CLUSTER PROPERTY FailureConditionLevel = 0;  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)   
 [Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  
