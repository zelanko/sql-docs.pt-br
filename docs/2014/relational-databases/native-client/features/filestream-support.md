---
title: Suporte a FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 407bf9e6816a08af989b18cfeed3a52ee7fa8465
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130322"
---
# <a name="filestream-support"></a>Suporte a FILESTREAM
  FILESTREAM é uma forma de armazenar e acessar valores altos de binário, por meio do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou por acesso direto ao sistema de arquivos do Windows. Um valor binário grande é um valor superior a 2 gigabytes (GB). Para obter mais informações sobre suporte a FILESTREAM aprimorado, consulte [FILESTREAM &#40;SQL Server&#41;](../../blob/filestream-sql-server.md).  
  
 Quando uma conexão de banco de dados for aberta, `@@TEXTSIZE` será definido, por padrão, como -1 ("ilimitado").  
  
 Também é possível acessar e atualizar colunas FILESTREAM usando as APIs do sistema de arquivos do Windows.  
  
 Para obter mais informações, consulte os tópicos a seguir:  
  
-   [Suporte a FILESTREAM &#40;OLE DB&#41;](../ole-db/filestream-support-ole-db.md)  
  
-   [Suporte a FILESTREAM &#40;ODBC&#41;](../odbc/filestream-support-odbc.md)  
  
-   [Acessar dados do FILESTREAM com OpenSqlFilestream](../../blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Consultando colunas FILESTREAM  
 Conjuntos de linhas de esquema no OLE DB não relatarão se uma coluna é uma coluna FILESTREAM. ITableDefinition no OLE DB não pode ser usado para criar uma coluna FILESTREAM.  
  
 Funções de catálogo como SQLColumns no ODBC não relatarão se uma coluna é uma coluna FILESTREAM.  
  
 Para criar colunas FILESTREAM ou detectar quais colunas existentes são colunas FILESTREAM, você pode usar o `is_filestream` coluna o [Columns](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql) exibição do catálogo.  
  
 A seguir, é mostrado um exemplo:  
  
```  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>Compatibilidade com níveis inferiores  
 Se o cliente tiver sido compilado com a versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que estava incluída no [!INCLUDE[ssVersion2005](../../../includes/sscurrent-md.md)], `varbinary(max)` comportamento será compatível com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Ou seja, o tamanho máximo de dados retornados será limitado a 2 GB. Para valores de resultados maiores que 2 GB, ocorrerá truncamento e um aviso de "truncamento à direita dados de cadeia de caracteres" será retornado.  
  
 Quando a compatibilidade de tipo de dados estiver definida como 80, o comportamento do cliente será consistente com o comportamento de clientes de nível inferior.  
  
 Para clientes que usam SQLOLEDB ou outros provedores lançados antes do [!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)] Native Client, `varbinary(max)` será mapeado para imagem.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](sql-server-native-client-features.md)  
  
  
