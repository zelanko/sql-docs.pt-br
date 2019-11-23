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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b4e284d2086684af232c17b59675b834b26f497b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790633"
---
# <a name="blobs-and-ole-objects"></a>BLOBs e objetos OLE
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client expõe a interface **ISequentialStream** para dar suporte ao acesso do consumidor a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**, **Text**, **Image**, **varchar (max)** , **nvarchar (max)** , **varbinary (max)** e tipos de dados XML como BLOBs (objetos binários grandes). O método **Read** em **ISequentialStream** permite que o consumidor recupere muitos dados em partes gerenciáveis.  
  
 Para obter um exemplo que demonstra esse recurso, consulte [set Large &#40;data&#41;OLE DB](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md).  
  
 O provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar uma interface **IStorage** implementada pelo consumidor quando o consumidor fornece o ponteiro de interface em um acessador associado para modificação de dados.  
  
 Para tipos de dados de valor grande, o provedor de OLE DB do cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifica se há suposições de tamanho de tipo em interfaces **IRowset** e DDL. Colunas com tipos de dados **varchar**, **nvarchar**e **varbinary** com tamanho máximo definido como ilimitado serão representadas como isduras por meio de conjuntos de linhas de esquema e interfaces que retornam tipos de dados de coluna.  
  
 O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client expõe os tipos **varchar (max)** , **varbinary (max)** e **nvarchar (max)** como DBTYPE_STR, DBTYPE_BYTES e DBTYPE_WSTR, respectivamente.  
  
 Para trabalhar com esses tipos, um aplicativo tem as seguintes opções:  
  
-   Associar como o tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Se o buffer não for suficientemente grande, ocorrerá truncamento, exatamente como para esses tipos em versões anteriores (embora agora haja valores maiores disponíveis).  
  
-   Associar como o tipo e também especificar DBTYPE_BYREF.  
  
-   Associar como DBTYPE_IUNKNOWN e usar streaming.  
  
 Se associado a DBTYPE_IUNKNOWN, é usada a funcionalidade de fluxo ISequentialStream. O provedor de OLE DB de cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à associação de parâmetros de saída como DBTYPE_IUNKNOWN para tipos de dados de valor grande para facilitar cenários em que um procedimento armazenado retorna esses tipos de dados como valores de retorno que serão expostos como DBTYPE_IUNKNOWN para o cliente.  
  
## <a name="storage-object-limitations"></a>Limitações de objetos de armazenamento  
  
-   O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pode dar suporte a apenas um único objeto de armazenamento aberto. As tentativas de abrir mais de um objeto de armazenamento (para obter uma referência em mais de um ponteiro da interface **ISequentialStream**) retornam DBSTATUS_E_CANTCREATE.  
  
-   No provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, o valor padrão da propriedade somente leitura DBPROP_BLOCKINGSTORAGEOBJECTS é VARIANT_TRUE. Isso indica que se um objeto de armazenamento está ativo, alguns métodos (diferentes daqueles nos objetos de armazenamento) falharão com E_UNEXPECTED.  
  
-   O comprimento dos dados apresentados por um objeto de armazenamento implementado pelo consumidor deve ser conhecido pelo provedor de OLE DB do cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando o acessador de linha que faz referência ao objeto de armazenamento é criado. O consumidor deve associar um indicador de comprimento na estrutura DBBINDING usada para a criação do acessador.  
  
-   Se uma linha contiver mais de um único valor de dados grandes e DBPROP_ACCESSORDER não for DBPROPVAL_AO_RANDOM, o consumidor deverá usar um conjunto de linhas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente nativo OLE DB do provedor para recuperar dados de linha ou processar todos os valores de dados grandes antes de recuperar outros valores de linha. Se DBPROP_ACCESSORDER for DBPROPVAL_AO_RANDOM, o provedor de OLE DB do cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazenará em cache todos os tipos de dados XML como BLOBs (objetos binários grandes) para que possam ser acessados em qualquer ordem.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Obtendo dados grandes](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [Configurando dados grandes](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [Suporte de streaming para parâmetros de saída BLOB](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41; ](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usando tipos de valor grande](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
