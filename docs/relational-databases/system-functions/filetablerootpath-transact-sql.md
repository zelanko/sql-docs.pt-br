---
title: Funções filetablerootpath (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- FileTableRootPath_TSQL
- FileTableRootPath
dev_langs:
- TSQL
helpviewer_keywords:
- FileTableRootPath function
ms.assetid: 0cba908a-c85c-4b09-b16a-df1cb333c629
author: rothja
ms.author: jroth
ms.openlocfilehash: 10b4aa19b86530213f852ea90f959a1d7ef6c74f
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251232"
---
# <a name="filetablerootpath-transact-sql"></a>FileTableRootPath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o caminho UNC no nível raiz de uma FileTable específica ou do banco de dados atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FileTableRootPath ( [ '[schema_name.]FileTable_name' ], @option )  
```  
  
## <a name="arguments"></a>Argumentos  
 *FileTable_name*  
 O nome da FileTable. *FileTable_name* é do tipo **nvarchar**. Esse é um parâmetro opcional. O valor padrão é o banco de dados atual. A especificação de *schema_name* também é opcional. Você pode passar NULL para *FileTable_name* usar o valor do parâmetro padrão  
  
 *\@option*  
 Uma expressão de inteiro que define como o componente do servidor do caminho deve ser formatado. *\@option* pode ter um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Retorna o nome do servidor convertido no formato NetBIOS, por exemplo:<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> Este é o valor padrão.|  
|**1**|Retorna o nome do servidor sem conversão, por exemplo:<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|Retorna o caminho completo do servidor, por exemplo:<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>Tipo de retorno  
 **nvarchar(4000)**  
  
 Quando o banco de dados pertence a um grupo de disponibilidade Always On, a função **funções filetablerootpath** retorna o VNN (nome da rede virtual) em vez do nome do computador.  
  
## <a name="general-remarks"></a>Comentários gerais  
 A função **funções filetablerootpath** retornará NULL quando uma das seguintes condições for verdadeira:  
  
-   O valor de *FileTable_name* não é válido.  
  
-   O chamador não tiver permissão suficiente para referenciar a tabela especificada ou o banco de dados atual.  
  
-   A opção FILESTREAM de *database_directory* não está definida para o banco de dados atual.  
  
 Para obter mais informações, consulte [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Para manter código e aplicativos independentes do computador e do banco de dados atuais, evite escrever código baseado em caminhos de arquivo absolutos. Em vez disso, obtenha o caminho completo de um arquivo em tempo de execução usando as funções **funções filetablerootpath** e **GetFileNamespacePath** juntas, conforme mostrado no exemplo a seguir. Por padrão, a função **GetFileNamespacePath** retorna o caminho relativo do arquivo sob o caminho raiz do banco de dados.  
  
```sql  
USE MyDocumentDatabase;  
  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
@fullPath = varchar(1000);  
  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath()  
FROM DocumentStore  
WHERE Name = N'document.docx';  
```  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 A função **funções filetablerootpath** requer:  
  
-   A permissão SELECT no FileTable para obter o caminho raiz de um FileTable específico.  
  
-   a permissão **db_datareader** ou superior para obter o caminho raiz do banco de dados atual.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como chamar a função **funções filetablerootpath** .  
  
```  
USE MyDocumentDatabase;  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase"  
SELECT FileTableRootPath();  
  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable"  
SELECT FileTableRootPath(N'dbo.MyFileTable');  
  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable"  
SELECT FileTableRootPath(N'MyFileTable');  
```  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
