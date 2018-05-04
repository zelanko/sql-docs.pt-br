---
title: Suporte a FILESTREAM | Microsoft Docs
description: Suporte FILESTREAM no Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server [FILESTREAM support]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: c5de3b444ab28911875e65d581e836c16eadd528
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="filestream-support"></a>Suporte a FILESTREAM
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Começando com [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], OLE DB Driver para SQL Server dá suporte ao recurso FILESTREAM aprimorado. Para obter exemplos, consulte [Filestream e BD OLE](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md).  

FILESTREAM é uma forma de armazenar e acessar valores altos de binário, por meio do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou por acesso direto ao sistema de arquivos do Windows. Um valor binário grande é um valor superior a 2 gigabytes (GB). Para obter mais informações sobre suporte a FILESTREAM aprimorado, consulte [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md).  
  
Quando uma conexão de banco de dados é aberto, **@@TEXTSIZE**  será definido como -1 ("ilimitado"), por padrão.  
  
Também é possível acessar e atualizar colunas FILESTREAM usando as APIs do sistema de arquivos do Windows.  
  
Para obter mais informações, consulte [acessar dados FILESTREAM com OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Consultando colunas FILESTREAM  
Conjuntos de linhas de esquema no OLE DB não relatarão se uma coluna é uma coluna FILESTREAM. ITableDefinition no OLE DB não pode ser usado para criar uma coluna FILESTREAM.    
  
Para criar colunas FILESTREAM ou detectar quais colunas existentes são colunas FILESTREAM, você pode usar o **is_filestream** coluna o [Columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) exibição do catálogo.  
  
A seguir, é mostrado um exemplo:  
  
```sql  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>Compatibilidade com níveis inferiores  
Se o cliente tiver sido compilado usando o Driver do OLE DB para SQL Server e o aplicativo se conecta ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]), em seguida, **varbinary (max)** comportamento será compatível com o comportamento introduzido pela [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Ou seja, o tamanho máximo de dados retornados será limitado a 2 GB. Para valores de resultados maiores que 2 GB, ocorrerá truncamento e um aviso de "truncamento à direita dados de cadeia de caracteres" será retornado. 
  
Quando a compatibilidade de tipo de dados estiver definida como 80, o comportamento do cliente será consistente com o comportamento de clientes de nível inferior.  
  
Para clientes que usam SQLOLEDB ou outros provedores lançados antes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], **varbinary (max)** será mapeado para imagem.  
  
## <a name="comments"></a>Comentários
- Para enviar e receber **varbinary (max)** valores maiores que 2 GB, um aplicativo usa **DBTYPE_IUNKNOWN** em associações de parâmetro e resultado. Para parâmetros de provedor deve chamar IUnknown:: QueryInterface para ISequentialStream e para resultados que retornam ISequentialStream.  

-  Para OLE DB, a verificação relacionada aos valores de ISequentialStream será aliviada. Quando *wType* é **DBTYPE_IUNKNOWN** no **DBBINDING** struct, verificação de comprimento pode ser desabilitada omitindo **DBPART_LENGTH** de *dwPart* ou definindo o tamanho dos dados (no deslocamento *obLength* no buffer de dados) para ~ 0. Nesse caso, o provedor não verificará o comprimento do valor, e solicitará e retornará todos os dados disponíveis através do fluxo. Essa alteração será aplicada a todos os tipos LOB (objeto grande) e XML, mas somente quando conectados a servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (ou posterior). Isso oferecerá maior flexibilidade para desenvolvedores, ao mesmo tempo mantendo a consistência e compatibilidade com aplicativos e servidores de versões anteriores existentes.  Esta alteração afeta todas as interfaces que transferem dados, principalmente IRowset:: GetData ICommand:: execute e IRowsetFastLoad:: Insertrow.
 

## <a name="see-also"></a>Consulte também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
