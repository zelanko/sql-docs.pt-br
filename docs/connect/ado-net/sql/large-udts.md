---
title: UDTs grandes
description: Demonstra como recuperar dados de UDTs de valor grande introduzidos no SQL Server 2008.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 420ae24e-762b-4e09-b4c3-2112c470ee49
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4ea2c0002ceb01606cdf51f04246abcdc74429e0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452157"
---
# <a name="large-udts"></a>UDTs grandes

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Os UDTs (tipos definidos pelo usuário) permitem que os desenvolvedores estendam o sistema de tipo escalar do servidor armazenando objetos de CLR (Common Language Runtime) em um banco de dados SQL Server. Os UDTs podem conter vários elementos e ter comportamentos, diferentemente dos tipos de dados de alias tradicionais, que consistem em um único tipo de dados do sistema no SQL Server.  
  
Os UDTs eram anteriormente restritas a um tamanho máximo de 8 kilobytes. No SQL Server 2008, essa restrição foi removida para UDTs que têm um formato de <xref:Microsoft.Data.SqlClient.Server.Format.UserDefined>.  
  
Para obter a documentação completa de tipos definidos pelo usuário, consulte [tipos CLR definidos pelo usuário](https://go.microsoft.com/fwlink/?LinkId=98366) do manuais online do SQL Server.
  
## <a name="retrieving-udt-schemas-using-getschema"></a>Recuperando esquemas UDT usando GetSchema  
O método <xref:Microsoft.Data.SqlClient.SqlConnection.GetSchema%2A> de <xref:Microsoft.Data.SqlClient.SqlConnection> retorna informações de esquema de banco de dados em um <xref:System.Data.DataTable>.
  
### <a name="getschematable-column-values-for-udts"></a>Valores de coluna GetSchemaTable para UDTs  
O método <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> de um <xref:Microsoft.Data.SqlClient.SqlDataReader> retorna uma <xref:System.Data.DataTable> que descreve os metadados da coluna. A tabela a seguir descreve as diferenças nos metadados de coluna para UDTs grandes entre SQL Server 2005 e SQL Server 2008.  
  
|Coluna do SqlDataReader|SQL Server 2005|SQL Server 2008 e posterior|  
|--------------------------|---------------------|-------------------------------|  
|`ColumnSize`|Varia|Varia|  
|`NumericPrecision`|255|255|  
|`NumericScale`|255|255|  
|`DataType`|`Byte[]`|Instância UDT|  
|`ProviderSpecificDataType`|`SqlTypes.SqlBinary`|Instância UDT|  
|`ProviderType`|21 (`SqlDbType.VarBinary`)|29 (`SqlDbType.Udt`)|  
|`NonVersionedProviderType`|29 (`SqlDbType.Udt`)|29 (`SqlDbType.Udt`)|  
|`DataTypeName`|`SqlDbType.VarBinary`|O nome de três partes especificado como *Database.SchemaName.TypeName*.|  
|`IsLong`|Varia|Varia|  
  
## <a name="sqldatareader-considerations"></a>Considerações sobre o SqlDataReader  
O <xref:Microsoft.Data.SqlClient.SqlDataReader> foi estendido a partir do SQL Server 2008 para dar suporte à recuperação de valores UDT grandes. A forma como os valores UDT grandes são processados por uma <xref:Microsoft.Data.SqlClient.SqlDataReader> depende da versão do SQL Server que você está usando, bem como do `Type System Version` especificado na cadeia de conexão. Para obter mais informações, consulte <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
Os seguintes métodos de <xref:Microsoft.Data.SqlClient.SqlDataReader> retornarão um <xref:System.Data.SqlTypes.SqlBinary> em vez de um UDT quando o `Type System Version` for definido como SQL Server 2005:  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
Os métodos a seguir retornarão uma matriz de `Byte[]` em vez de um UDT quando a `Type System Version` for definida como SQL Server 2005:  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
Observe que nenhuma conversões é feita para a versão atual do ADO.NET.  
  
## <a name="specifying-sqlparameters"></a>Especificando Parameters  
As propriedades <xref:Microsoft.Data.SqlClient.SqlParameter> a seguir foram estendidas para funcionar com UDTs grandes.  
  
|Propriedade SqlParameter|Descrição|  
|---------------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|Obtém ou define um objeto que representa o valor do parâmetro. O padrão é nulo. A propriedade pode ser `SqlBinary`, `Byte[]` ou um objeto gerenciado.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|Obtém ou define um objeto que representa o valor do parâmetro. O padrão é nulo. A propriedade pode ser `SqlBinary`, `Byte[]` ou um objeto gerenciado.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|Obtém ou define o tamanho do valor do parâmetro a ser resolvido. O valor padrão é 0. A propriedade pode ser um inteiro que representa o tamanho do valor do parâmetro. Para UDTs grandes, pode ser o tamanho real de UDT ou-1 para desconhecido.|  
  
## <a name="retrieving-data-example"></a>Exemplo de recuperação de dados  
O fragmento de código a seguir demonstra como recuperar dados UDT grandes. A variável `connectionString` assume uma conexão válida com um banco de dados SQL Server e a variável `commandString` pressupõe uma instrução SELECT válida com a coluna de chave primária listada primeiro.  
  
```csharp  
using (SqlConnection connection = new SqlConnection(   
    connectionString, commandString))  
{  
  connection.Open();  
  SqlCommand command = new SqlCommand(commandString);  
  SqlDataReader reader = command.ExecuteReader();  
  while (reader.Read())  
  {  
    // Retrieve the value of the Primary Key column.  
    int id = reader.GetInt32(0);  
  
    // Retrieve the value of the UDT.  
    LargeUDT udt = (LargeUDT)reader[1];  
  
    // You can also use GetSqlValue and GetValue.  
    // LargeUDT udt = (LargeUDT)reader.GetSqlValue(1);  
    // LargeUDT udt = (LargeUDT)reader.GetValue(1);  
  
    Console.WriteLine(  
     "ID={0} LargeUDT={1}", id, udt);  
  }  
reader.close  
}  
```  
  
## <a name="next-steps"></a>Próximas etapas
- [Dados binários e de valor grande do SQL Server](sql-server-binary-large-value-data.md)
