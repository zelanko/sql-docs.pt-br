---
title: "Criar tabelas, partições e colunas em um modelo Tabular | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: cf0e4791-ad3b-41a8-81ce-509d4cf223f8
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 94bad422a63276ad130027ea77de4734571016a8
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="create-tables-partitions-and-columns-in-a-tabular-model"></a>Criar tabelas, partições e colunas em um modelo de tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Em um modelo de tabela, uma tabela consiste em linhas e colunas. Linhas são organizadas em partições para dar suporte à atualização de dados incrementais. Uma solução Tabular pode dar suporte a vários tipos de tabelas, dependendo de onde os dados são provenientes de:  

* Tabelas regulares, onde os dados são originados de uma fonte de dados relacional, por meio do provedor de dados. 

* Tabelas enviadas por push, onde dados são "enviados" para a tabela programaticamente. 

* Tabelas calculadas, onde os dados vêm de uma expressão DAX que faz referência a outro objeto dentro do modelo para seus dados.  

No exemplo de código abaixo, vamos definir uma tabela normal. 

## <a name="required-elements"></a>Elementos necessários 

Uma tabela deve ter pelo menos uma partição. Uma tabela normal também deve ter pelo menos uma coluna definida. 

Cada partição deve ter uma fonte especificando a origem dos dados, mas a origem pode ser definida como null. Normalmente, a fonte é uma expressão de consulta que define uma fatia de dados na linguagem de consulta de banco de dados relevante. 

## <a name="code-example-create-a-table-column-parition"></a>Exemplo de código: criar uma tabela, coluna, partição

Tabelas são representadas pela classe de tabela (no namespace AnalysisServices). 

No exemplo a seguir, vamos definir uma tabela normal ter uma partição vinculada a uma fonte de dados relacional e algumas colunas normais. Podemos também enviar as alterações para o servidor e disparar uma atualização de dados que coloca os dados no modelo. Isso representa o cenário mais comum quando você deseja carregar dados de um banco de dados relacional do SQL Server para uma solução de tabela. 


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
                    server.Databases.GetNewName("Database with a Table Definition"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var dbWithTable = new Database() 
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
                dbWithTable.Model = new Model() 
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
                string dataSourceName = "SQL Server Data Source Example"; 
                dbWithTable.Model.DataSources.Add(new ProviderDataSource() 
                { 
                    Name = dataSourceName, 
                    Description = "A data source definition that uses explicit Windows credentials for authentication against SQL Server.", 
                    ConnectionString = "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureWorks2014;Integrated Security=SSPI;Persist Security Info=false", 
                    ImpersonationMode = Microsoft.AnalysisServices.Tabular.ImpersonationMode.ImpersonateAccount, 
                    Account = @".\Administrator", 
                    Password = "P@ssw0rd", 
                }); 
 
                //  
                // Add a table called Individual Customers to the data model 
                // with a partition that points to a [Sales].[vIndividualCustomer] view 
                // in the underlying data source. 
                // 
                dbWithTable.Model.Tables.Add(new Table() 
                { 
                    Name = dbWithTable.Model.Tables.GetNewName("Individual Customers"), 
                    Description = "Individual customers (names and email addresses) that purchase Adventure Works Cycles products online.", 
                    Partitions = { 
                        // 
                        // Create a single partition with a QueryPartitionSource for a query 
                        // that imports all customer rows from the underlying data source. 
                        // 
                        new Partition() { 
                            Name = "All Customers", 
                            Source = new QueryPartitionSource() { 
                                DataSource = dbWithTable.Model.DataSources[dataSourceName], 
                                Query = @"SELECT   [FirstName] 
                                                    ,[MiddleName] 
                                                    ,[LastName] 
                                                    ,[PhoneNumber]  
                                                    ,[EmailAddress] 
                                                    ,[City] 
                                        FROM [Sales].[vIndividualCustomer]", 
                            } 
                        } 
                    }, 
                    Columns = 
                    { 
                        // 
                       // DataColumn objects refer to regular table columns.  
                        // Each DataColumn object corresponds to a column in the underlying data source query. 
                        // 
                        new DataColumn() { 
                            Name = "FirstName", 
                            DataType = DataType.String, 
                            SourceColumn = "FirstName", 
                        }, 
                        new DataColumn() { 
                            Name = "MiddleName", 
                            DataType = DataType.String, 
                            SourceColumn = "MiddleName", 
                        }, 
                        new DataColumn() { 
                            Name = "LastName", 
                            DataType = DataType.String, 
                            SourceColumn = "LastName", 
                        }, 
                        new DataColumn() { 
                            Name = "PhoneNumber", 
                            DataType = DataType.String, 
                            SourceColumn = "PhoneNumber", 
                        }, 
                        new DataColumn() { 
                            Name = "EmailAddress", 
                            DataType = DataType.String, 
                            SourceColumn = "EmailAddress", 
                        }, 
                        new DataColumn() { 
                            Name = "City", 
                            DataType = DataType.String, 
                            SourceColumn = "City", 
                        }, 
                    } 
                }); 
 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(dbWithTable); 
 
                //  
                // Request a full refresh to import the data from the data source and 
                // and perform any necessary recalculations. 
                // The refresh operation will be performed with the next 
                // invocation of Model.SaveChanges() or Database.Update(UpdateOptions.ExpandFull). 
                dbWithTable.Model.RequestRefresh(Microsoft.AnalysisServices.Tabular.RefreshType.Full); 
                dbWithTable.Update(UpdateOptions.ExpandFull); 
 
 
                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(dbWithTable.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
 
                Console.WriteLine("The data model includes the following table definitions:"); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                foreach (Table tbl in dbWithTable.Model.Tables) 
                { 
                    Console.WriteLine("\tTable name:\t\t{0}", tbl.Name); 
                    Console.WriteLine("\ttbl description:\t{0}", tbl.Description); 
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

## <a name="partitions-in-a-table"></a>Partições em uma tabela 

Partições são representadas por um **partição** classe (no namespace AnalysisServices). O **partição** classe expõe um **fonte** propriedade de P**artitionSource** de tipo, que fornece uma abstração sobre as diferentes abordagens para a ingestão de dados partição. Um **partição** instância pode ter um **fonte** push de propriedade como nula, que indica que dados sejam enviados para a partição enviando blocos de dados para o servidor como parte da API de dados exposto pelo Analysis Services . No SQL Server 2016, **PartitionSource** classe tem duas classes derivadas que representam formas para associar dados a uma partição: **QueryPartitionSource** e **CalculatedPartitionSource**. 

## <a name="columns-in-a-table"></a>Colunas em uma tabela 

Colunas são representadas por várias classes derivadas de base **coluna** classe (no namespace AnalysisServices): 

* **DataColumn** (para regulares colunas em tabelas regulares)
* **CalculatedColumn** (para colunas com o apoio de expressão DAX)
* **CalculatedTableColumn** (para regulares colunas em tabelas calculadas)
* **RowNumberColumn** (um tipo especial de coluna criada pelo SSAS para cada tabela). 

## <a name="row-numbers-in-a-table"></a>Números de linha em uma tabela 

Cada **tabela** objeto em um servidor tem um **RowNumberColumn** usado para fins de indexação. Você não pode criar ou adicioná-lo explicitamente. A coluna é criada automaticamente quando você salva ou atualizar o objeto: 

* **banco de dados. SaveChanges** 

* **banco de dados. Update(ExpandFull)** 

Ao chamar o método, o servidor criará coluna de número da linha automaticamente, que ficará visível como **RowNumberColumn** coleção de colunas da tabela. 

## <a name="calculated-tables"></a>Tabelas calculadas 

Tabelas calculadas são originadas de uma expressão DAX que repurposes dados de estruturas de dados existentes no modelo ou de associações fora de linha. Para criar uma tabela calculada por meio de programação, faça o seguinte: 

* Criar um genérico **tabela**. 

* Adicionar uma partição a ele com o tipo de origem **CalculatedPartitionSource**, onde a fonte é uma expressão DAX. Origem da partição é o que diferencia uma tabela normal de uma tabela calculada. 

Quando você salvar as alterações para o servidor, o servidor retornará a lista inferida de **CalculatedTableColumns** (calculado tabelas são compostas de colunas de tabela calculada), visíveis por meio da coleção de colunas da tabela. 

## <a name="next-steps"></a>Próximas etapas

Revise as classes usadas para tratamento de exceções em TOM: [manipulação de erros em TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/handling-errors-in-the-tom-api-analysis-services-amo-tom.md)
  
