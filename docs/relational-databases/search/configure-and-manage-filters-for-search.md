---
title: Configurar e gerenciar filtros para pesquisa | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
caps.latest.revision: 68
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a9a3c108e0a9c66daa6a6cde799694ac8491e796
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="configure-and-manage-filters-for-search"></a>Configurar e gerenciar filtros para pesquisa
  A indexação de documentos em uma coluna de tipo de dados **varbinary**, **varbinary(max)**, **image**ou **xml** exige processamento extra. Esse processamento deve ser realizado por um filtro. O filtro extrai as informações textuais do documento (removendo a formatação). Em seguida, o filtro envia o texto para o componente separador de palavras do idioma associado à coluna da tabela.  
  
 Um determinado filtro é específico a um determinado tipo de documento (.doc, .pdf, .xls, .xml e assim por diante). Estes filtros implementam a interface IFilter. Para obter mais informações sobre estes tipos de documento, veja a exibição de catálogo [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) .  
  
 Documentos binários podem ser armazenados em uma única coluna **varbinary(max)** ou **image** . Para cada documento, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escolhe o filtro correto com base na extensão de arquivo. Como a extensão de arquivo não é visível quando o arquivo é armazenado em uma coluna **varbinary(max)** ou **image** , a extensão de arquivo (.doc, .xls, .pdf e assim por diante) deve ser armazenada em outra coluna da tabela, chamada de coluna de tipo. Essa coluna de tipo pode ser do tipo de dados com base em quaisquer caracteres e contém a extensão do arquivo de documento, como .doc para um documento do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word. Na tabela **Document** de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], a coluna **Document** é do tipo **varbinary(max)**e a coluna de tipo **FileExtension**é do tipo **nvarchar(8)**.  
  
> [!NOTE]  
>  É possível que um filtro consiga processar objetos incorporados ao objeto pai, dependendo da sua implementação. No entanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não configura filtros para seguir links para outros objetos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala seus próprios filtros XML e HTML. Além disso, qualquer filtro de formatos proprietários do [!INCLUDE[msCoName](../../includes/msconame-md.md)] (.doc, .xdoc, .ppt e assim por diante) que já esteja instalado no sistema operacional também é carregado pelo  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para identificar os filtros que estão carregados atualmente em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o procedimento armazenado [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) , da seguinte maneira:  
  
```  
EXEC sp_help_fulltext_system_components 'filter';   
```  
  
 Para que seja possível usar filtros para formatos que não são do [!INCLUDE[msCoName](../../includes/msconame-md.md)] , no entanto, você deve carregá-los manualmente na instância de servidor. Para obter informações sobre como instalar filtros adicionais, veja [Exibir ou alterar filtros registrados e separadores de palavras](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
 **Para exibir a coluna de tipo em um índice de texto completo existente**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
## <a name="see-also"></a>Consulte também  
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [Compatibilidade do FILESTREAM com outros recursos do SQL Server](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
