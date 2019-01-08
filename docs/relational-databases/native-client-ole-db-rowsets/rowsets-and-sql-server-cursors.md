---
title: Conjuntos de linhas e cursores do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB rowsets, cursors
- SQL Server Native Client OLE DB provider, rowsets
- rowsets [OLE DB], cursors
- properties [OLE DB]
- cursors [OLE DB]
ms.assetid: 26a11e26-2a3a-451e-8f78-fba51e330ecb
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6f8c58f38f100258ed9c6b0b1a95cbd37273aaa1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507808"
---
# <a name="rowsets-and-sql-server-cursors"></a>Conjuntos de linha e cursores do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna conjuntos de resultados para clientes usando dois métodos:  
  
-   Conjuntos de resultados padrão que:  
  
    -   Minimizam sobrecarga.  
  
    -   Proporcionam desempenho máximo na busca de dados.  
  
    -   Oferecem suporte à funcionalidade de cursor apenas de encaminhamento e somente leitura.  
  
    -   Retornam linhas para o consumidor uma linha por vez.  
  
    -   Oferecem suporte a apenas uma instrução ativa por vez em uma conexão.  
  
         Após a execução de uma instrução, nenhuma outra pode ser executada na conexão até que todos os resultados sejam recuperados pelo cliente ou a instrução seja cancelada.  
  
    -   Oferecem suporte a todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Cursores de servidor que:  
  
    -   Oferecem suporte a toda a funcionalidade de cursor.  
  
    -   Podem retornar blocos de linhas para o consumidor.  
  
    -   Oferecem suporte a várias instruções ativas em uma única conexão.  
  
    -   Equilibram a funcionalidade de cursor em relação ao desempenho.  
  
         O suporte à funcionalidade de cursor pode diminuir o desempenho em relação a um conjunto de resultados padrão. Isso pode ser compensado caso o consumidor possa usar a funcionalidade de cursor para recuperar um conjunto menor de linhas.  
  
    -   Não oferecem suporte a nenhuma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que retorna mais do que um único conjunto de resultados.  
  
 Os consumidores podem solicitar diversos comportamentos de cursor em um conjunto de linhas definindo determinadas propriedades de conjunto de linhas. Se o consumidor não definir qualquer uma dessas propriedades de conjunto de linhas ou defina todas como seus valores padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client implementa o conjunto de linhas usando um conjunto de resultados padrão. Se qualquer uma dessas propriedades for definida como um valor diferente do padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client implementa o conjunto de linhas usando um cursor de servidor.  
  
 As seguintes propriedades de conjunto de linhas levam o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a usar cursores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Algumas propriedades podem ser tranquilamente combinadas com outras. Por exemplo, um conjunto de linhas que exibe as propriedades DBPROP_IRowsetScroll e DBPROP_IRowsetChange será um conjunto de linhas indicador que exibe um comportamento de atualização imediato. Outras propriedades são mutuamente excludentes. Por exemplo, um conjunto de linhas que exibe DBPROP_OTHERINSERT não pode conter indicadores.  
  
|ID da propriedade|Valor|Comportamento do conjunto de linhas|  
|-----------------|-----------|---------------------|  
|DBPROP_SERVERCURSOR|VARIANT_TRUE|Não é possível atualizar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no conjunto de linhas. O conjunto de linhas é sequencial, o que oferece suporte apenas ao roll-forward e à busca. Há suporte para o posicionamento de linha relativo. O texto do comando pode conter uma cláusula ORDER BY.|  
|DBPROP_CANSCROLLBACKWARDS ou DBPROP_CANFETCHBACKWARDS|VARIANT_TRUE|Não é possível atualizar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no conjunto de linhas. O conjunto de linhas oferece suporte à rolagem e à busca em qualquer direção. Há suporte para o posicionamento de linha relativo. O texto do comando pode conter uma cláusula ORDER BY.|  
|DBPROP_BOOKMARKS ou DBPROP_LITERALBOOKMARKS|VARIANT_TRUE|Não é possível atualizar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no conjunto de linhas. O conjunto de linhas é sequencial, o que oferece suporte apenas ao roll-forward e à busca. Há suporte para o posicionamento de linha relativo. O texto do comando pode conter uma cláusula ORDER BY.|  
|DBPROP_OWNUPDATEDELETE ou DBPROP_OWNINSERT ou DBPROP_OTHERUPDATEDELETE|VARIANT_TRUE|Não é possível atualizar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no conjunto de linhas. O conjunto de linhas oferece suporte à rolagem e à busca em qualquer direção. Há suporte para o posicionamento de linha relativo. O texto do comando pode conter uma cláusula ORDER BY.|  
|DBPROP_OTHERINSERT|VARIANT_TRUE|Não é possível atualizar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no conjunto de linhas. O conjunto de linhas oferece suporte à rolagem e à busca em qualquer direção. Há suporte para o posicionamento de linha relativo. O texto do comando pode incluir uma cláusula ORDER BY caso haja um índice nas colunas referenciadas.<br /><br /> DBPROP_OTHERINSERT não pode ser VARIANT_TRUE caso o conjunto de linhas contenha indicadores. Tentar criar um conjunto de linhas com essa propriedade de visibilidade e indicadores causa um erro.|  
|DBPROP_IRowsetLocate ou DBPROP_IRowsetScroll|VARIANT_TRUE|Não é possível atualizar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no conjunto de linhas. O conjunto de linhas oferece suporte à rolagem e à busca em qualquer direção. Há suporte para indicadores e posicionamento absoluto por meio da interface **IRowsetLocate** no conjunto de linhas. O texto do comando pode conter uma cláusula ORDER BY.<br /><br /> DBPROP_IRowsetLocate e DBPROP_IRowsetScroll exigem marcadores no conjunto de linhas. Tentar criar um conjunto de linhas com indicadores e DBPROP_OTHERINSERT definidos como VARIANT_TRUE causa um erro.|  
|DBPROP_IRowsetChange ou DBPROP_IRowsetUpdate|VARIANT_TRUE|É possível atualizar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do conjunto de linhas. O conjunto de linhas é sequencial, o que oferece suporte apenas ao roll-forward e à busca. Há suporte para o posicionamento de linha relativo. Todos os comandos que oferecem suporte a cursores atualizáveis podem oferecer suporte a essas interfaces.|  
|DBPROP_IRowsetLocate ou DBPROP_IRowsetScroll e DBPROP_IRowsetChange ou DBPROP_IRowsetUpdate|VARIANT_TRUE|É possível atualizar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do conjunto de linhas. O conjunto de linhas oferece suporte à rolagem e à busca em qualquer direção. Há suporte para indicadores e posicionamento absoluto por meio de **IRowsetLocate** no conjunto de linhas. O texto do comando pode conter uma cláusula ORDER BY.|  
|DBPROP_IMMOBILEROWS|VARIANT_FALSE|Não é possível atualizar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no conjunto de linhas. O conjunto de linhas oferece suporte apenas a roll-forward. Há suporte para o posicionamento de linha relativo. O texto do comando pode incluir uma cláusula ORDER BY caso haja um índice nas colunas referenciadas.<br /><br /> DBPROP_IMMOBILEROWS só está disponível em conjuntos de linhas capazes de mostrar linhas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inseridas por comandos em outras sessões ou por outros usuários. Tentar abrir um conjunto de linhas com a propriedade definida como VARIANT_FALSE em qualquer conjunto de linhas em que DBPROP_OTHERINSERT não pode ser VARIANT_TRUE causa um erro.|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|Não é possível atualizar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no conjunto de linhas. O conjunto de linhas oferece suporte apenas a roll-forward. Há suporte para o posicionamento de linha relativo. O texto do comando pode conter uma cláusula ORDER BY, exceto quando restrito por outra propriedade.|  
  
 Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de linhas do provedor OLE DB do Native Client tem suportado por um cursor de servidor pode ser facilmente criado em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela base ou exibição usando o **IOpenRowset:: OPENROWSET** método. Especifique a tabela ou a exibição por nome, passando os conjuntos de propriedades do conjunto de linhas necessários no parâmetro *rgPropertySets*.  
  
 O texto do comando que cria um conjunto de linhas é restringido quando o consumidor exige que haja suporte ao conjunto por um cursor de servidor. Mais especificamente, o texto do comando é restringido a uma única instrução SELECT que retorna um único resultado do conjunto de linhas ou um procedimento armazenado que implementa uma única instrução SELECT que retorna um único resultado do conjunto de linhas.  
  
 Essas duas tabelas mostram os mapeamentos de várias propriedades OLE DB e os modelos de cursor. Elas também mostram as propriedades do conjunto de linhas que devem ser definidas para usar um determinado tipo de modelo de cursor.  
  
 Cada célula na tabela contém um valor da propriedade do conjunto de linhas para o modelo de cursor específico. O tipo de dados de todas as propriedades do conjunto de linhas listado anteriormente neste tópico é VT_BOOL e o valor padrão, VARIANT_FALSE. Os seguintes símbolos são usados na tabela.  
  
 F = valor padrão (VARIANT_FALSE)  
  
 T = VARIANT_TRUE  
  
 \- = VARIANT_TRUE ou VARIANT_FALSE  
  
 Para usar um determinado tipo de modelo de cursor, localize a coluna correspondente ao modelo de cursor e encontre todas as propriedades do conjunto de linhas com o valor 'T' na coluna. Defina essas propriedades do conjunto de linhas como VARIANT_TRUE para usar o modelo de cursor específico. As propriedades do conjunto de linhas com '-' como um valor podem ser definidas como VARIANT_TRUE ou VARIANT_FALSE.  
  
|Propriedades do conjunto de linhas/modelos de cursor|Padrão<br /><br /> result<br /><br /> set<br /><br /> (RO)|Rápido<br /><br /> avanço<br /><br /> rápido<br /><br /> (RO)|Estático<br /><br /> (RO)|Keyset<br /><br /> por conjunto de chaves<br /><br /> (RO)|  
|--------------------------------------|-------------------------------------------|--------------------------------------------|-----------------------|----------------------------------|  
|DBPROP_SERVERCURSOR|F|T|T|T|  
|DBPROP_DEFERRED|F|F|-|-|  
|DBPROP_IrowsetChange|F|F|F|F|  
|DBPROP_IrowsetLocate|F|F|-|-|  
|DBPROP_IrowsetScroll|F|F|-|-|  
|DBPROP_IrowsetUpdate|F|F|F|F|  
|DBPROP_BOOKMARKS|F|F|-|-|  
|DBPROP_CANFETCHBACKWARDS|F|F|-|-|  
|DBPROP_CANSRCOLLBACKWARDS|F|F|-|-|  
|DBPROP_CANHOLDROWS|F|F|-|-|  
|DBPROP_LITERALBOOKMARKS|F|F|-|-|  
|DBPROP_OTHERINSERT|F|T|F|F|  
|DBPROP_OTHERUPDATEDELETE|F|T|F|T|  
|DBPROP_OWNINSERT|F|T|F|T|  
|DBPROP_OWNUPDATEDELETE|F|T|F|T|  
|DBPROP_QUICKSTART|F|F|-|-|  
|DBPROP_REMOVEDELETED|F|F|F|-|  
|DBPROP_IrowsetResynch|F|F|F|-|  
|DBPROP_CHANGEINSERTEDROWS|F|F|F|F|  
|DBPROP_SERVERDATAONINSERT|F|F|F|-|  
|DBPROP_UNIQUEROWS|-|F|F|F|  
|DBPROP_IMMOBILEROWS|-|-|-|T|  
  
|Propriedades/modelos de cursor do conjunto de linhas|Dinâmico (RO)|Conjunto de chaves (R/W)|Dinâmico (R/W)|  
|--------------------------------------|--------------------|---------------------|----------------------|  
|DBPROP_SERVERCURSOR|T|T|T|  
|DBPROP_DEFERRED|-|-|-|  
|DBPROP_IrowsetChange|F|-|-|  
|DBPROP_IrowsetLocate|F|-|F|  
|DBPROP_IrowsetScroll|F|-|F|  
|DBPROP_IrowsetUpdate|F|-|-|  
|DBPROP_BOOKMARKS|F|-|F|  
|DBPROP_CANFETCHBACKWARDS|-|-|-|  
|DBPROP_CANSRCOLLBACKWARDS|-|-|-|  
|DBPROP_CANHOLDROWS|F|-|F|  
|DBPROP_LITERALBOOKMARKS|F|-|F|  
|DBPROP_OTHERINSERT|T|F|T|  
|DBPROP_OTHERUPDATEDELETE|T|T|T|  
|DBPROP_OWNINSERT|T|T|T|  
|DBPROP_OWNUPDATEDELETE|T|T|T|  
|DBPROP_QUICKSTART|-|-|-|  
|DBPROP_REMOVEDELETED|T|-|T|  
|DBPROP_IrowsetResynch|-|-|-|  
|DBPROP_CHANGEINSERTEDROWS|F|-|F|  
|DBPROP_SERVERDATAONINSERT|F|-|F|  
|DBPROP_UNIQUEROWS|F|F|F|  
|DBPROP_IMMOBILEROWS|F|T|F|  
  
 Para um determinado conjunto de propriedades de conjunto de linhas, o modelo de cursor selecionado é determinado da forma a seguir.  
  
 Na coleção especificada de propriedades do conjunto de linhas, obtenha um subconjunto das propriedades listadas nas tabelas anteriores. Divida essas propriedades em dois subgrupos de acordo com o valor do sinalizador obrigatório (T, F) ou opcional (-) de cada propriedade do conjunto de linhas. Para cada modelo de cursor, comece na primeira tabela e se mova da esquerda para direita. Compare os valores das propriedades nos dois subgrupos com os valores das propriedades correspondentes na coluna. O modelo de cursor que não tem nenhuma incompatibilidade com as propriedades exigidas e o menor número de incompatibilidades com as propriedades opcionais é selecionado. Caso haja mais de um modelo de cursor, é escolhido o mais à esquerda.  
  
## <a name="sql-server-cursor-block-size"></a>Tamanho do bloco de cursor do SQL Server  
 Quando um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursor dá suporte a uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de linhas de provedor OLE DB do Native Client, o número de elementos na linha de parâmetro de matriz de lidar com o **IRowset::** ou o **irowsetlocate:: Getrowsat**  métodos define o tamanho do bloco de cursor. As linhas apontadas pelos identificadores na matriz são os membros do bloco de cursor.  
  
 Para conjuntos de linhas que dão suporte a indicadores, os identificadores de linha recuperados usando o método **IRowsetLocate::GetRowsByBookmark** definem os membros do bloco de cursor.  
  
 Independentemente do método usado para preencher o conjunto de linhas e formar o bloco de cursor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o bloco permanece ativo até que o próximo método de busca de linhas seja executado no conjunto.  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
