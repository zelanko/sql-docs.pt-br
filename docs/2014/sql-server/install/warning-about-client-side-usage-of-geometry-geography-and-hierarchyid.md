---
title: Aviso sobre o uso do lado do cliente de GEOMETRY, GEOGRAPHY e HIERARCHYID | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 500ee6b3-2154-45d2-a3cf-8760166d9413
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 02748f9dca8e4f9f29c7c94658d2a4068b1ba65e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121626"
---
# <a name="warning-about-client-side-usage-of-geometry-geography-and-hierarchyid"></a>Aviso sobre uso no lado do cliente de GEOMETRY, GEOGRAPHY e HIERARCHYID
  O assembly **Microsoft.SqlServer.Types.dll**, que contém os tipos de dados espaciais foi atualizado da versão 10.0 para a versão 11.0. Aplicativos personalizados que referenciam esse assembly poderão falhar quando certas condições forem verdadeiras.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 O assembly **Microsoft.SqlServer.Types.dll**, que contém os tipos de dados espaciais foi atualizado da versão 10.0 para a versão 11.0. Aplicativos personalizados que referenciam esse assembly poderão falhar quando as condições a seguir forem verdadeiras.  
  
-   Quando você move um aplicativo personalizado em um computador no qual [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] foi instalado em um computador no qual apenas [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] é instalado, o aplicativo falhará porque a versão referenciada 10.0 do **SqlTypes** assembly não está presente. Talvez você receba esta mensagem de erro: `“Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified.”`  
  
-   Quando você faz referência a **SqlTypes** assembly versão 11.0 e a versão 10.0 também estiver instalada, você verá essa mensagem de erro: `“System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'.”`  
  
-   Quando você faz referência a **SqlTypes** assembly versão 11.0 de um aplicativo personalizado que tem como alvo o .NET 3.5, 4 ou 4.5, o aplicativo falhará porque a versão 10.0 do assembly é carregado SqlClient por design. Essa falha ocorre quando o aplicativo chama um dos seguintes métodos:  
  
    -   O método `GetValue` da classe `SqlDataReader`  
  
    -   O método `GetValues` da classe `SqlDataReader`  
  
    -   operador de índice de colchete [] da classe `SqlDataReader`  
  
    -   O método `ExecuteScalar` da classe `SqlCommand`  
  
## <a name="corrective-action"></a>Ação corretiva  
 Você pode contornar esse problema usando um dos seguintes métodos:  
  
-   Você pode contornar esse problema no seu código chamando o método `GetSqlBytes`, em vez dos métodos Get listados acima, para recuperar tipos de sistema CLR do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], conforme mostrado no exemplo a seguir:  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   Você pode contornar esse problema usando redirecionamento de assembly no arquivo de configuração de aplicativo, conforme mostrado no seguinte exemplo:  
  
    ```xml  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    ```  
  
-   Você pode contornar esse problema na sua cadeia de conexão especificando um valor "SQL Server 2012" para o atributo "Type System Version" para forçar o SqlClient a carregar a versão 11.0 do assembly. Esse atributo de cadeia de conexão está disponível apenas no .NET 4.5 e versões superiores.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
