---
title: Aviso sobre o uso do lado do cliente de GEOMETRY, geography e HIERARCHYid | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 500ee6b3-2154-45d2-a3cf-8760166d9413
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 524400e9c9420fb54447220215d4660874ec6d69
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091084"
---
# <a name="warning-about-client-side-usage-of-geometry-geography-and-hierarchyid"></a>Aviso sobre uso no lado do cliente de GEOMETRY, GEOGRAPHY e HIERARCHYID
  O assembly **Microsoft. SqlServer. Types. dll**, que contém os tipos de dados espaciais, foi atualizado da versão 10,0 para a versão 11,0. Aplicativos personalizados que referenciam esse assembly poderão falhar quando certas condições forem verdadeiras.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 O assembly **Microsoft. SqlServer. Types. dll**, que contém os tipos de dados espaciais, foi atualizado da versão 10,0 para a versão 11,0. Aplicativos personalizados que referenciam esse assembly poderão falhar quando as condições a seguir forem verdadeiras.  
  
-   Quando você move um aplicativo personalizado de um computador no qual [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o foi instalado em um computador no qual [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o só está instalado, o aplicativo falhará porque a versão referenciada 10,0 do assembly **SqlTypes** não está presente. Talvez você receba esta mensagem de erro: `"Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified."`  
  
-   Quando você faz referência à versão 11,0 do assembly **SqlTypes** e a versão 10,0 também está instalada, essa mensagem de erro pode ser exibida:`"System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'."`  
  
-   Quando você faz referência à versão 11,0 do assembly **SqlTypes** de um aplicativo personalizado que tem como alvo o .net 3,5, 4 ou 4,5, o aplicativo falhará, pois o SqlClient por Design carrega a versão 10,0 do assembly. Essa falha ocorre quando o aplicativo chama um dos seguintes métodos:  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md
)  
  
  
