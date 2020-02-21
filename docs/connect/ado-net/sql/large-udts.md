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
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: af8402a7ff58e5d5b90d655547abcaf159bb67b4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247719"
---
# <a name="large-udts"></a>UDTs grandes

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Os UDTs (tipos definidos pelo usuário) permitem que os desenvolvedores estendam o sistema de tipo escalar do servidor armazenando objetos de CLR (Common Language Runtime) em um banco de dados SQL Server. Os UDTs podem conter vários elementos e ter comportamentos, diferentemente dos tipos de dados de alias tradicionais, que consistem em um único tipo de dados do sistema no SQL Server.  
  
Os UDTs eram anteriormente restritas a um tamanho máximo de 8 kilobytes. No SQL Server 2008, essa restrição foi removida para UDTs que têm um formato de <xref:Microsoft.Data.SqlClient.Server.Format.UserDefined>.  
  
Para obter a documentação completa dos tipos definidos pelo usuário, confira [Tipos CLR definidos pelo usuário](https://go.microsoft.com/fwlink/?LinkId=98366) nos Manuais Online do SQL Server.
  
## <a name="retrieving-udt-schemas-using-getschema"></a>Recuperar esquemas UDT usando GetSchema  
O método <xref:Microsoft.Data.SqlClient.SqlConnection.GetSchema%2A> de <xref:Microsoft.Data.SqlClient.SqlConnection> retorna informações de esquema de banco de dados em um <xref:System.Data.DataTable>.
  
### <a name="getschematable-column-values-for-udts"></a>Valores de coluna GetSchemaTable para UDTs  
O método <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> de um <xref:Microsoft.Data.SqlClient.SqlDataReader> retorna um <xref:System.Data.DataTable> que descreve os metadados da coluna. A tabela a seguir descreve as diferenças nos metadados da coluna para UDTs grandes entre o SQL Server 2005 e o SQL Server 2008.  
  
|Coluna SqlDataReader|SQL Server 2005|SQL Server 2008 e posterior|  
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
O <xref:Microsoft.Data.SqlClient.SqlDataReader> foi estendido a partir do SQL Server 2008 para dar suporte à recuperação de UDTs de valores grandes. A forma como as UDT de valores grandes são processadas por um <xref:Microsoft.Data.SqlClient.SqlDataReader> dependem da versão do SQL Server que você está usando, bem como do `Type System Version` especificado na cadeia de conexão. Para obter mais informações, consulte <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
Os seguintes métodos de <xref:Microsoft.Data.SqlClient.SqlDataReader> retornarão um <xref:System.Data.SqlTypes.SqlBinary> em vez de uma UDT quando o `Type System Version` for definido como SQL Server 2005:  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
Os seguintes métodos retornarão uma matriz de `Byte[]` em vez de uma UDT quando o `Type System Version` for definido como SQL Server 2005:  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
Observe que nenhuma das conversões são feitas para a versão atual do ADO.NET.  
  
## <a name="specifying-sqlparameters"></a>Especificar SqlParameters  
As propriedades <xref:Microsoft.Data.SqlClient.SqlParameter> a seguir foram estendidas para funcionar com UDTs grandes.  
  
|Propriedade SqlParameter|Descrição|  
|---------------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|Obtém ou define um objeto que representa o valor do parâmetro. O padrão é nulo. A propriedade pode ser `SqlBinary`, `Byte[]` ou um objeto gerenciado.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|Obtém ou define um objeto que representa o valor do parâmetro. O padrão é nulo. A propriedade pode ser `SqlBinary`, `Byte[]` ou um objeto gerenciado.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|Obtém ou define o tamanho do valor do parâmetro a ser resolvido. O valor padrão é 0. A propriedade pode ser um inteiro que representa o tamanho do valor do parâmetro. Para UDTs grandes, pode ser o tamanho real da UDT ou -1 para desconhecido.|  
  
## <a name="retrieving-data-example"></a>Exemplo de recuperação de dados  
O fragmento de código a seguir demonstra como recuperar dados de uma UDT grande. A variável `connectionString` assume uma conexão válida com um banco de dados SQL Server, e a variável `commandString` pressupõe uma instrução SELECT válida com a coluna de chave primária listada primeiro.  
  
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
