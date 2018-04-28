---
title: 'Ibcpsession:: Bcpreadfmt (OLE DB) | Microsoft Docs'
description: 'Usando ibcpsession:: Bcpreadfmt para ler dados de um arquivo de formato (OLE DB)'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPReadFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPReadFmt method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4fa9b54be41682c266bb9583473f79dda2efb38
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Lê informações de formato relativas a cada coluna no arquivo de formato.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT BCPReadFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 O método **BCPReadFmt** é usado para ler dados de um arquivo de formato que especifica o formato de dados no arquivo de dados. Este método é capaz de detectar a versão correta do arquivo de formato. Ele pode detectar automaticamente se o arquivo de formato está em xml ou formato de texto de estilo antigo e se comporta adequadamente. As versões de arquivo de formato com suporte pelo Driver OLE DB para SQL Server BCP são versão 6.0 ou mais recente.  
  
 Após o **BCPReadFmt** método lê os valores de formato, fará as chamadas apropriadas para o [ibcpsession:: BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) e [ibcpsession:: BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) métodos. Não há necessidade de o usuário analisar um arquivo de formato e fazer essas chamadas.  
  
 Para salvar um arquivo de formato, chame o [ibcpsession:: Bcpwritefmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) método. As chamadas ao método **BCPReadFmt** podem referenciar formatos salvos. Como alternativa, o utilitário de cópia em massa (**bcp**) pode salvar formatos de dados definidos pelo usuário em arquivos que podem ser referenciados pelo método **BCPReadFmt** .  
  
 O **BCP_OPTION_DELAYREADFMT** valor o *eOption* parâmetro [ibcpsession:: Bcpcontrol](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) modifica o comportamento de ibcpsession:: Bcpreadfmt.  
  
## <a name="arguments"></a>Argumentos  
 *pwszFormatFile*[in]  
 O caminho e o nome do arquivo que contém os valores de formato do arquivo de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_FAIL  
 Ocorreu um erro específico do provedor, para obter informações detalhadas, use o [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) interface.  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o [ibcpsession:: BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) método não foi chamado antes de chamar esse método.  
  
## <a name="see-also"></a>Consulte também  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Executando operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
