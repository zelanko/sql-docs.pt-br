---
description: 'IBCPSession:: BCPColumns (provedor de OLE DB de cliente nativo)'
title: 'IBCPSession:: BCPColumns (provedor de OLE DB de cliente nativo) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IBCPSession::BCPColumns (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColumns method
ms.assetid: c338abe8-9e30-4853-a7c6-b1a6c00095e1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0e912bf8e1a7ef3d9bf620799f73ec120eca51bb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476077"
---
# <a name="ibcpsessionbcpcolumns-native-client-ole-db-provider"></a>IBCPSession:: BCPColumns (provedor de OLE DB de cliente nativo)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Define o número de campos que devem ser associados às colunas de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT BCPColumns(   
      DBCOUNTITEM nColumns);  
```  
  
## <a name="remarks"></a>Comentários  
 Internamente, ele chama [IBCPSession::BCPColFmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) para definir os valores padrão para dados de campo. Esses valores padrão são obtidos nas informações de coluna do SQL Server que o provedor recupera internamente quando o nome da tabela é especificado por meio de [IBCPSession::BCPInit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md).  
  
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
 Um erro específico do provedor ocorreu. Para obter informações detalhadas, use a interface [ISQLServerErrorInfo](isqlservererrorinfo-geterrorinfo-ole-db.md).  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o método **BCPInit** não foi chamado antes da chamada desse método. Também ocorre quando esse método é chamado mais de uma vez para uma operação de cópia em massa.  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
## <a name="see-also"></a>Consulte Também  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [Executando operações de cópia em massa](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
