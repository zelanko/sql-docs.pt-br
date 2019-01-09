---
title: Ferramentas e aplicativos usados no Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8d3ecb5de4c70c09bc367b9008f5d62c6a23faef
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210058"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Ferramentas e aplicativos usados no Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  Encontre as ferramentas e aplicativos que você precisa para a criação de modelos do Analysis Services e gerenciamento de bancos de dados implantados.  
  
## <a name="analysis-services-model-designers"></a>Designers de modelos do Analysis Services  
 Modelos são criados usando modelos de projeto no SSDT SQL Server Data Tools (), um shell do Visual Studio. Modelos de projeto fornecem designers de modelo para criar os objetos de modelo de dados que compõem uma solução do Analysis Services. O SSDT é um download gratuito da web atualizado mensalmente.

 **[Baixar o SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)** 
  
 Os modelos têm uma configuração de nível de compatibilidade que determina a disponibilidade do recursos e em qual versão do Analysis Services executar o modelo.  Se você especificar que um determinado nível de compatibilidade é determinada em parte pelo designer de modelo.  
  
 Modelos de tabela usando a funcionalidade mais recente, como arquivos BIM no formato JSON tabular e bidirecionais filtragem cruzam, devem ser criados ou atualizados no nível de compatibilidade 1200 ou superior.  
  
 Se você precisar de um nível de compatibilidade mais baixo, talvez porque você deseja implantar um modelo em uma versão anterior do Analysis Services, você pode usar o designer de modelo no SSDT. Versões mais recentes da ferramenta de suportam a criação de qualquer tipo de modelo (tabular ou multidimensional), em qualquer nível de compatibilidade.   

## <a name="administrative-tools"></a>Ferramentas administrativas  
  
 SQL Server Management Studio (SSMS) é a principal ferramenta de administração para todos os recursos do SQL Server, inclusive o Analysis Services. O SSMS é um download gratuito da web atualizado mensalmente. 
  
**[Baixar o SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)** 
  
 SSMS inclui eventos estendidos (xEvents), fornecendo uma alternativa leve para rastreamentos do SQL Server Profiler usado para atividade de monitoramento e diagnosticar problemas no SQL Server 2016 e servidores do Azure Analysis Services. Consulte [Monitorar o Analysis Services com Eventos Estendidos do SQL Server](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) .  
  
### <a name="sql-server-profiler"></a>SQL Server Profiler  
 Embora oficialmente preterido em favor do xEvents, o SQL Server Profiler fornece uma abordagem familiar para conexões de monitoramento, execução da consulta MDX, e outras operações do servidor. O SQL Server Profiler é instalado por padrão. Você pode achar com aplicativos do SQL Server nos aplicativos no Windows.  
  
### <a name="powershell"></a>PowerShell  
 Você pode usar os comandos do PowerShell para realizar muitas tarefas administrativas. Ver [referência do PowerShell](../analysis-services/powershell/analysis-services-powershell-reference.md) para obter mais informações.  
  
### <a name="community-and-third-party-tools"></a>Ferramentas da comunidade e de terceiros  
 Verifique a [página de codeplex do Analysis Services](http://sqlsrvanalysissrvcs.codeplex.com/) para ver exemplos de código da comunidade. Os[fóruns](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) podem ser úteis ao buscar recomendações de ferramentas de terceiros com suporte para o Analysis Services.  
  
## <a name="see-also"></a>Consulte também  
 [Nível de compatibilidade de um banco de dados Multidimensional](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Nível de compatibilidade para modelos de tabela](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
