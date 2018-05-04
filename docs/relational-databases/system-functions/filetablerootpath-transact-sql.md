---
title: FileTableRootPath (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FileTableRootPath_TSQL
- FileTableRootPath
dev_langs:
- TSQL
helpviewer_keywords:
- FileTableRootPath function
ms.assetid: 0cba908a-c85c-4b09-b16a-df1cb333c629
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1c877d75e08662b95f9d22ca55b378ff03aafcec
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="filetablerootpath-transact-sql"></a>FileTableRootPath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o caminho UNC no nível raiz de uma FileTable específica ou do banco de dados atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FileTableRootPath ( [ ‘[schema_name.]FileTable_name’ ], @option )  
```  
  
## <a name="arguments"></a>Argumentos  
 *FileTable_name*  
 O nome da FileTable. *FileTable_name* é do tipo **nvarchar**. Esse é um parâmetro opcional. O valor padrão é o banco de dados atual. Especificando *schema_name* também é opcional. É possível passar NULL *FileTable_name* para usar o valor de parâmetro padrão  
  
 *@option*  
 Uma expressão de inteiro que define como o componente do servidor do caminho deve ser formatado. *@option* Pode ter um dos seguintes valores:  
  
|Value|Descrição|  
|-----------|-----------------|  
|**0**|Retorna o nome do servidor convertido no formato NetBIOS, por exemplo:<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> Este é o valor padrão.|  
|**1**|Retorna o nome do servidor sem conversão, por exemplo:<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|Retorna o caminho completo do servidor, por exemplo:<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>Tipo de retorno  
 **nvarchar(4000)**  
  
 Quando o banco de dados pertence a um grupo de disponibilidade AlwaysOn, então o **FileTableRootPath** função retorna o nome de rede virtual (VNN) em vez do nome do computador.  
  
## <a name="general-remarks"></a>Comentários gerais  
 O **FileTableRootPath** função retorna NULL quando uma das seguintes condições for verdadeira:  
  
-   O valor de *FileTable_name* não é válido.  
  
-   O chamador não tiver permissão suficiente para referenciar a tabela especificada ou o banco de dados atual.  
  
-   A opção FILESTREAM de *database_directory* não está definido para o banco de dados atual.  
  
 Para obter mais informações, consulte [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Para manter código e aplicativos independentes do computador e do banco de dados atuais, evite escrever código baseado em caminhos de arquivo absolutos. Em vez disso, obtenha o caminho completo para um arquivo em tempo de execução usando o **FileTableRootPath** e **GetFileNamespacePath** funções juntas, conforme mostrado no exemplo a seguir. Por padrão, a função **GetFileNamespacePath** retorna o caminho relativo do arquivo sob o caminho raiz do banco de dados.  
  
```sql  
USE MyDocumentDatabase;  
  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
@fullPath = varchar(1000);  
  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath()  
FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 O **FileTableRootPath** função requer:  
  
-   A permissão SELECT no FileTable para obter o caminho raiz de um FileTable específico.  
  
-   **db_datareader** ou permissão mais alta para obter o caminho raiz para o banco de dados atual.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como chamar o **FileTableRootPath** função.  
  
```  
USE MyDocumentDatabase;  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDatabase”  
SELECT FileTableRootPath();  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable”  
SELECT FileTableRootPath(N'dbo.MyFileTable');  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable”  
SELECT FileTableRootPath(N'MyFileTable');  
```  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
