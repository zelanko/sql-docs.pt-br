---
title: Parâmetros de comando | Microsoft Docs
description: Parâmetros de comando
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- parameters [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, parameters
- OLE DB Driver for SQL Server, commands
- parameters [OLE DB Driver for SQL Server], OLE DB
- commands [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 1ed49ebaffb46b8542247e67ff7c639cec1cca1d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68016109"
---
# <a name="command-parameters"></a>Parâmetros de comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Os parâmetros são marcados no texto do comando com o caractere de ponto de interrogação. Por exemplo, a seguinte instrução SQL é marcada para um único parâmetro de entrada:  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 Para melhorar o desempenho reduzindo o tráfego de rede, o OLE DB Driver for SQL Server não obtém automaticamente as informações de parâmetro, a menos que **ICommandWithParameters::GetParameterInfo** ou **ICommandPrepare::Prepare** seja chamado antes da execução de um comando. Isso significa que o Driver do OLE DB para SQL Server não faz automaticamente o seguinte:  
  
-   Verifique a exatidão do tipo de dados especificado com **ICommandWithParameters::SetParameterInfo**.  
  
-   Mapeie do DBTYPE especificado nas informações de associação do acessador para o tipo de dados correto do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do parâmetro.  
  
 Os aplicativos receberão erros possíveis ou perda de precisão com um desses métodos, se especificarem tipos de dados não compatíveis com o tipo de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do parâmetro.  
  
 Para garantir que isso não aconteça, o aplicativo deve:  
  
-   Garantir que *pwszDataSourceType* corresponda aos tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do parâmetro em caso de hard-coding de **ICommandWithParameters::SetParameterInfo**.  
  
-   Garantir que o valor DBTYPE associado ao parâmetro seja do mesmo tipo do tipo de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do parâmetro em caso de hard-coding de um acessador.  
  
-   Codifique o aplicativo para chamar **ICommandWithParameters::GetParameterInfo** de forma que o provedor possa obter os tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dos parâmetros dinamicamente. Observe que isso causa uma viagem de ida e volta na rede adicional até o servidor.  
  
> [!NOTE]  
>  O provedor não dá suporte à chamada a **ICommandWithParameters::GetParameterInfo** em nenhuma instrução UPDATE ou DELETE do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que contenha uma cláusula FROM; em qualquer instrução SQL que dependa de uma subconsulta que contenha parâmetros; em instruções SQL que contenham marcadores de parâmetro em expressões de uma comparação, semelhança ou predicado quantificado; ou em consultas nas quais um dos parâmetros é um parâmetro de uma função. Ao processar um lote de instruções SQL, o provedor também não dá suporte à chamada a **ICommandWithParameters::GetParameterInfo** em marcadores de parâmetro nas instruções após a primeira instrução no lote. Não são permitidos comentários (/* \*/) no comando [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 O Driver do OLE DB para SQL Server é compatível com parâmetros de entrada em comandos de instrução SQL. Nos comandos de chamada de procedimento, o Driver do OLE DB para SQL Server é compatível com parâmetros de entrada, de saída e de entrada/saída. Os valores de parâmetro de saída são retornados para o aplicativo na execução (apenas se não houver nenhum conjunto de linhas retornado) ou quando todos os conjuntos de linhas retornados são esgotados pelo aplicativo. Para garantir a validade dos valores retornados, use **IMultipleResults** para forçar o consumo do conjunto de linhas.  
  
 Os nomes dos parâmetros de procedimento armazenado não precisam ser especificados em uma estrutura DBPARAMBINDINFO. Use NULL para o valor do membro *pwszName* para indicar que o OLE DB Driver for SQL Server deve ignorar o nome do parâmetro e usar apenas o ordinal especificado no membro *rgParamOrdinals* de **ICommandWithParameters::SetParameterInfo**. Caso o texto do comando contenha parâmetros nomeados e sem-nome, todos os parâmetros sem-nome devem ser especificados antes de qualquer parâmetro nomeado.  
  
 Caso o nome de um parâmetro de procedimento armazenado seja especificado, o OLE DB Driver for SQL Server verificará o nome para garantir sua validade. O Driver do OLE DB para SQL Server retorna um erro ao receber um nome de parâmetro incorreto do consumidor.  
  
> [!NOTE]  
>  Para expor o suporte a XML e à UDT (tipos definidos pelo usuário) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o OLE DB Driver for SQL Server implementa uma nova interface [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
