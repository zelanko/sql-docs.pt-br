---
title: IBCPSession::BCPColumns (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPColumns (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPColumns method
ms.assetid: c338abe8-9e30-4853-a7c6-b1a6c00095e1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f18437b807c9cc45b54841255d2b7bb4ba98b45c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82695745"
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns (OLE DB)
  Define o número de campos que devem ser associados às colunas de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT BCPColumns(   
DBCOUNTITEMnColumns);  
```  
  
## <a name="remarks"></a>Comentários  
 Internamente, ele chama [IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) para definir os valores padrão para dados de campo. Esses valores padrão são obtidos nas informações de coluna do SQL Server que o provedor recupera internamente quando o nome da tabela é especificado por meio de [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md).  
  
> [!NOTE]  
>   Esse método só pode ser chamado depois que **BCPInit** foi chamado com um nome de arquivo válido.  
  
 Você só deve chamar esse método se pretender usar um formato de arquivo de usuário diferente do padrão. Para obter mais informações sobre uma descrição do formato de arquivo de usuário padrão, consulte o método **BCPInit** .  
  
 Depois de chamar o método **BCPColumns** , você precisa chamar o método **BCPColFmt** para cada coluna no arquivo de usuário para definir completamente um formato de arquivo personalizado.  
  
## <a name="arguments"></a>Argumentos  
 *nColumns*[in]  
 O número total de campos no arquivo de usuário. Mesmo se você estiver se preparando para copiar em massa os dados do arquivo de usuário para uma tabela do SQL Server e não pretender copiar todos os campos no arquivo de usuário, ainda assim será necessário definir o argumento *nColumns* como o número total de campos de arquivo de usuário. Os campos ignorados podem ser especificados através de **BCPColFmt**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_FAIL  
 Ocorreu um erro específico do provedor; para obter informações detalhadas, use a interface [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) .  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o método **BCPInit** não foi chamado antes da chamada desse método. Também ocorre quando esse método é chamado mais de uma vez para uma operação de cópia em massa.  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
## <a name="see-also"></a>Consulte Também  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Executando operações de cópia em massa](../native-client/features/performing-bulk-copy-operations.md)  
  
  
