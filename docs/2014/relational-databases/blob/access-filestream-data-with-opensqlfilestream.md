---
title: Acessar dados do FILESTREAM com OpenSqlFilestream | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- OpenSqlFilestream
api_location:
- sqlncli11.dll
helpviewer_keywords:
- OpenSqlFilestream
ms.assetid: d8205653-93dd-4599-8cdf-f9199074025f
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 81dab09c293fff8ad4d47df63a7069e48f63d638
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012743"
---
# <a name="access-filestream-data-with-opensqlfilestream"></a>Acessar dados do FILESTREAM com OpenSqlFilestream
  A API OpenSqlFilestream obtém um identificador de arquivo compatível com Win32 para um objeto binário grande FILESTREAM (BLOB) que é armazenado no sistema de arquivos. O identificador pode ser passado para qualquer uma das APIs do Win32: [ReadFile](http://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](http://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](http://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](http://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](http://go.microsoft.com/fwlink/?LinkId=86426)ou [FlushFileBuffers](http://go.microsoft.com/fwlink/?LinkId=86427). Se você passar esse identificador para qualquer outra API do Win32, o erro ERROR_ACCESS_DENIED será retornado. O identificador deve ser fechado passando-o para a API [CloseHandle](http://go.microsoft.com/fwlink/?LinkId=86428) do Win32 antes de a transação ser confirmada ou revertida. O não fechamento do identificador provocará vazamentos de recursos do servidor.  
  
 Acesso ao contêiner todos os dados FILESTREAM deve ser executado em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transação. [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções também podem ser executadas na mesma transação. Isso mantém consistência entre os dados do SQL e dados do BLOB do FILESTREAM.  
  
 Para acessar o BLOB FILESTREAM usando o Win32, a [Autorização do Windows](../security/choose-an-authentication-mode.md) deve estar habilitada.  
  
> [!IMPORTANT]  
>  Quando o arquivo é aberto para acesso de gravação, a transação pertence ao agente de FILESTREAM. Somente a E/S do arquivo do Win32 é permitida até que a transação seja liberada. Para liberar a transação, o identificador de gravação deve ser fechado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
  HANDLE OpenSqlFilestream (  
  LPCWSTR  
  FilestreamPath  
  ,  
  SQL_FILESTREAM_DESIRED_ACCESS  
  DesiredAccess,  
ULONGOpenOptions,LPBYTEFilestreamTransactionContext,SIZE_TFilestreamTransactionContextLength,PLARGE_INTEGERAllocationSize);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *FilestreamPath*  
 [in] É o `nvarchar(max)` caminho retornado pelo [PathName](/sql/relational-databases/system-functions/pathname-transact-sql) função. PathName deve ser chamado a partir do contexto de uma conta que tenha as permissões SELECT ou UPDATE do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na tabela e na coluna FILESTREAM.  
  
 *DesiredAccess*  
 [in] Define o modo usado para acessar dados BLOB do FILESTREAM. Esse valor é passado para a [Função DeviceIoControl](http://go.microsoft.com/fwlink/?LinkId=105527).  
  
|Nome|Valor|Significado|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_READ|0|Os dados podem ser lidos no arquivo.|  
|SQL_FILESTREAM_WRITE|1|Os dados podem ser gravados no arquivo.|  
|SQL_FILESTREAM_READWRITE|2|Os dados podem ser lidos e gravados no arquivo.|  
  
> [!NOTE]  
>  Esses valores são definidos na enumeração SQL_FILESTREAM_DESIRED_ACCESS em sqlncli.h.  
  
 *OpenOptions*  
 [in] Os atributos e sinalizadores do arquivo. Esse parâmetro também pode incluir qualquer combinação dos sinalizadores a seguir.  
  
|Sinalizador|Valor|Significado|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_OPEN_NONE|0x00000000:|O arquivo está sendo aberto ou criado sem opções especiais.|  
|SQL_FILESTREAM_OPEN_FLAG_ASYNC|0x00000001L|O arquivo está sendo aberto ou criado para E/S assíncrona.|  
|SQL_FILESTREAM_OPEN_FLAG_NO_BUFFERING|0x00000002L|O sistema abre o arquivo sem usar cache do sistema.|  
|SQL_FILESTREAM_OPEN_FLAG_NO_WRITE_THROUGH|0x00000004L|O sistema não grava por meio de um cache intermediário. Ele grava direto no disco.|  
|SQL_FILESTREAM_OPEN_FLAG_SEQUENTIAL_SCAN|0x00000008L|Um arquivo é acessado sequencialmente do princípio ao fim. O sistema pode usar isso como uma dica para otimizar o cache de arquivo. Se um aplicativo mover o ponteiro de arquivo para acesso aleatório, a otimização do cache poderá não ocorrer.|  
|SQL_FILESTREAM_OPEN_FLAG_RANDOM_ACCESS|0x00000010L|Um arquivo é acessado aleatoriamente. O sistema pode usar isso como uma dica para otimizar o cache de arquivo.|  
  
 *FilestreamTransactionContext*  
 [in] O valor retornado pela função [GET_FILESTREAM_TRANSACTION_CONTEXT](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql) .  
  
 *FilestreamTransactionContextLength*  
 [in] Número de bytes no `varbinary(max)` dados retornados pela função GET_FILESTREAM_TRANSACTION_CONTEXT. A função retorna uma matriz de N bytes. N é determinado pela função e é uma propriedade da matriz do byte retornada.  
  
 *AllocationSize*  
 [in] Especifica o tamanho de alocação inicial do arquivo de dados em bytes. É ignorado em modo de leitura. Esse parâmetro pode ser NULL, em cujo caso o comportamento do sistema de arquivos padrão é usado.  
  
## <a name="return-value"></a>Valor retornado  
 Se a função tiver êxito, o valor de retorno será um identificador aberto para um arquivo especificado. Se houver falha na função, o valor de retorno será INVALID_HANDLE_VALUE. Para obter informações sobre erros estendidos, chame GetLastError().  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como usar a API `OpenSqlFilestream` para obter um identificador de Win32.  
  
 [!code-csharp[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cs/filestream.cs#fs_cs_readandwriteblob)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/vb/filestream.vb#fs_vb_readandwriteblob)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_writeblob)]  
  
## <a name="remarks"></a>Remarks  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client deve ser instalado para usar essa API. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client é instalado com ferramentas de cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Instalando o SQL Server Native Client](../native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="see-also"></a>Consulte também  
 [Objeto binário grande &#40;Blob&#41; Dados &#40;SQL Server&#41;](binary-large-object-blob-data-sql-server.md)   
 [Fazer atualizações parciais em dados do FILESTREAM](make-partial-updates-to-filestream-data.md)   
 [Evitar conflitos com operações de banco de dados em aplicativos de FILESTREAM](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
