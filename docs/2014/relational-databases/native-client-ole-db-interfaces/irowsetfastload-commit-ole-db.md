---
title: IRowsetFastLoad::Commit (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IRowsetFastLoad::Commit (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Commit method
ms.assetid: 19de9128-b91a-4626-847f-af721edaa24e
author: rothja
ms.author: jroth
ms.openlocfilehash: 91b04ff0bffc0dd8905b16271cc7a04085f9bc59
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056199"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
  Marca o término de um lote de linhas inseridas e escreve as linhas na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter exemplos, confira [Copiar Dados em massa usando IRowsetFastLoad &#40;OLE DB&#41;](irowsetfastload-ole-db.md) e [Enviar dados de blob para o SQL Server usando IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT Commit(  
BOOL   
fDone  
);  
  
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
 [IRowsetFastLoad &#40;OLE DB&#41;](irowsetfastload-ole-db.md)  
  
  
