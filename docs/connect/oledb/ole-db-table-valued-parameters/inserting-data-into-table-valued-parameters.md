---
title: Inserindo dados em parâmetros com valor de tabela | Microsoft Docs
description: Usando o Driver do OLE DB para SQL Server para inserir dados em parâmetros com valor de tabela
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, inserting data into
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: c1edbe7d411e06e477db016db62b4245e0893aee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801160"
---
# <a name="inserting-data-into-table-valued-parameters"></a>Inserindo dados em parâmetros com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O OLE DB Driver for SQL Server dá suporte a dois modelos para o consumidor especificar dados para as linhas de parâmetro com valor de tabela: um modelo de push e um modelo de pull. Uma amostra que apresenta o modelo de pull está disponível; confira [Amostras de programação do SQL Server Data](https://msftdpprodsamples.codeplex.com/).  
  
> [!NOTE]  
>  Uma coluna de parâmetro com valor de tabela deve ter valores não padrão em todas as linhas ou valores padrão em todas as linhas. Não é possível ter valores padrão em algumas linhas, mas não em outras. Dessa forma, em associações de parâmetro com valor de tabela, os únicos valores de status permitidos para os dados da coluna do conjunto de linhas do parâmetro com valor de tabela são DBSTATUS_S_ISNULL e DBSTATUS_S_OK. DBSTATUS_S_DEFAULT resultará em falha e o valor de status associado será definido como DBSTATUS_E_BADSTATUS.  
  
## <a name="push-model-loads-all-table-valued-paremeter-data-in-memory"></a>Modelo de push (carrega todos os dados do parâmetro com valor de tabela na memória)  
 O modelo de push é semelhante ao uso de conjuntos de parâmetro (ou seja, o parâmetro DBPARAMS em ICommand::Execute). O modelo de push só será usado se forem usados objetos de conjunto de linhas de parâmetro com valor de tabela sem uma implementação personalizada de interfaces IRowset. O modelo de push é recomendado quando o número de linhas no conjunto de linhas do parâmetro com valor de tabela é pequeno e não se espera que uma pressão excessiva de memória seja colocada no aplicativo. Esse modelo é mais simples do que o modelo de pull, pois não exige nenhuma outra funcionalidade do aplicativo do consumidor daquela que seja atualmente comum em aplicativos OLE DB típicos.  
  
 Espera-se que o consumidor forneça todos os dados de parâmetro com valor de tabela ao provedor antes de executar um comando. Para fornecer os dados, o consumidor popula um objeto do conjunto de linhas de parâmetro com valor de tabela para cada parâmetro com valor de tabela. O objeto do conjunto de linhas de parâmetro com valor de tabela expõe operações Insert, Set e Delete do conjunto de linhas, que o consumidor usará para manipular os dados de parâmetro com valor de tabela. O provedor buscará os dados do objeto do conjunto de linhas de parâmetro com valor de tabela em tempo de execução.  
  
 Quando um objeto do conjunto de linhas de parâmetro com valor de tabela é fornecido ao consumidor, o consumidor pode processá-lo como um objeto do conjunto de linhas. O consumidor pode obter as informações de tipo de cada coluna (tipo, comprimento máximo, precisão e escala) usando o método de interface icolumnsinfo:: Getcolumninfo ou IColumnsRowset:: Getcolumnsrowset. Em seguida, o consumidor cria um acessador para especificar as associações referentes aos dados. A próxima etapa é inserir linhas de dados no conjunto de linhas de parâmetro com valor de tabela. Isso pode ser feito usando IRowsetChange:: Insertrow. IRowsetChange:: SetData ou IRowsetChange:: DeleteRows também pode ser usado no objeto de conjunto de linhas de parâmetro com valor de tabela se você tiver que manipular os dados. Objetos do conjunto de linhas de parâmetro com valor de tabela são contados como referência, semelhante à transmissão de objetos.  
  
 Se IColumnsRowset:: Getcolumnsrowset for usado, haverá chamadas subsequentes para IRowset:: IRowset:: GetData e IRowset:: Releaserows métodos no objeto de conjunto de linhas da coluna resultante.  
  
 Depois que o OLE DB Driver for SQL Server começa a executar o comando, os valores de parâmetro com valor de tabela serão buscados nesse objeto do conjunto de linhas de parâmetro com valor de tabela e enviados para o servidor.  
  
 O modelo de push requer um esforço mínimo do consumidor, mas usa mais memória do que o modelo de pull, pois todos os dados de parâmetro com valor de tabela precisam estar na memória em tempo de execução.  
  
## <a name="pull-model-obtaining-table-valued-parameter-data-on-demand-from-the-consumer"></a>Modelo de pull (obtendo dados de parâmetro com valor de tabela sob demanda do consumidor)  
 O modelo de pull é útil para dois cenários:  
  
-   Para transmitir linhas.  
  
-   Se um conjunto de linhas de outro provedor estiver sendo usado como o valor do parâmetro com valor de tabela.  
  
 No modelo de pull, o consumidor fornece dados sob demanda para o provedor. Use esta abordagem se seu aplicativo tiver muitas inserções de dados, e os dados do conjunto de linhas de parâmetro com valor de tabela na memória resultarem em acesso de memória excessivo. Se forem usados vários provedores OLE DB, o modelo de pull do consumidor permitirá que o consumidor forneça qualquer objeto do conjunto de linhas como o valor de parâmetro com valor de tabela.  
  
 Para usar o modelo de pull, os consumidores precisam fornecer suas próprias implementações de um objeto do conjunto de linhas. Ao usar o modelo de pull com conjuntos de linhas de parâmetro com valor de tabela (CLSID_ROWSET_TVP), o consumidor é necessário para agregar o objeto de conjunto de linhas de parâmetro com valor de tabela que o provedor expõe por meio de ITableDefinitionWithConstraints:: CreateTableWithConstraints ou o método IOpenRowset:: OPENROWSET. Espera-se que o objeto do consumidor substitua a implementação da interface IRowset. Você deve substituir as seguintes funções:  
  
-   IRowset::GetNextRows  
  
-   IRowset::AddRefRows  
  
-   IRowset::GetData  
  
-   IRowset::ReleaseRows  
  
-   IRowset::RestartPosition  
  
 O OLE DB Driver for SQL Server lerá uma ou mais linhas por vez do objeto de conjunto de linhas do consumidor para dar suporte ao comportamento de streaming em parâmetros com valor de tabela. Por exemplo, o usuário pode ter os dados do conjunto de linhas de parâmetro com valor de tabela no disco (não na memória) e pode implementar a funcionalidade para ler dados do disco em caso de exigência do OLE DB Driver for SQL Server.  
  
 O consumidor comunicará seu formato de dados para o Driver do OLE DB para SQL Server usando IAccessor:: CreateAccessor no objeto de conjunto de linhas de parâmetro com valor de tabela. Ao ler dados do buffer do consumidor, o provedor verifica se todas as colunas graváveis e não padrão estão disponíveis através de pelo menos um identificador do acessador e usa os identificadores correspondentes para ler dados das colunas. Para evitar ambiguidade, deve haver uma correspondência um-para-um entre uma coluna do conjunto de linhas de parâmetro com valor de tabela e uma associação. Associações duplicadas para a mesma coluna resultarão em um erro. Além disso, cada acessador deve ter o *iOrdinal* membro na sequência do DBBindings. Haverá mais chamadas a IRowset::GetData que o número de acessadores por linha, e a ordem das chamadas será baseada na ordem do valor de *iOrdinal*, dos valores mais baixos até os mais altos.  
  
 É esperado que o provedor implemente a maioria das interfaces exposta pelo objeto do conjunto de linhas de parâmetro com valor de tabela. O consumidor implementará um objeto de conjunto de linhas com interfaces mínimas (IRowset). Por causa de agregação cega, as interfaces obrigatórias restantes do objeto de conjunto de linhas serão implementadas pelo objeto do conjunto de linhas de parâmetro com valor de tabela.  
  
 Para qualquer outro objeto do conjunto de linhas, como os objetos obtidos para qualquer provedor OLE DB, o conjunto de linhas fornecido pelo consumidor deverá implementar todas as interfaces obrigatórias do objeto de conjunto de linhas, conforme indicado na especificação do OLE DB.  
  
 No momento da execução, o OLE DB Driver for SQL Server chamará novamente o objeto do conjunto de linhas para buscar as linhas e ler dados de coluna.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
