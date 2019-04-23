---
title: Visão geral de atributos personalizados de integração de CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- custom attributes [CLR integration]
- attributes [CLR integration]
- common language runtime [SQL Server], attributes
- database objects [CLR integration], custom attributes
- building database objects [CLR integration], custom attributes
ms.assetid: ecf5c097-0972-48e2-a9c0-b695b7dd2820
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8df7881dd5f38935628cb6653d57763a8846e60f
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60154202"
---
# <a name="overview-of-clr-integration-custom-attributes"></a>Visão geral dos atributos personalizados da integração CLR
  O CLR (common language runtime) do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] permite o uso de palavras-chave descritivas, denominadas atributos. Esses atributos fornecem informações adicionais para vários elementos, como métodos e classes. Os atributos são salvos no assembly com os metadados do objeto e podem ser usados para descrever seu código para outras ferramentas de desenvolvimento ou para afetar o comportamento do tempo de execução dentro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando você registrar uma rotina de CLR com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será gerado um conjunto de propriedades sobre a rotina. Essas propriedades de rotina determinam os recursos da rotina, incluindo sua possibilidade de ser indexada. Por exemplo, a definição da propriedade `DataAccess` como `DataAccessKind.Read` permite que você acesse dados de tabelas do usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dentro de uma função CLR. O exemplo a seguir mostra um caso simples em que o `DataAccess` propriedade é definida para facilitar o acesso a dados de uma tabela de usuário **table1**.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public partial class UserDefinedFunctions  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static string func1()  
    {  
        // Open a connection and create a command  
        SqlConnection conn = new SqlConnection("context connection = true");  
        conn.Open();  
        SqlCommand cmd = conn.CreateCommand();  
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10";  
        // where table1 is a user table  
        // Execute this command   
        SqlDataReader rd = cmd.ExecuteReader();  
        // Set string ret_val to str_val returned from the query  
        string ret_val = rd.GetValue(0).ToString();  
        rd.Close();  
        return ret_val;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public partial Class UserDefinedFunctions  
    <SqlFunction(DataAccess = DataAccessKind.Read)> _   
    Public Shared Function func1() As String  
        ' Open a connection and create a command  
        Dim conn As SqlConnection = New SqlConnection("context connection = true")   
        conn.Open()  
        Dim cmd As SqlCommand =  conn.CreateCommand()   
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10"  
        ' where table1 is a user table  
        ' Execute this command   
        Dim rd As SqlDataReader =  cmd.ExecuteReader()   
        ' Set string ret_val to str_val returned from the query  
        Dim ret_val As String =  rd.GetValue(0).ToString()   
        rd.Close()  
        Return ret_val  
    End Function  
End Class  
```  
  
 Para rotinas do [!INCLUDE[tsql](../../includes/tsql-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera as propriedades de rotina diretamente da definição de rotina. Para rotinas de CLR, o servidor não analisa o corpo da rotina para gerar essas propriedades. Em vez disso, você pode personalizar atributos para classes e membros de classe implementados em uma linguagem do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
 Os atributos personalizados necessários para rotinas de CLR, tipos definidos pelo usuário e agregações são definidos no namespace `Microsoft.SqlServer.Server`.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos personalizados para rotinas de CLR](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)  
  
  
