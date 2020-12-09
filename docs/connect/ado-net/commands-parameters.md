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
ms.openlocfilehash: 931c36619f5eaed0159ee04db3a08eb745634698
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428179"
---
# <a name="commands-and-parameters"></a>Comandos e parâmetros

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Depois de estabelecer uma conexão a uma fonte de dados, você pode executar comandos e retornar resultados da fonte de dados usando um objeto <xref:System.Data.Common.DbCommand>. Você pode criar um comando usando um dos construtores do Provedor de Dados do Microsoft SqlClient para SQL Server. Os construtores podem usar argumentos opcionais, como uma instrução SQL para executar na fonte de dados, em um objeto <xref:System.Data.Common.DbConnection> ou em um objeto <xref:System.Data.Common.DbTransaction>.

Você também pode configurar esses objetos como propriedades do comando. Pode também criar um comando para uma conexão específica usando o método <xref:System.Data.Common.DbConnection.CreateCommand%2A> de um objeto `DbConnection`. A instrução SQL que está sendo executada pelo comando pode ser configurada usando a propriedade <xref:System.Data.Common.DbCommand.CommandText%2A>. O Provedor de Dados do Microsoft SqlClient para SQL Server tem o objeto <xref:Microsoft.Data.SqlClient.SqlCommand>.

## <a name="in-this-section"></a>Nesta seção

[Executar um comando](execute-command.md) Descreve o objeto `Command` do ADO.NET e como usá-lo para executar consultas e comandos em uma fonte de dados.

[Configurar parâmetros](configure-parameters.md) Descreve como trabalhar com parâmetros `Command`, incluindo a direção, os tipos de dados e a sintaxe do parâmetro.

[Gerar comandos com CommandBuilders](generate-commands-with-commandbuilders.md)  
Descreve como usar construtores de comando para gerar automaticamente comandos INSERT, UPDATE, e DELETE para um `DataAdapter` que possui um comando SELECT de uma única tabela.

[Obter um único valor de um banco de dados](obtain-single-value-from-database.md) Descreve como usar o método `ExecuteScalar` de um objeto `Command` para retornar um único valor de uma consulta de banco de dados.

[Usar comandos para modificar dados](use-commands-to-modify-data.md) Descreve como usar o Provedor de Dados do Microsoft SqlClient para SQL Server a fim de executar procedimentos armazenados ou instruções DDL (linguagem de definição de dados).

## <a name="see-also"></a>Confira também

- [Conectar-se a fontes de dados](connecting-to-data-source.md)
