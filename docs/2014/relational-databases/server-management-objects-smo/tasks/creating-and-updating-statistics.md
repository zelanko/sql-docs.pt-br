---
title: Criando e atualizando estatísticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- statistical information [SMO]
ms.assetid: 47a0a172-a969-4deb-bca9-dd04401a0fe1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54995cc99aae2065112cbb510203b656c409dcac
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782125"
---
# <a name="creating-and-updating-statistics"></a>Criando e atualizando estatísticas
  No SMO, as informações estatísticas sobre o processamento de consultas no banco de dados podem ser coletadas por meio do objeto <xref:Microsoft.SqlServer.Management.Smo.Statistic>.  
  
 É possível criar estatísticas para qualquer coluna através dos objetos <xref:Microsoft.SqlServer.Management.Smo.Statistic> e <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn>. O método <xref:Microsoft.SqlServer.Management.Smo.Statistic.Update%2A> pode ser executado para atualizar as estatísticas no objeto <xref:Microsoft.SqlServer.Management.Smo.Statistic>. Os resultados podem ser exibidos no Otimizador de Consulta.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic Smo no Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-and-update-statistics-in-visual-basic"></a>Criando e atualizando estatísticas no Visual Basic  
 Este exemplo de código cria uma nova tabela em um banco de dados existente para o qual os objetos <xref:Microsoft.SqlServer.Management.Smo.Statistic> e <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> são criados.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBStatistics1](SMO How to#SMO_VBStatistics1)]  -->  
  
## <a name="creating-and-update-statistics-in-visual-c"></a>Criando e atualizando estatísticas no Visual C#  
 Este exemplo de código cria uma nova tabela em um banco de dados existente para o qual os objetos <xref:Microsoft.SqlServer.Management.Smo.Statistic> e <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> são criados.  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Reference the CreditCard table.   
  
           Table tb = db.Tables["CreditCard", "Sales"];  
            //Define a Statistic object by supplying the parent table and name   
            //arguments in the constructor.   
            Statistic stat = default(Statistic);  
            stat = new Statistic(tb, "Test_Statistics");  
            //Define a StatisticColumn object variable for the CardType column   
            //and add to the Statistic object variable.   
            StatisticColumn statcol = default(StatisticColumn);  
            statcol = new StatisticColumn(stat, "CardType");  
            stat.StatisticColumns.Add(statcol);  
            //Create the statistic counter on the instance of SQL Server.   
            stat.Create();  
        }  
```  
  
## <a name="creating-and-update-statistics-in-powershell"></a>Criando e atualizando estatísticas no PowerShell  
 Este exemplo de código cria uma nova tabela em um banco de dados existente para o qual os objetos <xref:Microsoft.SqlServer.Management.Smo.Statistic> e <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> são criados.  
  
```powershell
# Example of implementing a full text search on the default instance.  
# Set the path context to the local, default instance of SQL Server and database tables  
  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
CD AdventureWorks2012\tables  
  
#Get a reference to the table  
$tb = get-item Production.ProductCategory  
  
# Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
  
$ftc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextCatalog -argumentlist $db, "Test_Catalog2"  
$ftc.IsDefault = $true  
  
# Create the Full Text Search catalog on the instance of SQL Server.  
$ftc.Create()  
  
# Define a FullTextIndex object variable by supplying the parent table argument in the constructor.  
$fti = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndex -argumentlist $tb  
  
#  Define a FullTextIndexColumn object variable by supplying the parent index   
#  and column name arguments in the constructor.  
  
$ftic = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndexColumn -argumentlist $fti, "Name"  
  
# Add the indexed column to the index.  
$fti.IndexedColumns.Add($ftic)  
  
# Set change tracking  
$fti.ChangeTracking = [Microsoft.SqlServer.Management.SMO.ChangeTracking]::Automatic  
  
# Specify the unique index on the table that is required by the Full Text Search index.  
$fti.UniqueIndexName = "AK_ProductCategory_Name"  
  
# Specify the catalog associated with the index.  
$fti.CatalogName = "Test_Catalog2"  
  
# Create the Full Text Search Index  
$fti.Create()  
```  
