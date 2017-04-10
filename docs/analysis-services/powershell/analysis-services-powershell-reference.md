---
title: "Refer&#234;ncia do Analysis Services PowerShell | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 6c435e40-bfaf-4073-8cef-bc3260602246
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Refer&#234;ncia do Analysis Services PowerShell
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inclui um provedor do PowerShell (SQLAS) e cmdlets (SQLASCMDLETS) para que você possa usar o Windows PowerShell para navegar, administrar e consultar objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações sobre como carregar e usar o provedor e os cmdlets, consulte [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md). Para ver um exemplo de como usar os tipos de AMO no PowerShell para criar um Banco de dados de tabela, veja [AMO PowerShell Example](../../analysis-services/powershell/amo-powershell-example.md).  
  
##  <a name="bkmk_cmdlets"></a> Cmdlets do Analysis Services  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece cmdlets correspondem aos métodos no **Microsoft. AnalysisServices** namespace. A tabela a seguir descreve cada cmdlet e fornece um link para o método AMO correspondente.  
  
 Se você quiser usar o PowerShell para executar uma tarefa que não esteja representada na lista a seguir (por exemplo, para criar ou sincronizar um banco de dados), escreva um script TMSL ou XMLA para essa ação e execute-o usando o cmdlet **Invoke-ASCmd**.  
  
|Cmdlet|Description|Métodos equivalentes do AMO|  
|------------|-----------------|----------------------------|  
|[Cmdlet Add-RoleMember](../../analysis-services/powershell/add-rolemember-cmdlet.md)|Adicionar um membro a uma função de banco de dados.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Cmdlet Backup-ASDatabase](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)|Fazer backup de um banco de dados do Analysis Services.|<xref:Microsoft.AnalysisServices.Database.Backup%2A>|  
|[Cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|Executar uma consulta ou script no formato XMLA ou TSML (JSON).|<xref:Microsoft.AnalysisServices.Server.Execute%2A>|  
|[Chamar ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)|Processar um banco de dados.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet ProcessCube](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|Processar um cubo.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessDimension](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|Processar uma dimensão.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessPartition](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|Processar uma partição.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessTable](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|Processar uma tabela em um modelo de tabela, no modelo de compatibilidade 1200 ou posterior.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Merge-Partition](../../analysis-services/powershell/merge-partition-cmdlet.md)|Mesclar uma partição.|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[Cmdlet New-RestoreFolder](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|Criar uma pasta para conter um backup de banco de dados.|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[Cmdlet New-RestoreLocation](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|Especificar um ou mais servidores remotos nos quais o banco de dados deve ser restaurado.|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Cmdlet Remove-RoleMember](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|Remover um membro de uma função de banco de dados.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|Restaurar um banco de dados em uma instância de servidor.|<xref:Microsoft.AnalysisServices.Server.Restore%2A>|  
  
## Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Linguagem de script do Analysis Services &#40;ASSL para XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)  
  
  