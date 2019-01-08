---
title: Aviso sobre uso de lado do cliente de GEOMETRY, GEOGRAPHY e HIERARCHYID | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 500ee6b3-2154-45d2-a3cf-8760166d9413
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d9ee14c39f7fee577065de934f839f9d6c88e630
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52413763"
---
# <a name="warning-about-client-side-usage-of-geometry-geography-and-hierarchyid"></a>Aviso sobre uso no lado do cliente de GEOMETRY, GEOGRAPHY e HIERARCHYID
  O assembly **Types**, que contém os tipos de dados espaciais foi atualizado da versão 10.0 para a versão 11.0. Aplicativos personalizados que referenciam esse assembly poderão falhar quando certas condições forem verdadeiras.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 O assembly **Types**, que contém os tipos de dados espaciais foi atualizado da versão 10.0 para a versão 11.0. Aplicativos personalizados que referenciam esse assembly poderão falhar quando as condições a seguir forem verdadeiras.  
  
-   Quando você move um aplicativo personalizado de um computador no qual [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] tiver sido instalado em um computador no qual apenas [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] é instalado, o aplicativo falhará porque a versão referenciada 10.0 do **SqlTypes** assembly não está presente. Você verá esta mensagem de erro: `"Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified."`  
  
-   Quando você faz referência a **SqlTypes** assembly versão 11.0 e a versão 10.0 também estiver instalada, você poderá ver esta mensagem de erro: `"System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'."`  
  
-   Quando você faz referência a **SqlTypes** assembly versão 11.0 de um aplicativo personalizado que tem como alvo o .NET 3.5, 4 ou 4.5, o aplicativo falhará porque o SqlClient por design carrega a versão 10.0 do assembly. Essa falha ocorre quando o aplicativo chama um dos seguintes métodos:  
  
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
  
  
