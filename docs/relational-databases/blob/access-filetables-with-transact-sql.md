---
title: Acessar FileTables com Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with T-SQL
ms.assetid: 3c4a5ffb-c521-4696-99cb-2b03cffc9c02
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 622bbe1c2d2d4f564ad6fff72fee4e286287a8f2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47844494"
---
# <a name="access-filetables-with-transact-sql"></a>Acessar FileTables com Transact-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Descreve como os comandos DML (linguagem de manipulação de dados) do [!INCLUDE[tsql](../../includes/tsql-md.md)] funcionam em FileTables.  
  
##  <a name="BasicsInsert"></a> Operações INSERT em FileTables  
 As considerações a seguir se aplicam a operações **INSERT** em FileTables:  
  
-   Todas as colunas de atributo de arquivo têm restrições NOT NULL. Se não forem definidos valores explicitamente, então serão fornecidos valores padrão apropriados.  
  
-   Serão impostas restrições definidas pelo sistema se a instrução INSERT definir **name**, **path_locator**, **parent_path_locator** ou atributos de arquivos.  
  
-   O aplicativo pode obter o **path_locator** para um arquivo ou diretório fornecendo o caminho do sistema de arquivos à função [GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md).  
  
##  <a name="BasicsUpdate"></a> Operações UPDATE em FileTables  
 As considerações a seguir se aplicam a operações **UPDATE** em FileTables:  
  
-   São permitidas atualizações em quaisquer dados definidos pelo usuário.  
  
-   Serão impostas restrições definidas pelo sistema se a instrução INSERT definir **name**, **path_locator**, **parent_path_locator**ou atributos de arquivos.  
  
-   Podem ser feitas atualizações nos dados FILESTREAM da coluna **file_stream** sem afetar nenhuma outra coluna, incluindo os carimbos de data/hora.  
  
##  <a name="BasicsDelete"></a> Operações DELETE em FileTables  
 As considerações a seguir se aplicam a operações **DELETE** em FileTables:  
  
-   A exclusão de uma linha remove o arquivo ou diretório correspondente do sistema de arquivos.  
  
-   A exclusão de uma linha não funcionará se a linha corresponder a um diretório que contém outros arquivos ou diretórios.  
  
##  <a name="BasicsConstraints"></a> Restrições que são impostas para operações DML em FileTables  
 As restrições definidas pelo sistema garante que as ações DML não comprometem a integridade da hierarquia de namespaces de arquivo. Estas são as restrições impostas:  
  
-   Quando você define ou altera o **nome** do arquivo ou diretório:  
  
    -   As convenções de nomenclatura de arquivo e diretório do Windows são impostas.  
  
    -   A exclusividade do nome no diretório pai é imposta.  
  
-   Quando você define ou altera o local de um arquivo ou diretório definindo ou alterando o **path_locator** ou **parent_path_locator**:  
  
    -   A exclusividade é imposta.  
  
    -   A consistência da árvore hierárquica de diretórios e arquivos é imposta, incluindo a consistência dos valores **path_locator** e **parent_path_locator** .  
  
-   O valor de **is_directory** não pode ser definido como true quando uma coluna **file_stream** não é nula. Os dados na coluna **file_stream** indicam que a linha representa um arquivo, e não um diretório.  
  
-   As colunas de atributo de arquivo não podem ser nulas. As restrições NOT NULL são impostas com valores padrão.  
  
-   O valor de **last_access_time** não pode ser anterior a **last_write_time** e **creation_time**.  
  
## <a name="see-also"></a>Consulte Também  
 [Carregar arquivos em FileTables](../../relational-databases/blob/load-files-into-filetables.md)   
 [Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [Acessar FileTables com APIs de entrada e saída de arquivo](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)   
 [DDL, funções, procedimentos armazenados e exibições de FileTable](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
