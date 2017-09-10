---
title: "Determinar quais pacotes estão instalados no SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 90e7146bde123ca8ac8a8e6ff3e11d212fd4a35a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="determine-which-packages-are-installed-on-sql-server"></a>Determinar quais pacotes estão instalados no SQL Server
  Este tópico descreve como você pode determinar quais pacotes de R estão instalados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Por padrão, a instalação do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] cria uma biblioteca de pacote de R associada a cada instância. Portanto, para saber quais pacotes estão instalados em um computador, você deve executar essa consulta em cada instância separada em que o R Services está instalado. Observe que as bibliotecas de pacote **não** são compartilhados entre instâncias, portanto, é possível que diferentes pacotes estejam instalados em instâncias diferentes.

Para obter informações sobre como determinar o local da biblioteca padrão para uma instância, consulte [Instalar e gerenciar pacotes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).   
   
 
## <a name="get-a-list-of-installed-packages-using-r"></a>Obter uma lista de pacotes instalados usando o R  
 Há várias maneiras de se obter uma lista de pacotes instalados ou carregados, usando ferramentas de R e funções de R.  
  
+   Muitas ferramentas de desenvolvimento do R fornecem um pesquisador de objetos ou uma lista de pacotes instalados ou carregados no espaço de trabalho atual do R.  

+ Recomendamos as seguintes funções do pacote RevoScaleR, que são fornecidas especificamente para o gerenciamento de pacotes em contextos de computação:
  - [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)
  - [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)   
  
+   Você pode usar uma função do R, como `installed.packages()`, que está incluído no pacote do `utils` instalado. A função examina os arquivos DESCRIPTION de cada pacote encontrado na biblioteca especificada e retorna uma matriz de nomes de pacote, caminhos de biblioteca e números de versão.  
 
### <a name="examples"></a>Exemplos  
O exemplo a seguir usa a função `rxInstalledPackages` para obter uma lista de pacotes disponíveis no contexto de computação do SQL Server fornecido.

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 O exemplo a seguir usa a função de R base `installed.packages()` em um procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] para obter uma matriz de pacotes que foram instalados na biblioteca R_SERVICES da instância atual. Para evitar a análise dos campos no arquivo DESCRIPTION, somente o nome será retornado.  
  
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
  
 Para obter mais informações, consulte a descrição de campos padrão e campos opcionais para o arquivo DESCRIPTION do pacote de R, em [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).  
  
## <a name="see-also"></a>Consulte também  
 [Instalar pacotes de R adicionais no SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  

