---
title: Definir as configurações da propriedade FailureConditionLevel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 513dd179-9a46-46da-9fdd-7632cf6d0816
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8924b864d7cc8be078b370e3182713114f54ff6c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062517"
---
# <a name="configure-failureconditionlevel-property-settings"></a>Definir as configurações da propriedade FailureConditionLevel
  Use a propriedade FailureConditionLevel para definir as condições da FCI AlwaysOn para failover ou reinicialização. As alterações feitas nessa propriedade são aplicadas imediatamente, sem a necessidade de uma reinicialização do serviço WSFC (Windows Server Failover Cluster) ou do recurso FCI.  
  
-   **Antes de começar:**  [Configurações da propriedade FailureConditionLevel](#Restrictions), [Segurança](#Security)  
  
-   **Para definir as configurações de propriedade de FailureConditionLevel usando:** [PowerShell](#PowerShellProcedure), [Gerenciador de Cluster de Failover](#WSFC) e [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="failureconditionlevel-property-settings"></a><a name="Restrictions"></a> Configurações da propriedade FailureConditionLevel  
 As condições de falha são definidas em uma escala crescente. Para os níveis 1-5, cada um deles deve incluir todas as condições dos níveis anteriores, além de suas próprias condições. Isso significa que, a cada nível, há uma probabilidade crescente de failover ou reinicialização.  Para obter mais informações, consulte a seção "Determinando falhas" do tópico [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md) .  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer as permissões ALTER SETTINGS e VIEW SERVER STATE.  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
  
### <a name="to-configure-failureconditionlevel-settings"></a>Para configurar a propriedade FailureConditionLevel  
  
1.  Inicie um Windows PowerShell elevado via **Executar como Administrador**.  
  
2.  Importe o módulo `FailoverClusters` para habilitar cmdlets de cluster.  
  
3.  Use o `Get-ClusterResource` cmdlet para localizar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recurso e, em seguida, use o `Set-ClusterParameter` cmdlet para definir a propriedade **FailureConditionLevel** para uma instância de cluster de failover.  
  
> [!TIP]  
>  Sempre que você abrir uma nova janela do PowerShell, deverá importar o módulo `FailoverClusters`.  

 O exemplo a seguir altera a configuração FailureConditionLevel no recurso " [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] " do`SQL Server (INST1)`para fazer failover ou reiniciar em erros de servidor críticos.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter FailureConditionLevel 3
```  
  
### <a name="related-content-powershell"></a>Conteúdo relacionado (PowerShell)  
  
-   [Clustering e alta disponibilidade](https://techcommunity.microsoft.com/t5/failover-clustering/bg-p/FailoverClustering) (Blog da equipe de Clustering de Failover e Balanceamento de Carga de Rede)  
  
-   [Guia de Introdução ao Windows PowerShell em um cluster de failover](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandos de recursos de cluster e cmdlets equivalentes no Windows PowerShell](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="using-the-failover-cluster-manager-snap-in"></a><a name="WSFC"></a> Usando o snap-in Gerenciador de Cluster de Failover  

### <a name="to-configure-failureconditionlevel-property-settings"></a>Para definir as configurações da propriedade FailureConditionLevel
  
1.  Abra o snap-in Gerenciador de Cluster de Failover.  
  
2.  Expanda **Serviços e Aplicativos** e selecione a FCI.  
  
3.  Clique com o botão direito do mouse em **Recurso do SQL Server** em **Outros Recursos**e selecione **Propriedades** no menu de atalho. A caixa de diálogo **Propriedades** do recurso do SQL Server é aberta.  
  
4.  Selecione a guia **Propriedades** , insira o valor desejado para a propriedade **FaliureConditionLevel** propriedade e clique em **OK** para aplicar a alteração.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  

### <a name="to-configure-failureconditionlevel-property-settings"></a>Para definir as configurações da propriedade FailureConditionLevel
  
 Usando a instrução [ALTER Server Configuration](/sql/t-sql/statements/alter-server-configuration-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] , você pode especificar o valor da propriedade FailureConditionLevel.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir define a propriedade FailureConditionLevel como 0, indicando que nenhum failover ou reinicialização será disparado automaticamente em nenhuma condição de falha.  
  
```sql
ALTER SERVER CONFIGURATION SET FAILOVER CLUSTER PROPERTY FailureConditionLevel = 0;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_server_diagnostics](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)   
 [Política de failover para instâncias de cluster de failover](failover-policy-for-failover-cluster-instances.md)  
