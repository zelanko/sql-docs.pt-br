---
description: 'IRowsetFastLoad:: Commit (provedor de OLE DB de cliente nativo)'
title: 'IRowsetFastLoad:: Commit (provedor de OLE DB de cliente nativo) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
ms.assetid: 19de9128-b91a-4626-847f-af721edaa24e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 152ae0916dd5d01bc72526a5ef2494bc6bb04e93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455640"
---
# <a name="irowsetfastloadcommit-native-client-ole-db-provider"></a>IRowsetFastLoad:: Commit (provedor de OLE DB de cliente nativo)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Marca o término de um lote de linhas inseridas e escreve as linhas na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter exemplos, confira [Copiar Dados em massa usando IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) e [Enviar dados de blob para o SQL Server usando IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT Commit(  
      BOOL fDone);  
```  
  
## <a name="arguments"></a>Argumentos  
 *fDone*[in]  
 Se FALSE, o conjunto de linhas manterá validade e poderá ser usado pelo consumidor para inserção de linha adicional. Caso seja TRUE, o conjunto de linhas perde validade e nenhuma inserção adicional pode ser feita pelo consumidor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método teve êxito e todos os dados inseridos foram escritos na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 E_FAIL  
 Ocorreu um erro específico de provedor. Recupere informações de erro para o texto de erro específico do provedor.  
  
 E_UNEXPECTED  
 O método foi chamado em um conjunto de linhas de cópia em massa invalidado anteriormente pelo método **IRowsetFastLoad::Commit**.  
  
## <a name="remarks"></a>Comentários  
 Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de linhas de cópia em massa do provedor de OLE DB de cliente nativo se comporta como um conjunto de linhas de modo de atualização atrasada. Conforme o usuário insere dados de linha pelo conjunto de linhas, as linhas inseridas são tratadas da mesma forma que as inserções pendentes em um conjunto de linhas que dá suporte a **IRowsetUpdate**.  
  
 O consumidor deve chamar o método **Commit** no conjunto de linhas de cópia em massa para gravar as linhas inseridas na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da mesma forma que o método **IRowsetUpdate::Update** é usado para enviar linhas pendentes para uma instância do SQL Server.  
  
 Caso o consumidor libere a referência no conjunto de linhas de cópia em massa sem chamar o método **Commit**, todas as linhas inseridas não gravadas previamente serão perdidas.  
  
 O consumidor pode processar em lotes as linhas inseridas chamando o método **Commit** com o argumento *fDone* definido como FALSE. Quando *fDone* é definido como TRUE, o conjunto de linhas se torna inválido. Um conjunto de linhas de cópia em massa inválido dá suporte apenas à interface **ISupportErrorInfo** e ao método **IRowsetFastLoad::Release**.  
  
## <a name="see-also"></a>Consulte Também  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
