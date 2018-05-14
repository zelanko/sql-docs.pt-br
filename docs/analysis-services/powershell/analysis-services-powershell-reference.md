---
title: Referência do PowerShell do Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9632b9aaecfc6f6fa86684ac604706ecaac90071
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="analysis-services-powershell-reference"></a>Referência do Analysis Services PowerShell
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cmdlets do PowerShell são incluídos no [módulo do SqlServer](https://www.powershellgallery.com/packages/SqlServer/21.0.17099). 
  
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
|[Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)|Processar um banco de dados.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessCube](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|Processar um cubo.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessDimension](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|Processar uma dimensão.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessPartition](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|Processar uma partição.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessTable](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|Processe uma tabela em um modelo Tabular, o modelo de compatibilidade 1200 ou superior.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Merge-Partition](../../analysis-services/powershell/merge-partition-cmdlet.md)|Mesclar uma partição.|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[Cmdlet New-RestoreFolder](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|Criar uma pasta para conter um backup de banco de dados.|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[Cmdlet New-RestoreLocation](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|Especificar um ou mais servidores remotos nos quais o banco de dados deve ser restaurado.|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Cmdlet Remove-RoleMember](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|Remover um membro de uma função de banco de dados.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|Restaurar um banco de dados em uma instância de servidor.|<xref:Microsoft.AnalysisServices.Core.Server.Restore%2A>|  
  

  
  
