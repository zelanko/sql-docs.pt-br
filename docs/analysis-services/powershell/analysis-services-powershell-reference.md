---
title: "Referência do PowerShell do Analysis Services | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/21/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 6c435e40-bfaf-4073-8cef-bc3260602246
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7999198236f93a1c64ea731659017bce4efd3e55
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-powershell-reference"></a>Referência do Analysis Services PowerShell

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]


  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Cmdlets do PowerShell são incluídos no [módulo do SqlServer](https://www.powershellgallery.com/packages/SqlServer/21.0.17099). 
  
>[!NOTE] 
> Operações de banco de dados do Analysis Services do Azure usam o módulo do SqlServer mesmo como o SQL Server Analysis Services. No entanto, nem todos os cmdlets têm suporte para serviços de análise do Azure. Para obter mais informações, consulte [gerenciar serviços de análise do Azure com o PowerShell](https://docs.microsoft.com/azure/analysis-services/analysis-services-powershell).
  
##  <a name="bkmk_cmdlets"></a> Cmdlets do Analysis Services  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece cmdlets correspondem aos métodos no **Microsoft. AnalysisServices** namespace. A tabela a seguir descreve cada cmdlet e fornece um link para o método AMO correspondente.  
  
 Se você quiser usar o PowerShell para executar uma tarefa que não esteja representada na lista a seguir (por exemplo, para criar ou sincronizar um banco de dados), escreva um script TMSL ou XMLA para essa ação e execute-o usando o cmdlet **Invoke-ASCmd** .  
  
|Cmdlet|Description|Métodos equivalentes do AMO|  
|------------|-----------------|----------------------------|  
|[Cmdlet Add-RoleMember](../../analysis-services/powershell/add-rolemember-cmdlet.md)|Adicionar um membro a uma função de banco de dados.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Cmdlet Backup-ASDatabase](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)|Fazer backup de um banco de dados do Analysis Services.|[Database.Backup](https://msdn.microsoft.com/library/microsoft.analysisservices.database.backup.aspx)|  
|[Cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|Executar uma consulta ou script no formato XMLA ou TSML (JSON).|<xref:Microsoft.AnalysisServices.Core.Server.Execute%2A>|  
|[Chamar ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)|Processar um banco de dados.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet ProcessCube](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|Processar um cubo.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessDimension](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|Processar uma dimensão.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessPartition](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|Processar uma partição.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessTable](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|Processe uma tabela em um modelo Tabular, o modelo de compatibilidade 1200 ou superior.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Merge-Partition](../../analysis-services/powershell/merge-partition-cmdlet.md)|Mesclar uma partição.|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[Cmdlet New-RestoreFolder](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|Criar uma pasta para conter um backup de banco de dados.|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[Cmdlet New-RestoreLocation](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|Especificar um ou mais servidores remotos nos quais o banco de dados deve ser restaurado.|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Cmdlet Remove-RoleMember](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|Remover um membro de uma função de banco de dados.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|Restaurar um banco de dados em uma instância de servidor.|<xref:Microsoft.AnalysisServices.Core.Server.Restore%2A>|  
  

  
  

