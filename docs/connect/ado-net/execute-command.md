---
title: Executando um comando
description: Descreve o objeto `Command` do Provedor de Dados do Microsoft SqlClient para SQL Server e como usá-lo para executar consultas e comandos em uma fonte de dados.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: 40494916-c25a-4cb8-8f7c-fcb8d378464e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: b1427fa78e52c985478996bfb41cb7a20e1ee608
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428169"
---
# <a name="executing-a-command"></a>Executando um comando

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O Provedor de Dados do Microsoft SqlClient para SQL Server tem um objeto <xref:Microsoft.Data.SqlClient.SqlCommand> que herda de <xref:System.Data.Common.DbCommand>. Esse objeto expõe métodos de execução de comandos com base no tipo de comando e no valor de retorno desejado, conforme descrito na tabela a seguir.

|Comando|Valor Retornado|  
|-------------|------------------|  
|`ExecuteReader`|Retorna um objeto `DataReader`.|  
|`ExecuteScalar`|Retorna um único valor escalar.|  
|`ExecuteNonQuery`|Executa um comando que não retorna nenhuma linha.|  
|`ExecuteXMLReader`|Retorna um <xref:System.Xml.XmlReader>. Disponível somente para um objeto do `SqlCommand`.|

 Cada objeto de comando fortemente tipado também dá suporte a uma enumeração de <xref:System.Data.CommandType> que especifica como uma cadeia de caracteres de comando é interpretada, conforme descrito na tabela a seguir.

|CommandType|Descrição|
|-----------------|-----------------|  
|`Text`|Um comando SQL que define as instruções a serem executado na fonte de dados.|  
|`StoredProcedure`|O nome do procedimento armazenado. Você pode usar a propriedade `Parameters` de um comando para acessar os parâmetros de entrada e saída e os valores de retorno, independentemente do método `Execute` chamado.|  
|`TableDirect`|O nome de uma tabela.|

> [!IMPORTANT]
> Ao usar `ExecuteReader`, os valores de retorno e os parâmetros de saída não estarão acessíveis até que o `DataReader` seja fechado.

## <a name="example"></a>Exemplo

O código de exemplo a seguir demonstra como criar um objeto <xref:Microsoft.Data.SqlClient.SqlCommand> para executar um procedimento armazenado definindo suas propriedades. Um objeto <xref:Microsoft.Data.SqlClient.SqlParameter> é usado para especificar o parâmetro de entrada para o procedimento armazenado. O comando é executado usando o método <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteReader%2A> e a saída do <xref:Microsoft.Data.SqlClient.SqlDataReader> é exibida na janela do console.

[!code-csharp[DataWorks SqlClient.StoredProcedure#1](~/../sqlclient/doc/samples/SqlCommand_StoredProcedure.cs#1)]

### <a name="troubleshooting-commands"></a>Comandos de solução de problemas

[!INCLUDE[appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

O Provedor de Dados do Microsoft SqlClient para SQL Server adiciona **contadores de desempenho** para permitir que você detecte problemas intermitentes relacionados a execuções de comandos com falha.

## <a name="see-also"></a>Confira também

- [Comandos e parâmetros](commands-parameters.md)
