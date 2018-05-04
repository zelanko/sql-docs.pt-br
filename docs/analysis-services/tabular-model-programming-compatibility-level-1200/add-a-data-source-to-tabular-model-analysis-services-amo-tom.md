---
title: Adicionar uma fonte de dados ao modelo de tabela (Analysis Services AMO-TOM) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e54a8a1b-b964-4b6e-9057-44d50af676c0
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3892601961f95b0d4dd4f0de0d3767eff01186d1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="add-a-data-source-to-tabular-model-analysis-services-amo-tom"></a>Adicionar uma fonte de dados ao modelo de tabela (Analysis Services AMO-TOM)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
O **DataSource** classe no namespace AnalysisServices é uma abstração de um modelo de tabela fonte de dados que especifica o tipo e o local dos dados importados durante uma operação de atualização de dados. 

Você pode adicionar uma fonte de dados para o modelo de tabela ao instanciar um objeto de uma classe derivada de **DataSource**e, em seguida, adicioná-lo para o **fontes de dados** coleção do objeto de modelo. Para confirmar as alterações para o servidor, chame **Model.SaveChanges()** ou **Database.Update(UpdateOptions.ExpandFull)**. 

No SQL Server 2016, o Analysis Services oferece suporte à importação de dados somente de bancos de dados relacionais, em que o provedor de dados expõe dados em forma de tabelas e colunas. Como tal, o modelo de objeto de tabela usa a classe de ProviderDataSource (derivada da fonte de dados) para expor esse recurso. 

## <a name="code-example-add-a-data-source"></a>Exemplo de código: adicionar uma fonte de dados 

Este exemplo demonstram como criar uma instância de um **ProviderDataSource** e adicioná-lo para um modelo de dados. 

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
                    server.Databases.GetNewName("Database with a Data Source Definition"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var dbWithDataSource = new Database() 
                { 
                    Name = newDatabaseName, 
                    ID = newDatabaseName, 
                    CompatibilityLevel = 1200, 
                    StorageEngineUsed = StorageEngineUsed.TabularMetadata, 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.Model object to the 
                // database, which acts as a root for all other Tabular metadata objects. 
                // 
                dbWithDataSource.Model = new Model() 
                { 
                    Name = "Tabular Data Model", 
                    Description = "A Tabular data model at the 1200 compatibility level." 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.ProviderDataSource object 
                // to the data Model object created in the previous step. The connection 
                // string of the data source object in this example  
                // points to an instance of the AdventureWorks2014 SQL Server database. 
                // 
                dbWithDataSource.Model.DataSources.Add(new ProviderDataSource() 
                { 
                    Name = "SQL Server Data Source Example", 
                    Description = "A data source definition that uses explicit Windows credentials for authentication against SQL Server.", 
                    ConnectionString = "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureWorks2014;Integrated Security=SSPI;Persist Security Info=false", 
                    ImpersonationMode = Microsoft.AnalysisServices.Tabular.ImpersonationMode.ImpersonateAccount, 
                    Account = @".\Administrator", 
                    Password = "P@ssw0rd", 
                }); 
 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(dbWithDataSource); 
                dbWithDataSource.Update(UpdateOptions.ExpandFull); 
 
                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(dbWithDataSource.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
                Console.WriteLine("The data model includes the following data source definitions:"); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                foreach (DataSource ds in dbWithDataSource.Model.DataSources) 
                { 
                    Console.WriteLine("\tData source name:\t\t{0}", ds.Name); 
                    Console.WriteLine("\tData source description:\t{0}", ds.Description); 
                } 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```

## <a name="next-step"></a>Próxima etapa 

Em um modelo, você precisará configurar associações de dados que mapeiam colunas de origem na fonte de dados para colunas de destino no modelo. Você também precisará definir as partições, no mínimo uma por tabela, que armazenam os dados. O link a seguir mostra como: [criar tabelas, partições e colunas](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-tables-partitions-and-columns-in-a-tabular-model.md) 
