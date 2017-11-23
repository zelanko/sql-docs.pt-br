---
title: GetFileNamespacePath (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetFileNamespacePath
- GetFileNamespacePath_TSQL
dev_langs: TSQL
helpviewer_keywords: GetFileNamespacePath function
ms.assetid: b393ecef-baa8-4d05-a268-b2f309fce89a
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e2f2e898438a6d8ce613aab6960f0472c32a55e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="getfilenamespacepath-transact-sql"></a>GetFileNamespacePath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o caminho UNC de um arquivo ou diretório em uma FileTable.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até a [versão atual](http://msdn.microsoft.com/library/bb500435.aspx)).|  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<column-name>.GetFileNamespacePath(is_full_path, @option)  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome da coluna*  
 O nome da coluna do varbinary (max) **file_stream** coluna em uma FileTable.  
  
 O *nome de coluna* valor deve ser um nome de coluna válido. Não pode ser uma expressão ou um valor convertido de uma coluna de outro tipo de dados.  
  
 *is_full_path*  
 Uma expressão de inteiro que especifica se um caminho relativo ou absoluto deve ser retornado. *is_full_path* pode ter um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Retorna o caminho relativo dentro do diretório no nível do banco de dados.<br /><br /> Esse é o valor padrão.|  
|**1**|Retorna o caminho UNC completo, a partir do `\\computer_name`.|  
  
 *@option*  
 Uma expressão de inteiro que define como o componente do servidor do caminho deve ser formatado. *@option*pode ter um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Retorna o nome do servidor convertido no formato NetBIOS, por exemplo:<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDB`<br /><br /> Este é o valor padrão.|  
|**1**|Retorna o nome do servidor sem conversão, por exemplo:<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDB`|  
|**2**|Retorna o caminho completo do servidor, por exemplo:<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDB`|  
  
## <a name="return-type"></a>Tipo de retorno  
 **nvarchar(max)**  
  
 Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for clusterizada em um cluster de failover, o nome do computador retornado como parte desse caminho será o nome de host virtual da instância clusterizada.  
  
 Quando o banco de dados pertence a um grupo de disponibilidade AlwaysOn, então o **FileTableRootPath** função retorna o nome de rede virtual (VNN) em vez do nome do computador.  
  
## <a name="general-remarks"></a>Comentários gerais  
 O caminho que o **GetFileNamespacePath** função retorna um caminho de diretório ou arquivo lógico no seguinte formato:  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\...`  
  
 Esse caminho lógico não corresponde diretamente a um caminho NTFS físico. Ele é convertido no caminho físico pelo driver de filtro do sistema de arquivos do FILESTREAM e pelo agente de FILESTREAM. Esta separação entre os caminhos lógico e físico permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reorganize dados internamente sem afetar a validade do caminho.  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Para manter código e aplicativos independentes do computador e do banco de dados atuais, evite escrever código baseado em caminhos de arquivo absolutos. Em vez disso, obtenha o caminho completo para um arquivo em tempo de execução usando o **FileTableRootPath** e **GetFileNamespacePath** funções juntas, conforme mostrado no exemplo a seguir. Por padrão, a função **GetFileNamespacePath** retorna o caminho relativo do arquivo sob o caminho raiz do banco de dados.  
  
```tsql  
USE MyDocumentDB;  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
  
@fullPath = varchar(1000);  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath() FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como chamar o **GetFileNamespacePath** função para obter o caminho UNC para um arquivo ou diretório em uma FileTable.  
  
```  
-- returns the relative path of the form “\MyFileTable\MyDocDirectory\document.docx”  
SELECT file_stream.GetFileNamespacePath() AS FilePath FROM DocumentStore  
WHERE Name = N’document.docx’;  
  
-- returns “\\MyServer\MSSQLSERVER\MyDocumentDB\MyFileTable\MyDocDirectory\document.docx”  
SELECT file_stream.GetFileNamespacePath(1, Null) AS FilePath FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
