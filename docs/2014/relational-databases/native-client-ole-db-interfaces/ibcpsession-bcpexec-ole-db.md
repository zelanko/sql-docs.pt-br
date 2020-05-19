---
title: IBCPSession::BCPExec (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPExec (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPExec method
ms.assetid: 0f4ebb63-cf03-4e53-846e-6c3021cde007
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5695ef3c8a049ef3b6dd75c78648be8eb3a8916b
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82695467"
---
# <a name="ibcpsessionbcpexec-ole-db"></a>IBCPSession::BCPExec (OLE DB)
  Executa a operação de cópia em massa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT BCPExec(   
DBROWCOUNT *pRowsCopied);  
```  
  
## <a name="remarks"></a>Comentários  
 O método **BCPExec** copia os dados de um arquivo de usuário para uma tabela de banco de dados ou vice-versa, dependendo do valor do parâmetro *eDirection* usado com o método [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md).  
  
 Antes de chamar **BCPExec**, chame o método **BCPInit** com um nome de arquivo de usuário válido. Caso isso não seja feito, será gerado um erro. A única exceção será se uma consulta for usada para uma operação de cópia em massa. Nesse caso, especifique NULL para o nome da tabela no método **BCPInit** e, depois, especifique a consulta usando a opção BCP_OPTION_HINTS.  
  
 O método **BCPExec** é o único método de cópia em massa que provavelmente permanecerá pendente durante qualquer intervalo de tempo. Ele é, portanto, o único método de cópia em massa que oferece suporte ao modo assíncrono. Para usar o modo assíncrono, defina a propriedade de sessão SSPROP_ASYNCH_BULKCOPY específica do provedor como VARIANT_TRUE antes de chamar o método **BCPExec** . Essa propriedade está disponível no conjunto de propriedades DBPROPSET_SQLSERVERSESSION. Para testar a conclusão, chame o método **BCPExec** com os mesmos parâmetros. Se a cópia em massa ainda não estiver concluída, o método **BCPExec** retornará DB_S_ASYNCHRONOUS. Ele também retornará, no argumento *pRowsCopied* , uma contagem de status do número de linhas que foram enviadas para o servidor ou recebidas dele. As linhas enviadas para o servidor não serão confirmadas até que o fim de um lote seja atingido.  
  
## <a name="arguments"></a>Argumentos  
 *pRowsCopied*[out]  
 Um ponteiro para uma DWORD. O método **BCPExec** preenche a método com o número de linhas copiadas com êxito. Se o argumento *pRowsCopied* for definido como NULL, ele será ignorado pelo método **BCPExec** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_FAIL  
 Ocorreu um erro específico do provedor; para obter informações detalhadas, use a interface [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) .  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o método **BCPInit** não foi chamado antes da chamada desse método. Também ocorrerá se a operação for anulada com a opção BCP_OPTION_ABORT e o método **BCPExec** for chamado depois.  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
 DB_S_ENDOFROWSET  
 A operação de cópia em massa terminou e toda a transferência de dados foi concluída.  
  
 DB_S_ASYNCHRONOUS  
 O lote atual de linhas foi copiado. Chame o método **BCPExec** novamente para transferir o próximo lote.  
  
 DB_S_ERRORSOCCURRED  
 Ocorreram erros durante a operação de cópia em massa e algumas linhas podem não ter sido copiadas. O número de erros ainda é menor do que o máximo de erros permitido.  
  
## <a name="see-also"></a>Consulte Também  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Executando operações de cópia em massa](../native-client/features/performing-bulk-copy-operations.md)  
  
  
