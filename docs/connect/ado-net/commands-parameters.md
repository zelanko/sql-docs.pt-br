---
title: Comandos e parâmetros
description: Saiba como usar objetos de comando no Provedor de Dados do Microsoft SqlClient para SQL Server a fim de executar comandos e retornar resultados de uma fonte de dados.
ms.date: 11/25/2020
ms.assetid: b623f810-d871-49a5-b0f5-078cc3c34db6
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: f899ad41e609874cbcc22c2a3ac959c41574e0eb
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761524"
---
# <a name="commands-and-parameters"></a>Comandos e parâmetros

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Depois de estabelecer uma conexão a uma fonte de dados, você pode executar comandos e retornar resultados da fonte de dados usando um objeto <xref:System.Data.Common.DbCommand>. Você pode criar um comando usando um dos construtores do Provedor de Dados do Microsoft SqlClient para SQL Server. Os construtores podem usar argumentos opcionais, como uma instrução SQL para executar na fonte de dados, em um objeto <xref:System.Data.Common.DbConnection> ou em um objeto <xref:System.Data.Common.DbTransaction>.

Você também pode configurar esses objetos como propriedades do comando. Pode também criar um comando para uma conexão específica usando o método <xref:System.Data.Common.DbConnection.CreateCommand%2A> de um objeto `DbConnection`. A instrução SQL que está sendo executada pelo comando pode ser configurada usando a propriedade <xref:System.Data.Common.DbCommand.CommandText%2A>. O Provedor de Dados do Microsoft SqlClient para SQL Server tem o objeto <xref:Microsoft.Data.SqlClient.SqlCommand>.

## <a name="in-this-section"></a>Nesta seção

[Executando um comando](execute-command.md)  
Descreve o objeto `Command` ADO.NET e como usá-lo para executar consultas e comandos em uma fonte de dados.

[Configurando parâmetros](configure-parameters.md)  
Descreve como trabalhar com os parâmetros de `Command`, incluindo a direção, os tipos de dados e a sintaxe de parâmetro.

[Gerar comandos com CommandBuilders](generate-commands-with-commandbuilders.md)  
Descreve como usar construtores de comando para gerar automaticamente comandos INSERT, UPDATE, e DELETE para um `DataAdapter` que possui um comando SELECT de uma única tabela.

[Obtendo apenas um valor de um banco de dados](obtain-single-value-from-database.md)  
Descreve como usar o método `ExecuteScalar` de um objeto `Command` para retornar um único valor de uma consulta de banco de dados.

[Usar comandos para modificar dados](use-commands-to-modify-data.md)  
Descreve como usar o Provedor de Dados do Microsoft SqlClient para SQL Server a fim de executar procedimentos armazenados ou instruções DDL (linguagem de definição de dados).

## <a name="see-also"></a>Confira também

- [Conectar-se a fontes de dados](connecting-to-data-source.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
