---
title: BLOBs e objetos OLE | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-blobs
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
caps.latest.revision: 43
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9f5ec924883f046991c9eba6e62c79b9bec7a6fc
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707274"
---
# <a name="blobs-and-ole-objects"></a>BLOBs e objetos OLE
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client expõe a **ISequentialStream** interface para dar suporte ao acesso do consumidor para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**, **texto**, **imagem**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, e tipos de dados de xml binários como BLOBs (objetos grandes). O **leitura** método **ISequentialStream** permite que o consumidor recupere muitos dados em partes gerenciáveis.  
  
 Para obter um exemplo que demonstra esse recurso, consulte [do conjunto de dados grande &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client pode usar um consumidor implementado **IStorage** interface quando o consumidor fornece o ponteiro de interface em um acessador associado para modificação de dados.  
  
 Para tipos de dados de valor grande, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client verifica suposições de tamanho do tipo em **IRowset** e interfaces DDL. Colunas com **varchar**, **nvarchar**, e **varbinary** tipos de dados com tamanho máximo definido como ilimitado serão representados como ISLONG por meio de conjuntos de linhas de esquema e interfaces que retornam tipos de dados de coluna.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client expõe a **varchar (max)**, **varbinary (max)** e **nvarchar (max)** tipos como DBTYPE_STR, DBTYPE_BYTES e DBTYPE_WSTR, respectivamente.  
  
 Para trabalhar com esses tipos de um aplicativo tem as seguintes opções:  
  
-   Associar como o tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Se o buffer não for suficientemente grande, ocorrerá truncamento, exatamente como para esses tipos em versões anteriores (embora agora haja valores maiores disponíveis).  
  
-   Associar como o tipo e também especificar DBTYPE_BYREF.  
  
-   Associar como DBTYPE_IUNKNOWN e usar streaming.  
  
 Se associado a DBTYPE_IUNKNOWN, é usada a funcionalidade de fluxo ISequentialStream. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client oferece suporte à associação de parâmetros de saída como DBTYPE_IUNKNOWN para tipos de dados de valor grande facilitar cenários onde um procedimento armazenado retorna esses dados tipos como valores de retorno que serão expostos como DBTYPE_IUNKNOWN para o cliente.  
  
## <a name="storage-object-limitations"></a>Limitações de objetos de armazenamento  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client pode dar suporte a apenas um objeto de armazenamento aberto único. As tentativas de abrir mais de um objeto de armazenamento (para obter uma referência em mais de um **ISequentialStream** ponteiro de interface) retornam DBSTATUS_E_CANTCREATE.  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider, o valor padrão da propriedade somente leitura DBPROP_BLOCKINGSTORAGEOBJECTS é VARIANT_TRUE. Isso indica que se um objeto de armazenamento está ativo, alguns métodos (diferentes daqueles nos objetos de armazenamento) falharão com E_UNEXPECTED.  
  
-   O comprimento dos dados apresentados por um objeto de armazenamento implementado pelo consumidor deve ser feito conhecido para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client quando o acessador de linha que faz referência ao objeto de armazenamento é criado. O consumidor deve associar um indicador de comprimento na estrutura DBBINDING usada para a criação do acessador.  
  
-   Se uma linha contiver mais de um valor único de dados grande e DBPROP_ACCESSORDER não for DBPROPVAL_AO_RANDOM, o consumidor deve usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB linhas com suporte de cursor do provedor para recuperar dados de linha ou processar todos os valores de dados grandes antes de recuperar outros valores de linha. Se DBPROP_ACCESSORDER for DBPROPVAL_AO_RANDOM, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider armazena em cache todos os tipos de dados xml como objetos binários grandes (BLOBs) para que ele possa ser acessado em qualquer ordem.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Obtendo dados grandes](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [Configurando dados grandes](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [Suporte de streaming para parâmetros de saída BLOB](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usando tipos de valor grande](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
