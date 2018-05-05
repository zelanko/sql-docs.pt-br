---
title: Buscando linhas | Microsoft Docs
description: Buscar linhas usando a interface IRowset
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- IRowset interface
- OLE DB Driver for SQL Server, fetching
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 51f88888b2d6387bb406511b1330dba2113752d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="fetching-rows"></a>Buscando linhas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O **IRowset** interface é a interface de conjunto de linhas de base. O **IRowset** interface fornece métodos para buscar linhas em sequência, obter os dados dessas linhas e gerenciar linhas. Os consumidores usam os métodos em **IRowset** para todas as operações básicas de conjunto de linhas. Elas incluem a busca e a liberação de linhas e a obtenção de valores de coluna.  
  
 Quando um consumidor obtém um ponteiro de interface em um conjunto de linhas, a primeira etapa é normalmente determinar os recursos do conjunto de linhas usando o **irowsetinfo:: GetProperties** método. São retornadas informações sobre as interfaces expostas pelo conjunto de linhas, além dos recursos do conjunto de linhas que não aparecem como interfaces distintas, como o número máximo de linhas ativas e o número de linhas que podem ter atualizações pendentes simultaneamente.  
  
 A próxima etapa para os consumidores é determinar as características, ou metadados, das colunas no conjunto de linhas. Para isso, eles usam o **IColumnsInfo** método para obter informações de coluna simples ou o **IColumnsRowset** método para obter informações de coluna estendida. O **GetColumnInfo** método retorna as seguintes informações:  
  
-   O número de colunas no conjunto de resultados.  
  
-   Uma matriz de estruturas DBCOLUMNINFO, uma por coluna.  
  
     A ordem das estruturas é a ordem na qual as colunas aparecem no conjunto de linhas. Cada estrutura DBCOLUMNINFO inclui metadados de coluna, como o nome da coluna, o ordinal da coluna, o comprimento máximo possível de um valor na coluna, o tipo de dados da coluna, a precisão e o comprimento.  
  
-   O ponteiro para um armazenamento de todos os valores da cadeia de caracteres dentro de um único bloco de alocação.  
  
 O consumidor determina quais colunas são necessárias a partir dos metadados ou com base no comando de texto que gerou o conjunto de linhas. Determina os ordinais das colunas necessárias a partir da ordenação das informações de coluna retornadas por **IColumnsInfo** ou a partir dos ordinais no conjunto de linhas de metadados de coluna retornados por **IColumnsRowset**.  
  
 O **IColumnsInfo** e **IColumnsRowset** interfaces são usadas para extrair informações sobre as colunas no conjunto de linhas. O **IColumnsInfo** interface retorna um conjunto limitado de informações, enquanto **IColumnsRowset** fornece todos os metadados.  
  
> [!NOTE]  
>  Em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] versão 7.0 e anterior, a coluna de metadados opcional DBCOLUMN_COMPUTEMODE retornada por **icolumnsinfo:: Getcolumnsinfo** retorna DBSTATUS_S_ISNULL (em vez dos valores que descrevem se a coluna é calculado) porque ele não é possível determinar se a coluna subjacente é computada.  
  
 Os ordinais são usados para especificar uma associação com uma coluna. Uma associação é uma estrutura que associa um elemento da estrutura do consumidor com uma coluna. A associação pode associar o valor de dados, o comprimento e valor de status da coluna.  
  
 Um conjunto de associações é reunido em um acessador. Isso é criado usando o **IAccessor:: CreateAccessor** método. Um acessador pode conter várias associações, de forma que os dados de várias colunas podem ser recuperados ou definidos em uma única chamada. O consumidor pode criar vários acessadores que correspondem a diversos padrões de uso em diferentes partes do aplicativo. É possível criar e liberar acessadores enquanto o conjunto de linhas continua existindo.  
  
 Para buscar linhas do banco de dados, o consumidor chama um método, como **GetNextRows** ou **irowsetlocate:: Getrowsat**. Essas operações de busca colocam dados de linhas do servidor no buffer de linhas do provedor. O consumidor não tem acesso direto ao buffer de linhas do provedor. O consumidor usa **IRowset:: GetData** para copiar dados do buffer do provedor para o buffer do consumidor e **IRowsetChange:: SetData** para copiar as alterações de dados do buffer do consumidor para o buffer do provedor.  
  
 O consumidor chama o **GetData** método e passa o identificador para uma linha, o identificador para um acessador e um ponteiro para um buffer alocado pelo consumidor. **GetData** converte os dados e retorna as colunas como especificado nas associações usadas para criar o acessador. O consumidor pode chamar **GetData** mais de uma vez para uma linha, usando diferentes acessadores e buffers e, portanto, o consumidor pode obter várias cópias dos mesmos dados.  
  
 Os dados de colunas de comprimento variável podem ser tratados de várias maneiras. Primeiro, essas colunas podem ser associadas com uma seção finita da estrutura do consumidor. Isto gera truncamento, quando o comprimento dos dados excede o comprimento do buffer. O consumidor pode determinar se ocorreu truncamento verificando o status DBSTATUS_S_TRUNCATED. O comprimento retornado sempre é o comprimento real em bytes, de forma que o consumidor também pode determinar quantos dados foram truncados.  
  
 Quando o consumidor concluir a busca ou atualizar linhas, ele as libera com o **ReleaseRows** método. Isto libera recursos da cópia das linhas no conjunto de linhas, dando espaço a novas linhas. O consumidor pode repetir então o ciclo de busca ou criação de linhas e acessar os dados contidos nelas.  
  
 Quando o consumidor é concluído com o conjunto de linhas, ele chama o **IAccessor:: Releaseaccessor** método para liberar qualquer acessador. Ele chama o **IUnknown** método em todas as interfaces expostas pelo conjunto de linhas para liberar o conjunto de linhas. Quando o conjunto de linhas é liberado, é imposta a liberação de todas as linhas ou acessadores restantes que o consumidor possa deter.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Próxima posição de busca](../../oledb/ole-db-rowsets/fetching-rows-next-fetch-position.md)  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
