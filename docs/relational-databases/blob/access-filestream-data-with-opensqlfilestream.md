---
title: Acessar dados do FILESTREAM com OpenSqlFilestream | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: blob
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
apiname: OpenSqlFilestream
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: OpenSqlFilestream
ms.assetid: d8205653-93dd-4599-8cdf-f9199074025f
caps.latest.revision: "47"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7952076c536818d8a272a6eed35566c3e413ed21
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="access-filestream-data-with-opensqlfilestream"></a>Acessar dados do FILESTREAM com OpenSqlFilestream
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A API OpenSqlFilestream obtém um identificador de arquivo compatível com Win32 para um objeto binário grande (BLOB) FILESTREAM armazenado no sistema de arquivos. O identificador pode ser passado para qualquer uma das APIs do Win32: [ReadFile](http://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](http://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](http://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](http://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](http://go.microsoft.com/fwlink/?LinkId=86426)ou [FlushFileBuffers](http://go.microsoft.com/fwlink/?LinkId=86427). Se você passar esse identificador para qualquer outra API do Win32, o erro ERROR_ACCESS_DENIED será retornado. O identificador deve ser fechado passando-o para a API [CloseHandle](http://go.microsoft.com/fwlink/?LinkId=86428) do Win32 antes de a transação ser confirmada ou revertida. O não fechamento do identificador provocará vazamentos de recursos do servidor.  
  
 Você deve executar todo o acesso ao contêiner de dados FILESTREAM em uma transação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções também podem ser executadas na mesma transação. Isso mantém consistência entre os dados do SQL e dados do BLOB do FILESTREAM.  
  
 Para acessar o BLOB FILESTREAM usando o Win32, a [Autorização do Windows](../../relational-databases/security/choose-an-authentication-mode.md) deve estar habilitada.  
  
> [!IMPORTANT]  
>  Quando o arquivo é aberto para acesso de gravação, a transação pertence ao agente de FILESTREAM. Somente a E/S do arquivo do Win32 é permitida até que a transação seja liberada. Para liberar a transação, o identificador de gravação deve ser fechado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HANDLE OpenSqlFilestream (  
    LPCWSTR FilestreamPath,  
    SQL_FILESTREAM_DESIRED_ACCESS DesiredAccess,  
    ULONG OpenOptions,  
    LPBYTE FilestreamTransactionContext,  
    SIZE_T FilestreamTransactionContextLength,  
    PLARGE_INTEGER AllocationSize);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *FilestreamPath*  
 [in] É o caminho **nvarchar(max)** retornado pela função [PathName](../../relational-databases/system-functions/pathname-transact-sql.md) . PathName deve ser chamado a partir do contexto de uma conta que tenha as permissões SELECT ou UPDATE do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na tabela e na coluna FILESTREAM.  
  
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
 [in] O valor retornado pela função [GET_FILESTREAM_TRANSACTION_CONTEXT](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) .  
  
 *FilestreamTransactionContextLength*  
 [in] Número de bytes nos dados **varbinary(max)** retornados pela função GET_FILESTREAM_TRANSACTION_CONTEXT. A função retorna uma matriz de N bytes. N é determinado pela função e é uma propriedade da matriz do byte retornada.  
  
 *AllocationSize*  
 [in] Especifica o tamanho de alocação inicial do arquivo de dados em bytes. É ignorado em modo de leitura. Esse parâmetro pode ser NULL, em cujo caso o comportamento do sistema de arquivos padrão é usado.  
  
## <a name="return-value"></a>Valor de retorno  
 Se a função tiver êxito, o valor de retorno será um identificador aberto para um arquivo especificado. Se houver falha na função, o valor de retorno será INVALID_HANDLE_VALUE. Para obter informações sobre erros estendidos, chame GetLastError().  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como usar a API `OpenSqlFilestream` para obter um identificador de Win32.  
  
 [!code-cs[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/csharp/access-filestream-data-w_0_1.cs)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/visualbasic/access-filestream-data-w_0_2.vb)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../relational-databases/blob/codesnippet/cpp/access-filestream-data-w_0_3.cpp)]  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client deve ser instalado para usar essa API. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client é instalado com ferramentas de cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Instalando o SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="see-also"></a>Consulte também  
 [Objeto binário grande &#40;Blob&#41; Dados &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [Fazer atualizações parciais em dados do FILESTREAM](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)   
 [Evitar conflitos com operações de banco de dados em aplicativos de FILESTREAM](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
