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
ms.openlocfilehash: 01bb3af0f1c8e28cfe6002286ed6a2094dff1a50
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760606"
---
# <a name="blobs-and-ole-objects"></a>BLOBs e objetos OLE
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo expõe a interface **ISequentialStream** para dar suporte ao acesso de consumidor aos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados **ntext**, **Text**, **Image**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)** e XML como BLOBs (objetos binários grandes). O método **Read** em **ISequentialStream** permite que o consumidor recupere muitos dados em partes gerenciáveis.  
  
 Para obter um exemplo que demonstra esse recurso, confira [Definir &#40;OLE DB&#41; de dados grandes](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo pode usar uma interface **IStorage** implementada pelo consumidor quando o consumidor fornece o ponteiro de interface em um acessador associado para modificação de dados.  
  
 Para tipos de dados de valor grande, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo verifica se há suposições de tamanho de tipo nas interfaces **IROWSET** e DDL. Colunas com tipos de dados **varchar**, **nvarchar**e **varbinary** com tamanho máximo definido como ilimitado serão representadas como isduras por meio de conjuntos de linhas de esquema e interfaces que retornam tipos de dados de coluna.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo expõe os tipos **varchar (max)**, **varbinary (max)** e **nvarchar (max)** como DBTYPE_STR, DBTYPE_BYTES e DBTYPE_WSTR, respectivamente.  
  
 Para trabalhar com esses tipos, um aplicativo tem as seguintes opções:  
  
-   Associar como o tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Se o buffer não for suficientemente grande, ocorrerá truncamento, exatamente como para esses tipos em versões anteriores (embora agora haja valores maiores disponíveis).  
  
-   Associar como o tipo e também especificar DBTYPE_BYREF.  
  
-   Associar como DBTYPE_IUNKNOWN e usar streaming.  
  
 Se associado a DBTYPE_IUNKNOWN, é usada a funcionalidade de fluxo ISequentialStream. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte à associação de parâmetros de saída como DBTYPE_IUNKNOWN para tipos de dados de valor grande para facilitar cenários em que um procedimento armazenado retorna esses tipos de dados como valores de retorno que serão expostos como DBTYPE_IUNKNOWN ao cliente.  
  
## <a name="storage-object-limitations"></a>Limitações de objetos de armazenamento  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo pode dar suporte a apenas um único objeto de armazenamento aberto. As tentativas de abrir mais de um objeto de armazenamento (para obter uma referência em mais de um ponteiro da interface **ISequentialStream**) retornam DBSTATUS_E_CANTCREATE.  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo, o valor padrão da propriedade DBPROP_BLOCKINGSTORAGEOBJECTS somente leitura é VARIANT_TRUE. Isso indica que se um objeto de armazenamento está ativo, alguns métodos (diferentes daqueles nos objetos de armazenamento) falharão com E_UNEXPECTED.  
  
-   O comprimento dos dados apresentados por um objeto de armazenamento implementado pelo consumidor deve ser conhecido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo quando o acessador de linha que faz referência ao objeto de armazenamento é criado. O consumidor deve associar um indicador de comprimento na estrutura DBBINDING usada para a criação do acessador.  
  
-   Se uma linha contiver mais de um único valor de dados grandes e DBPROP_ACCESSORDER não for DBPROPVAL_AO_RANDOM, o consumidor deverá usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de linhas com suporte do cursor do provedor de OLE DB de cliente nativo para recuperar dados de linha ou processar todos os valores de dados grandes antes de recuperar outros valores de linha. Se DBPROP_ACCESSORDER for DBPROPVAL_AO_RANDOM, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo armazenará em cache todos os tipos de dados XML como BLOBs (objetos binários grandes) para que possam ser acessados em qualquer ordem.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Obtendo dados grandes](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [Definindo dados grandes](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [Suporte de transmissão a parâmetros de saída BLOB](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usando tipos de valor grande](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
