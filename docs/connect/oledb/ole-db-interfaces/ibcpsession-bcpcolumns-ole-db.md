---
title: 'Ibcpsession:: BCPColumns (OLE DB) | Microsoft Docs'
description: IBCPSession::BCPColumns (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPColumns (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColumns method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: c66dadc27b4a58e507aa08f0e075d05f17500740
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35304945"
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Define o número de campos que devem ser associados às colunas de uma tabela do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT BCPColumns(   
      DBCOUNTITEM nColumns);  
```  
  
## <a name="remarks"></a>Remarks  
 Internamente, ele chama [ibcpsession:: BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) para definir os valores padrão para dados de campo. Esses valores padrão são obtidos com as informações de coluna do SQL Server que o provedor recupera internamente quando o nome da tabela é especificado por meio de [ibcpsession:: BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md).  
  
> [!NOTE]  
>  Esse método só pode ser chamado depois que **BCPInit** foi chamado com um nome de arquivo válido.  
  
 Você só deve chamar esse método se pretender usar um formato de arquivo de usuário diferente do padrão. Para obter mais informações sobre uma descrição do formato de arquivo de usuário padrão, consulte o método **BCPInit** .  
  
 Depois de chamar o método **BCPColumns** , você precisa chamar o método **BCPColFmt** para cada coluna no arquivo de usuário para definir completamente um formato de arquivo personalizado.  
  
## <a name="arguments"></a>Argumentos  
 *nColumns*[in]  
 O número total de campos no arquivo de usuário. Mesmo se você estiver se preparando para copiar em massa os dados do arquivo de usuário para uma tabela do SQL Server e não pretender copiar todos os campos no arquivo de usuário, ainda assim será necessário definir o argumento *nColumns* como o número total de campos de arquivo de usuário. Os campos ignorados podem ser especificados através de **BCPColFmt**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_FAIL  
 Ocorreu um erro específico do provedor; Para obter informações detalhadas, use o [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) interface.  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o método **BCPInit** não foi chamado antes da chamada desse método. Também ocorre quando esse método é chamado mais de uma vez para uma operação de cópia em massa.  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
## <a name="see-also"></a>Consulte também  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Executando operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
