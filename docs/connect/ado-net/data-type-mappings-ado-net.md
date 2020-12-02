---
title: Mapeamentos de tipo de dados
description: Descreve os tipos de dados usados pelo Provedor de Dados do Microsoft SqlClient para SQL Server.
ms.date: 11/13/2020
ms.assetid: d4afab94-ada6-4c77-a73c-41f17bae6b5a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 20897f6ffbcf165c38bedac2ed1f8e6ad760cc93
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126333"
---
# <a name="data-type-mappings-in-adonet"></a>Mapeamentos de tipo de dados no ADO.NET

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O ADO.NET é baseado no Common Type System, que define como os tipos são declarados, usados e gerenciados no runtime. Consiste nos tipos de valor e nos tipos de referência, que derivam do tipo de base <xref:System.Object>. Ao trabalhar com uma fonte de dados, o tipo de dados será inferido no provedor de dados se não for especificado explicitamente. Por exemplo, um objeto <xref:System.Data.DataSet> é independente de qualquer fonte de dados específica. Os dados de um `DataSet` são recuperados de uma fonte de dados, e as alterações são persistidas de volta para a fonte de dados usando o `DataAdapter`. Esse fluxo de programa significa que, quando um `DataAdapter` preenche um <xref:System.Data.DataTable> em um `DataSet` com valores de uma fonte de dados, os tipos de dados resultantes das colunas em `DataTable` são tipos de .NET Framework, em vez de tipos específicos do Provedor de Dados Microsoft SqlClient para SQL Server que são usados para se conectar à fonte de dados.

Da mesma forma, quando um `DataReader` retorna um valor de uma fonte de dados, o valor resultante é armazenado em uma variável local que tem um tipo de .NET Framework. Para as operações `Fill` do `DataAdapter` e os métodos `Get` do `DataReader`, o tipo de .NET Framework é inferido do valor retornado do Provedor de Dados Microsoft SqlClient para SQL Server.

Em vez de depender do tipo de dados inferido, você pode usar os métodos acessadores tipados do `DataReader` quando souber o tipo específico do valor que está sendo retornado. Os métodos acessadores tipados oferecem melhor desempenho retornando um valor como um tipo específico de .NET Framework, o que elimina a necessidade de conversão de tipo adicional.

> [!NOTE]
> Os valores nulos para os tipos de dados do Provedor de Dados Microsoft SqlClient para SQL Server são representados por `DBNull.Value`.

## <a name="in-this-section"></a>Nesta seção

[Mapeamentos de tipo de dados do SQL Server](sql-server-data-type-mappings.md) Lista mapeamentos de tipo de dados inferidos e métodos acessadores de dados para <xref:Microsoft.Data.SqlClient>.

[Números de pontos flutuantes](floating-point-numbers.md) Descreve os problemas que os desenvolvedores costumam encontrar ao trabalhar com números de pontos flutuantes.

## <a name="see-also"></a>Confira também

- [Tipos de dados do SQL Server e ADO.NET](./sql/sql-server-data-types.md)
