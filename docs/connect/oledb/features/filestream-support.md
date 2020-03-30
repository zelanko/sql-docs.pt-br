---
title: Compatibilidade com o FILESTREAM | Microsoft Docs
description: Suporte ao FILESTREAM no OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 09/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server [FILESTREAM support]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: da67f050eba24ecf040124533c9d98c3f3f6bfec
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74056727"
---
# <a name="filestream-support"></a>Suporte a FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] em diante, o Driver do OLE DB para SQL Server é compatível com o recurso avançado FILESTREAM. Para ver exemplos, confira [Fluxo de arquivos e OLE DB](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md).  

FILESTREAM é uma forma de armazenar e acessar valores altos de binário, por meio do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou por acesso direto ao sistema de arquivos do Windows. Um valor binário grande é um valor superior a 2 gigabytes (GB). Para saber mais sobre a compatibilidade com o FILESTREAM avançado, confira [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md).  
  
Quando uma conexão de banco de dados for aberta, **\@\@TEXTSIZE** será definido, por padrão, como -1 ("ilimitado").  
  
Também é possível acessar e atualizar colunas FILESTREAM usando as APIs do sistema de arquivos do Windows.  
  
Para obter mais informações, confira [Acessar dados FILESTREAM com OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Consultando colunas FILESTREAM  
Conjuntos de linhas de esquema no OLE DB não relatarão se uma coluna é uma coluna FILESTREAM. ITableDefinition no OLE DB não pode ser usado para criar uma coluna FILESTREAM.    
  
Para criar colunas FILESTREAM ou detectar quais colunas existentes são colunas FILESTREAM, use a coluna **is_filestream** da exibição de catálogo [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).  
  
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
Se o cliente tiver sido compilado com o Driver do OLE DB para SQL Server e o aplicativo se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] por meio do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]), então, o comportamento **varbinary(max)** será compatível com o comportamento apresentado pelo Cliente Nativo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Ou seja, o tamanho máximo de dados retornados será limitado a 2 GB. Para valores de resultado superiores a 2 GB, ocorrerá truncamento e será retornado um aviso de "truncamento à direita de dados de cadeia de caracteres". 
  
Quando a compatibilidade de tipo de dados estiver definida como 80, o comportamento do cliente será consistente com o comportamento de clientes de nível inferior.  
  
Para clientes que usam o SQLOLEDB ou outros provedores liberados antes da versão [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], **varbinary(max)** será mapeado para imagem.  
  
## <a name="comments"></a>Comentários
- Para enviar e receber valores **varbinary(max)** maiores que 2 GB, um aplicativo usa **DBTYPE_IUNKNOWN** nas associações de parâmetro e resultado. Para os parâmetros, o provedor precisa chamar IUnknown::QueryInterface para ISequentialStream e os resultados que retornam ISequentialStream.  

-  Para o OLE DB, a verificação relacionada aos valores ISequentialStream será aliviada. Quando *wType* for **DBTYPE_IUNKNOWN** no struct **DBBINDING**, a verificação do comprimento poderá ser desabilitada pela omissão de **DBPART_LENGTH** de *dwPart* ou pela configuração do comprimento dos dados (no deslocamento *obLength* no buffer de dados) para aproximadamente 0. Nesse caso, o provedor não verificará o comprimento do valor, e solicitará e retornará todos os dados disponíveis através do fluxo. Essa alteração será aplicada a todos os tipos LOB (objeto grande) e XML, mas somente quando conectados a servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (ou posterior). Isso oferecerá maior flexibilidade para desenvolvedores, ao mesmo tempo mantendo a consistência e compatibilidade com aplicativos e servidores de versões anteriores existentes.  Essa alteração afeta todas as interfaces que transferem dados, principalmente IRowset::GetData, ICommand::Execute e IRowsetFastLoad::InsertRow.
 

## <a name="see-also"></a>Consulte Também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
