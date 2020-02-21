---
title: Buscar linhas | Microsoft Docs
description: Buscar linhas usando a interface IRowset
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- IRowset interface
- OLE DB Driver for SQL Server, fetching
author: pmasl
ms.author: pelopes
ms.openlocfilehash: d47e94795f3bb81dd7a2d870190f081436c47e07
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015358"
---
# <a name="fetching-rows"></a>Buscando linhas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A interface **IRowset** é a interface de conjunto de linhas base. A interface **IRowset** fornece métodos para buscar linhas em sequência, obter os dados dessas linhas e gerenciar linhas. Os consumidores usam os métodos em **IRowset** para todas as operações básicas de conjunto de linhas. Elas incluem a busca e a liberação de linhas e a obtenção de valores de coluna.  
  
 Quando um consumidor obtém um ponteiro de interface em um conjunto de linhas, normalmente, a primeira etapa é determinar as funcionalidades do conjunto de linhas usando o método **IRowsetInfo::GetProperties**. São retornadas informações sobre as interfaces expostas pelo conjunto de linhas, além dos recursos do conjunto de linhas que não aparecem como interfaces distintas, como o número máximo de linhas ativas e o número de linhas que podem ter atualizações pendentes simultaneamente.  
  
 A próxima etapa para os consumidores é determinar as características, ou metadados, das colunas no conjunto de linhas. Para isso, são usados o método **IColumnsInfo** para informações de coluna simples ou o método **IColumnsRowset** para informações de coluna estendida. O método **GetColumnInfo** retorna as seguintes informações:  
  
-   O número de colunas no conjunto de resultados.  
  
-   Uma matriz de estruturas DBCOLUMNINFO, uma por coluna.  
  
     A ordem das estruturas é a ordem na qual as colunas aparecem no conjunto de linhas. Cada estrutura DBCOLUMNINFO inclui metadados de coluna, como o nome da coluna, o ordinal da coluna, o comprimento máximo possível de um valor na coluna, o tipo de dados da coluna, a precisão e o comprimento.  
  
-   O ponteiro para um armazenamento de todos os valores da cadeia de caracteres dentro de um único bloco de alocação.  
  
 O consumidor determina quais colunas são necessárias a partir dos metadados ou com base no comando de texto que gerou o conjunto de linhas. Ele determina os ordinais das colunas necessárias com base na ordenação das informações de coluna retornadas por **IColumnsInfo** ou com base nos ordinais no conjunto de linhas de metadados de coluna retornados por **IColumnsRowset**.  
  
 As interfaces **IColumnsInfo** e **IColumnsRowset** são usadas para extrair informações sobre as colunas no conjunto de linhas. A interface **IColumnsInfo** retorna um conjunto limitado de informações, enquanto **IColumnsRowset** fornece todo os metadados.  
  
> [!NOTE]  
>  No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] versão 7.0 e anterior, a coluna de metadados opcional DBCOLUMN_COMPUTEMODE retornada por **IColumnsInfo::GetColumnsInfo** retorna DBSTATUS_S_ISNULL (em vez dos valores que descrevem se a coluna foi computada), pois não é possível determinar se a coluna subjacente é computada.  
  
 Os ordinais são usados para especificar uma associação com uma coluna. Uma associação é uma estrutura que associa um elemento da estrutura do consumidor com uma coluna. A associação pode associar o valor de dados, o comprimento e valor de status da coluna.  
  
 Um conjunto de associações é reunido em um acessador. Ele é criado usando o método **IAccessor::CreateAccessor**. Um acessador pode conter várias associações, de forma que os dados de várias colunas podem ser recuperados ou definidos em uma única chamada. O consumidor pode criar vários acessadores que correspondem a diversos padrões de uso em diferentes partes do aplicativo. É possível criar e liberar acessadores enquanto o conjunto de linhas continua existindo.  
  
 Para buscar linhas do banco de dados, o consumidor chama um método, como **IRowset::GetNextRows** ou **IRowsetLocate::GetRowsAt**. Essas operações de busca colocam dados de linhas do servidor no buffer de linhas do provedor. O consumidor não tem acesso direto ao buffer de linhas do provedor. O consumidor usa **IRowset::GetData** para copiar dados do buffer do provedor para o buffer do consumidor e **IRowsetChange::SetData** para copiar alterações de dados do buffer do consumidor para o buffer do provedor.  
  
 O consumidor chama o método **GetData** e passa o identificador para uma linha, o identificador para um acessador e um ponteiro para um buffer alocado pelo consumidor. **GetData** converte os dados e retorna as colunas conforme especificado nas associações usadas para criar o acessador. O consumidor pode chamar **GetData** mais de uma vez para uma linha, usando acessadores e buffers diferentes; portanto, o consumidor pode obter várias cópias dos mesmos dados.  
  
 Os dados de colunas de comprimento variável podem ser tratados de várias maneiras. Primeiro, essas colunas podem ser associadas com uma seção finita da estrutura do consumidor. Isto gera truncamento, quando o comprimento dos dados excede o comprimento do buffer. O consumidor pode determinar se ocorreu truncamento verificando o status DBSTATUS_S_TRUNCATED. O comprimento retornado sempre é o comprimento real em bytes, de forma que o consumidor também pode determinar quantos dados foram truncados.  
  
 Quando o consumidor concluir o fetch ou a atualização das linhas, ele as liberará com o método **ReleaseRows**. Isto libera recursos da cópia das linhas no conjunto de linhas, dando espaço a novas linhas. O consumidor pode repetir então o ciclo de busca ou criação de linhas e acessar os dados contidos nelas.  
  
 Quando o consumidor conclui o conjunto de linhas, ele chama o método **IAccessor::ReleaseAccessor** para liberar qualquer acessador. Ele chama o método **IUnknown::Release** em todas as interfaces expostas pelo conjunto de linhas para liberar o conjunto de linhas. Quando o conjunto de linhas é liberado, é imposta a liberação de todas as linhas ou acessadores restantes que o consumidor possa deter.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Próxima posição de busca](../../oledb/ole-db-rowsets/fetching-rows-next-fetch-position.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
