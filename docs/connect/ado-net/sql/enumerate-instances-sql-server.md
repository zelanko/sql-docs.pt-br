---
title: Enumerando instâncias do SQL Server (ADO.NET)
description: Descreve como enumerar instâncias ativas do SQL Server.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ddf1c83c-9d40-45e6-b04d-9828c6cbbfdc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d6c83ffd407a9b27a04b254fb3e9e5673a600417
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452206"
---
# <a name="enumerating-instances-of-sql-server-adonet"></a>Enumerando instâncias do SQL Server (ADO.NET)

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server permite que os aplicativos encontrem SQL Server instâncias na rede atual. A classe <xref:System.Data.Sql.SqlDataSourceEnumerator> expõe essas informações ao desenvolvedor do aplicativo, fornecendo uma <xref:System.Data.DataTable> que contém informações sobre todos os servidores visíveis. Esta tabela retornada contém uma lista de instâncias de servidor disponíveis na rede que corresponde à lista fornecida quando um usuário tenta criar uma nova conexão, e expande a lista suspensa que contém todos os servidores disponíveis na caixa de diálogo **Propriedades da Conexão**. Os resultados exibidos nem sempre estão completos.  
  
> [!NOTE]
>  Assim como na maioria dos serviços do Windows, é melhor executar o serviço de SQL Browser com o mínimo possível de privilégios. Confira os Manuais Online do SQL Server para obter mais informações sobre o serviço do navegador do SQL e sobre como gerenciar seu comportamento.  
  
## <a name="retrieving-an-enumerator-instance"></a>Recuperando uma instância de enumerador  
Para recuperar a tabela que contém informações sobre as instâncias disponíveis do SQL Server, primeiro recupere um enumerador, usando a propriedade compartilhada/estática <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A>:  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =   
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
Depois de recuperar a instância estática, você pode chamar o método <xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A>, que retorna um <xref:System.Data.DataTable> que contém informações sobre os servidores disponíveis:  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
A tabela retornada da chamada de método contém as seguintes colunas, todas que contêm `string` valores:  
  
|coluna|Descrição|  
|------------|-----------------|  
|**ServerName**|O nome do servidor.|  
|**InstanceName**|Nome da instância do servidor. Em branco se o servidor estiver sendo executado como a instância padrão.|  
|**IsClustered**|Indica se o servidor faz parte de um cluster.|  
|**Versão**|Versão do servidor. Por exemplo:<br /><br /> -   9.00.x (SQL Server 2005)<br />-10.0. XX (SQL Server 2008)<br />-   10.50.x (SQL Server 2008 R2)<br />-11.0. XX (SQL Server 2012)|  
  
## <a name="enumeration-limitations"></a>Limitações de enumeração  
Todos os servidores disponíveis podem ou não estar listados. A lista pode variar dependendo de fatores como tempos limite e tráfego de rede. Isso pode fazer com que a lista seja diferente em duas chamadas consecutivas. Somente os servidores na mesma rede serão listados. Os pacotes de difusão normalmente não percorrerão roteadores, motivo pelo qual você não verá um servidor listado, mas será estável em chamadas.  
  
Os servidores listados podem ou não ter informações adicionais, como `IsClustered` e versão. Isso depende de como a lista foi obtida. Servidores listados através do serviço do navegador do SQL Server terão mais detalhes do que os encontrados pela infraestrutura do Windows, que listarão somente o nome.  
  
> [!NOTE]
>  A enumeração de servidor só está disponível quando executada em confiança total. Os assemblies em execução em um ambiente parcialmente confiável não poderão usá-lo, mesmo que tenham a permissão de CAS (segurança de acesso ao código) <xref:Microsoft.Data.SqlClient.SqlClientPermission>.  
  
O SQL Server fornece informações para <xref:System.Data.Sql.SqlDataSourceEnumerator> usando um serviço Windows externo chamado SQL Browser. Esse serviço é habilitado por padrão, mas os administradores podem desativá-lo ou desabilitá-lo, tornando a instância do servidor invisível para essa classe.  
  
## <a name="example"></a>Exemplo  
O aplicativo de console a seguir recupera informações sobre todas as instâncias visíveis do SQL Server e exibe as informações na janela do console.  
  
```csharp  
using System.Data.Sql;  
  
class Program  
{  
  static void Main()  
  {  
    // Retrieve the enumerator instance and then the data.  
    SqlDataSourceEnumerator instance =  
      SqlDataSourceEnumerator.Instance;  
    System.Data.DataTable table = instance.GetDataSources();  
  
    // Display the contents of the table.  
    DisplayData(table);  
  
    Console.WriteLine("Press any key to continue.");  
    Console.ReadKey();  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
    foreach (System.Data.DataRow row in table.Rows)  
    {  
      foreach (System.Data.DataColumn col in table.Columns)  
      {  
        Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
      }  
      Console.WriteLine("============================");  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
