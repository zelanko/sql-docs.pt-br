---
title: "Determinar quais pacotes est&#227;o instalados no SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Determinar quais pacotes est&#227;o instalados no SQL Server
  Este tópico descreve como você pode determinar quais pacotes R instalados na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.  
  
Por padrão, a instalação do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] cria uma biblioteca de pacote R associada a cada instância. Portanto, para saber quais pacotes estão instalados em um computador, você deve executar essa consulta em cada instância separada onde R Services está instalado. Observe que as bibliotecas de pacote são **não** compartilhados entre instâncias, assim é possível que diferentes pacotes a serem instalados em instâncias diferentes.

Para obter informações sobre como determinar o local da biblioteca padrão para uma instância, consulte [Instalando e Gerenciando pacotes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).   
   
 
## Obter uma lista de pacotes instalados usando R  
 Há várias maneiras de obter uma lista de pacotes instalados ou carregados usando ferramentas de R e funções de R.  
  
+   Muitas ferramentas de desenvolvimento do R fornecem um pesquisador de objetos ou uma lista de pacotes instalados ou carregados no espaço de trabalho atual do R.  

+ Recomendamos as seguintes funções do pacote RevoScaleR que são fornecidas especificamente para gerenciamento de pacotes em contextos de computação:
  - [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/rxfindpackage)
  - [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/rxInstalledPackages)   
  
+   Você pode usar uma função do R, como `installed.packages()`, que está incluído no pacote do `utils` instalado. A função verifica os arquivos de descrição de cada pacote que foi encontrado na biblioteca especificada e retorna uma matriz de nomes de pacote, caminhos de biblioteca e os números de versão.  
 
### Exemplos  
O exemplo a seguir usa a função `rxInstalledPackages` para obter uma lista de pacotes disponíveis no contexto fornecido de computação do SQL Server.

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 O exemplo a seguir usa a função R base `installed.packages()` em uma [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimento armazenado para obter uma matriz de pacotes que foram instalados na biblioteca R_SERVICES para a instância atual. Para evitar a análise dos campos no arquivo DESCRIPTION, somente o nome será retornado.  
  
```  
EXECUTE sp_execute_external_script  
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```  
  
 Para obter mais informações sobre o padrão e os campos opcionais no arquivo de descrição do pacote R, consulte [https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file](https://cran.r-project.org/doc/manuals/R-exts.html).  
  
## Consulte também  
 [Instalar pacotes R adicionais no SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  