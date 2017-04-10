---
title: "ScaleR fun&#231;&#245;es para trabalhar com dados do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5f3c9864-9c75-4688-947d-0940045b2671
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# ScaleR fun&#231;&#245;es para trabalhar com dados do SQL Server
Este tópico fornece uma visão geral das principais funções de ScaleR para uso com o SQL Server, juntamente com comentários sobre a sua sintaxe.

Para obter uma lista completa das funções de ScaleR e como usá-los, consulte o [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/index#) referência na biblioteca MSDN. 

## Funções para trabalhar com fontes de dados do SQL Server
As funções a seguir permitem que você defina um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] fonte de dados. Um objeto de fonte de dados é um contêiner que especifica uma cadeia de conexão com o conjunto de dados que você deseja, definido como uma tabela, exibição ou consulta. Não há suporte para chamadas de procedimento armazenado.  

Além de definir uma fonte de dados, você pode executar instruções DDL de R, se você tiver as permissões necessárias na instância e banco de dados. 
+ [RxSqlServerData](https://msdn.microsoft.com/microsoft-r/scaler/RxSqlServerData) -definir uma [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] objeto fonte de dados
+ [rxSqlServerDropTable](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerDropTable) -soltar um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] tabela
+ [rxSqlServerTableExists](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerTableExists) -Verificar a existência de uma tabela de banco de dados ou objeto
+ [rxExecuteSQLDDL](https://msdn.microsoft.com/microsoft-r/scaler/rxExecuteSQLDDL) - Execute um comando para definir, manipular e controlar dados do SQL, mas não retornam dados  

## Funções para definir ou gerenciar um contexto de computação
As funções a seguir permitem que você defina um novo contexto de computação, alternar contextos de computação ou identificar o contexto atual de computação.
+ [RxComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/RxComputeContext) -criar um contexto de computação. 
+ [rxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxInSqlServer) -gerar um contexto de computação do SQL Server que permite **ScaleR** funções executadas no SQL Server R Services.
+ [rxGetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxGetComputeContext) -obter o contexto atual de computação. 
+ [rxSetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxSetComputeContext) -especificar qual calcular o contexto a ser usado. 

## Funções para usar uma fonte de dados
Depois de criar um objeto de fonte de dados, você pode abri-lo para obter dados ou gravação de novos dados. Dependendo do tamanho dos dados de origem, você também pode definir o tamanho do lote como parte da fonte de dados e mover dados em partes. 
+ [rxIsOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxIsOpen) -Verificar se uma fonte de dados está disponível
+ [rxOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxOpen) -Abrir uma fonte de dados para leitura
+ [rxReadNext](https://msdn.microsoft.com/microsoft-r/scaler/rxReadNext) -ler dados de uma fonte
+ [rxWriteNext](https://msdn.microsoft.com/microsoft-r/scaler/rxWriteNext) -gravar dados no destino
+ [rxClose](https://msdn.microsoft.com/microsoft-r/scaler/rxclose) -Fechar uma fonte de dados

Para obter mais informações sobre como trabalhar com essas funções ScaleR, que pode trabalhar com fontes de dados diferente de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], consulte [ Microsoft R Server - Introdução](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started).

## Funções que funcionam com arquivos de XDF
As funções a seguir podem ser usadas para criar um cache de dados local no formato XDF. Esse arquivo pode ser útil ao trabalhar com mais dados que podem ser transferidos do banco de dados em um lote ou mais dados que possam caber na memória.

Se você mover regularmente grandes quantidades de dados de um banco de dados para uma estação de trabalho local, em vez de consulta o banco de dados repetidamente para cada operação de R, você pode usar o arquivo XDF para salvar os dados localmente e trabalhar com ele no espaço de trabalho R, usando o arquivo XDF como o cache.

+ `rxImport` -Mover dados de uma fonte ODBC no arquivo XDF
+ `RxXdfData` -Criar um objeto de dados XDF
+ `RxDataStep` -Ler dados de int XDF um quadro de dados
+ `rxXdfToDataFrame` -Leia dados de XDF em um quadro de dados
+ `rxReadXdf` -Lê dados do XDF em um quadro de dados

Para obter um exemplo de como os arquivos XDF são usados, consulte este tutorial:  [dados ciência aprofundamento - usando as funções de ScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)

Para obter mais informações sobre essas funções ScaleR, que pode ser usado para transferir dados de várias fontes diferentes, consulte[ Microsoft R Server - Introdução](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started).

## Consulte também
[Comparação de Base de R e funções ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)
