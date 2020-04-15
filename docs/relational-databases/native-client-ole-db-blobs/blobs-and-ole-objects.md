---
title: BLOBs e objetos OLE | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d0cb9751940489513f939ab8ee52728c6b75e925
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297618"
---
# <a name="blobs-and-ole-objects"></a>BLOBs e objetos OLE
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB expõe a interface **ISequentialStream** para suportar o acesso do consumidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a **ntext,** **text,** **image,** **varchar(max)**, **nvarchar(max)**, **varbinary(max)** e xml data types as biny large objects (BLOBs). O método **Read** em **ISequentialStream** permite que o consumidor recupere muitos dados em partes gerenciáveis.  
  
 Para obter um exemplo que demonstra esse recurso, confira [Definir &#40;OLE DB&#41; de dados grandes](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Nativo Cliente OLE DB pode usar uma interface **IStorage** implementada pelo consumidor quando o consumidor fornece o ponteiro de interface em um acessório vinculado à modificação de dados.  
  
 Para tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de grande valor, o provedor Native Client OLE DB verifica se há suposições de tamanho de tipo em interfaces **IRowset** e DDL. As colunas com tipos de dados **varchar,** **nvarchar**e **varbinary** com tamanho máximo definido como ilimitado serão representadas como ISLONG através dos conjuntos de linhas de esquema e interfaces que retornam aos tipos de dados da coluna.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB expõe os tipos **varchar(max)**, **varbinary(max)** e **nvarchar(max)** como DBTYPE_STR, DBTYPE_BYTES e DBTYPE_WSTR respectivamente.  
  
 Para trabalhar com esses tipos, um aplicativo tem as seguintes opções:  
  
-   Associar como o tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Se o buffer não for suficientemente grande, ocorrerá truncamento, exatamente como para esses tipos em versões anteriores (embora agora haja valores maiores disponíveis).  
  
-   Associar como o tipo e também especificar DBTYPE_BYREF.  
  
-   Associar como DBTYPE_IUNKNOWN e usar streaming.  
  
 Se associado a DBTYPE_IUNKNOWN, é usada a funcionalidade de fluxo ISequentialStream. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB suporta parâmetros de saída vinculantes como DBTYPE_IUNKNOWN para tipos de dados de grande valor para facilitar cenários em que um procedimento armazenado retorna esses tipos de dados como valores de retorno que serão expostos como DBTYPE_IUNKNOWN ao cliente.  
  
## <a name="storage-object-limitations"></a>Limitações de objetos de armazenamento  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB pode suportar apenas um único objeto de armazenamento aberto. As tentativas de abrir mais de um objeto de armazenamento (para obter uma referência em mais de um ponteiro da interface **ISequentialStream**) retornam DBSTATUS_E_CANTCREATE.  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB, o valor padrão da DBPROP_BLOCKINGSTORAGEOBJECTS propriedade somente leitura é VARIANT_TRUE. Isso indica que se um objeto de armazenamento está ativo, alguns métodos (diferentes daqueles nos objetos de armazenamento) falharão com E_UNEXPECTED.  
  
-   A duração dos dados apresentados por um objeto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazenamento implementado pelo consumidor deve ser conhecida pelo provedor Native Client OLE DB quando o acessório de linha que faz referência ao objeto de armazenamento for criado. O consumidor deve associar um indicador de comprimento na estrutura DBBINDING usada para a criação do acessador.  
  
-   Se uma linha contiver mais de um único grande valor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados e DBPROP_ACCESSORDER não for DBPROPVAL_AO_RANDOM, o consumidor deve usar um conjunto de linhas suportado pelo cursor do provedor DeLE DB para recuperar dados de linha ou processar todos os grandes valores de dados antes de recuperar outros valores de linha. Se DBPROP_ACCESSORDER estiver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROPVAL_AO_RANDOM, o provedor Native Client OLE DB armazena todos os tipos de dados xml como blobs binários grandes para que ele possa ser acessado em qualquer ordem.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Obtendo dados grandes](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [Definindo dados grandes](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [Suporte de transmissão a parâmetros de saída BLOB](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Cliente nativo do servidor SQL &#40;o ledb&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usando tipos de valor grande](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
