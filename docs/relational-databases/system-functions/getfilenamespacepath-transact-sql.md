---
title: GetFileNamespacePath (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- GetFileNamespacePath
- GetFileNamespacePath_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetFileNamespacePath function
ms.assetid: b393ecef-baa8-4d05-a268-b2f309fce89a
author: rothja
ms.author: jroth
ms.openlocfilehash: 42e3cd2c0431a1d23f3d67f7f1e983421b9b1e9a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72278337"
---
# <a name="getfilenamespacepath-transact-sql"></a>GetFileNamespacePath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o caminho UNC de um arquivo ou diretório em uma FileTable.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<column-name>.GetFileNamespacePath(is_full_path, @option)  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome da coluna*  
 O nome da coluna VARBINARY (MAX) **file_stream** em uma filetable.  
  
 O valor de *Column-Name* deve ser um nome de coluna válido. Não pode ser uma expressão ou um valor convertido de uma coluna de outro tipo de dados.  
  
 *is_full_path*  
 Uma expressão de inteiro que especifica se um caminho relativo ou absoluto deve ser retornado. *is_full_path* pode ter um dos seguintes valores:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**0**|Retorna o caminho relativo dentro do diretório no nível do banco de dados.<br /><br /> Este é o valor padrão|  
|**1**|Retorna o caminho UNC completo, a partir do `\\computer_name`.|  
  
 *\@Option*  
 Uma expressão de inteiro que define como o componente do servidor do caminho deve ser formatado. a opção pode ter um dos seguintes valores: * \@*  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**0**|Retorna o nome do servidor convertido no formato NetBIOS, por exemplo:<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> Esse é o valor padrão.|  
|**1**|Retorna o nome do servidor sem conversão, por exemplo:<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|Retorna o caminho completo do servidor, por exemplo:<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>Tipo de retorno  
 **nvarchar(max)**  
  
 Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for clusterizada em um cluster de failover, o nome do computador retornado como parte desse caminho será o nome de host virtual da instância clusterizada.  
  
 Quando o banco de dados pertence a um grupo de disponibilidade Always On, a função **funções filetablerootpath** retorna o VNN (nome da rede virtual) em vez do nome do computador.  
  
## <a name="general-remarks"></a>Comentários gerais  
 O caminho que a função **GetFileNamespacePath** retorna é um caminho de arquivo ou diretório lógico no seguinte formato:  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\...`  
  
 Esse caminho lógico não corresponde diretamente a um caminho NTFS físico. Ele é convertido no caminho físico pelo driver de filtro do sistema de arquivos do FILESTREAM e pelo agente FILESTREAM. Esta separação entre os caminhos lógico e físico permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reorganize dados internamente sem afetar a validade do caminho.  
  
## <a name="best-practices"></a>Práticas Recomendadas  
 Para manter código e aplicativos independentes do computador e do banco de dados atuais, evite escrever código baseado em caminhos de arquivo absolutos. Em vez disso, obtenha o caminho completo de um arquivo em tempo de execução usando as funções **funções filetablerootpath** e **GetFileNamespacePath** juntas, conforme mostrado no exemplo a seguir. Por padrão, a função **GetFileNamespacePath** retorna o caminho relativo do arquivo sob o caminho raiz do banco de dados.  
  
```sql  
USE MyDocumentDatabase;  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
  
@fullPath = varchar(1000);  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath() FROM DocumentStore  
WHERE Name = N'document.docx';  
```  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como chamar a função **GetFileNamespacePath** para obter o caminho UNC para um arquivo ou diretório em uma filetable.  
  
```  
-- returns the relative path of the form "\MyFileTable\MyDocDirectory\document.docx"  
SELECT file_stream.GetFileNamespacePath() AS FilePath FROM DocumentStore  
WHERE Name = N'document.docx';  
  
-- returns "\\MyServer\MSSQLSERVER\MyDocumentDatabase\MyFileTable\MyDocDirectory\document.docx"  
SELECT file_stream.GetFileNamespacePath(1, Null) AS FilePath FROM DocumentStore  
WHERE Name = N'document.docx';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
