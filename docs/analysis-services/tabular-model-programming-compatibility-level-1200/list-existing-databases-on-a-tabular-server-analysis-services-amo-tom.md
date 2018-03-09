---
title: Lista de bancos de dados existentes em um servidor de tabela (Analysis Services AMO-TOM) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ab5eb4b8-6254-442d-a42e-2372c346d260
caps.latest.revision: "2"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3864da736ccdeca7ffa9d6c024748e5cd60b7a5a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="list-existing-databases-on-a-tabular-server-analysis-services-amo-tom"></a>Lista de bancos de dados existentes em um servidor de tabela (Analysis Services AMO-TOM)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Quando você tiver um **servidor** do objeto que é conectado a uma instância do Analysis Services, você pode iterar **Server.Databases** coleção para listar todos os bancos de dados hospedados pela instância de serviços de análise. 

O **Server.Databases** coleção contém um **banco de dados** objeto para cada banco de dados hospedado no servidor, independentemente do modo de servidor (Multidimensional ou Tabular) ou o tipo de banco de dados (Multidimensional, Pré-1200 tabular, ou Tabular 1200 e superior). 

Você pode verificar o tipo de banco de dados por meio de **Database.StorageEngineUsed** propriedade.  

Bancos de dados 1200 e maior tabulares retornará não null **Database.Model** propriedade que fornece acesso a todos os objetos de metadados de tabela: tabelas, colunas, relações e assim por diante.  

Multidimensional ou de tabela 1103 e abaixo de Database.Model propriedade será nula. Nesse caso, os metadados de tabela-não estarão disponíveis em Propriedades multidimensionais (como Database.Cubes e Database.Dimensions), mas essas propriedades só são expostas pela classe Microsoft.AnalysisServices.Database (de AMO), não por Microsoft.AnalysisServices.Tabular.Database (para TOM). Para obter mais informações sobre qual classe de banco de dados para usar, consulte [instalar, distribuir e fazer referência a biblioteca de cliente de TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md).

A menos que Database.StorageEngineUsed é definido para TabularMetadata, você não poderá usar outras classes no namespace Tabular para acessar ou manipular a árvore de modelo. 

A tabela a seguir resume os comportamentos esperados quando você se conectar a um servidor ou banco de dados usando uma classe AnalysisServices em um servidor ou banco de dados. 

mode | Database.Model | Database.StorageEngineUsed
-----|----------------|---------------------------
Tabela 1200, 1400 | Retorna o nome do modelo| StorageEngineUsed.TabularMetadata 
Tabela 1103, 1050, 1100 | Retorna nulo | StorageEngineUsed.InMemory 
Multidimensional | Retorna nulo | StorageEngineUsed.Traditional 

## <a name="code-example-list-existing-databases"></a>Exemplo de código: lista de bancos de dados existentes

O código a seguir ilustra como se conectar ao servidor e a lista de bancos de dados hospedados pelo servidor. 

```
using System; using Microsoft.AnalysisServices; 
using Microsoft.AnalysisServices.Tabular; 

 
namespace TOMSamples 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
            // 
            // Connect to the local default instance of Analysis Services 
            // 
            string ConnectionString = "DataSource=localhost"; 

             // 
            // The using syntax ensures the correct use of the 
            // Microsoft.AnalysisServices.Tabular.Server object. 
            // 
            using (Server server = new Server()) 
            { 
                server.Connect(ConnectionString); 

                 // 
                // List common properties for the databases on the server. 
                // 
                foreach (Database db in server.Databases) 
                { 
                    Console.WriteLine("Properties for database {0}:", db.Name); 
                    Console.ForegroundColor = ConsoleColor.Yellow; 
                    Console.WriteLine("Database ID:\t\t\t{0}", db.ID); 
                    Console.WriteLine("Database compatibility level:\t{0}", db.CompatibilityLevel); 
                    Console.WriteLine("Database collation:\t\t{0}", db.Collation); 
                    Console.WriteLine("Database created timestamp:\t{0}", db.CreatedTimestamp); 
                    Console.WriteLine("Database language ID:\t\t{0}", db.Language); 
                    Console.WriteLine("Database model type:\t\t{0}", db.ModelType); 
                    Console.WriteLine("Database state:\t\t\t{0}", db.State); 
                    Console.ResetColor(); 
                    Console.WriteLine(); 
                } 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```


## <a name="get-an-item-from-a-database"></a>Obter um item de um banco de dados 

O trecho de código a seguir mostra como obter uma tabela ou coluna de banco de dados. 


```
var db = srv.Databases.GetByName("abc"); 

Column c1 = db.Model.Tables["foo"].Columns["bar"]; 
if (c1.ObjectType == ObjectType.Column) // always true 

MetadataObject obj; 

switch(obj.ObjectType) 
{ 
 case ObjectType.Table: 
  var t1 = (Table)obj; 
  break; 
} 
```

## <a name="next-steps"></a>Próximas etapas

Entender como [criar e implantar um banco de dados vazio](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md) usando a API de TOM.

