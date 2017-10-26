---
title: Criar e implantar um banco de dados vazio (Analysis Services AMO-TOM) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: dcb916e9-97c5-47e0-922a-404891423b2a
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f8aafa733ba61563072e304cf77945203df7585d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-and-deploy-an-empty-database-analysis-services-amo-tom"></a>Criar e implantar um banco de dados vazio (Analysis Services AMO-TOM)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

Um cenário comum de programação para TOM AMO é gerar modelos em tempo real e bancos de dados. Este artigo orienta você pelas etapas de criação de um banco de dados. 

Para soluções tabulares, há uma correspondência entre um banco de dados e o modelo, com um modelo para cada banco de dados. Normalmente você pode especificar um ou outro, e o mecanismo deduzirá do objeto ausente. 

Criando e implantando um novo banco de dados são uma tarefa de três partes: 

* Criar uma instância de um **banco de dados** do objeto e defina suas propriedades, incluindo um nome. 

* Adicionar o **banco de dados** o objeto para um **Server.Databases** coleção. 

* Chamar o **atualização** método o **banco de dados** objeto salvá-lo para o **servidor**. 

## <a name="code-example-create-empty-database"></a>Exemplo de código: criar o banco de dados vazio 

```
using System; 
using Microsoft.AnalysisServices; 
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
                // Generate a new database name and use GetNewName 
                // to ensure the database name is unique. 
                // 
                string newDatabaseName = 
                    server.Databases.GetNewName("New Empty Database"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var blankDatabase = new Database() 
                { 
                    Name = newDatabaseName, 
                    ID = newDatabaseName, 
                    CompatibilityLevel = 1200, 
                    StorageEngineUsed = StorageEngineUsed.TabularMetadata, 
                }; 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(blankDatabase); 
                blankDatabase.Update(UpdateOptions.ExpandFull); 

                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(blankDatabase.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```

## <a name="next-steps"></a>Próximas etapas 

Quando um banco de dados é criado, você pode adicionar objetos de modelo: 

- [Adicionar uma fonte de dados para um modelo de tabela](../../analysis-services/tabular-model-programming-compatibility-level-1200/add-a-data-source-to-tabular-model-analysis-services-amo-tom.md)
- [Criar tabelas, partições e colunas em um modelo de tabela](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-tables-partitions-and-columns-in-a-tabular-model.md)
 

