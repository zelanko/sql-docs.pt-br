---
title: Configurar e gerenciar filtros para pesquisa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
caps.latest.revision: 68
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7b19f9141df65be952551dbb899b6cb30544e9a3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278922"
---
# <a name="configure-and-manage-filters-for-search"></a>Configurar e gerenciar filtros para pesquisa
  Indexação de documentos em uma `varbinary`, `varbinary(max)`, `image`, ou `xml` coluna de tipo de dados exige processamento extra. Esse processamento deve ser realizado por um filtro. O filtro extrai as informações textuais do documento (removendo a formatação). Em seguida, o filtro envia o texto para o componente separador de palavras do idioma associado à coluna da tabela.  
  
 Um determinado filtro é específico a um determinado tipo de documento (.doc, .pdf, .xls, .xml e assim por diante). Estes filtros implementam a interface IFilter. Para obter mais informações sobre estes tipos de documento, veja a exibição de catálogo [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) .  
  
 É possível armazenar documentos binários em uma única coluna `varbinary(max)` ou `image`. Para cada documento, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] escolhe o filtro correto com base na extensão de arquivo. Como a extensão de arquivo não é visível quando o arquivo é armazenado em uma `varbinary(max)` ou `image` coluna, a extensão de arquivo (. doc,. xls,. PDF e assim por diante) deve ser armazenada em uma coluna separada na tabela, chamada de uma coluna de tipo. Essa coluna de tipo pode ser do tipo de dados com base em quaisquer caracteres e contém a extensão do arquivo de documento, como .doc para um documento do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Word. No **documento** na tabela [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], o **documento** coluna é do tipo `varbinary(max)`e a coluna de tipo **FileExtension**, é do tipo `nvarchar(8)`.  
  
> [!NOTE]  
>  É possível que um filtro consiga processar objetos incorporados ao objeto pai, dependendo da sua implementação. No entanto o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não configura filtros para seguir links para outros objetos.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala seus próprios filtros XML e HTML. Além disso, qualquer filtro de formatos proprietários do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] (.doc, .xdoc, .ppt e assim por diante) que já esteja instalado no sistema operacional também é carregado pelo  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para identificar os filtros que estão carregados atualmente em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], use o procedimento armazenado [sp_help_fulltext_system_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql) , da seguinte maneira:  
  
```  
EXEC sp_help_fulltext_system_components 'filter';   
```  
  
 Para que seja possível usar filtros para formatos que não são do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] , no entanto, você deve carregá-los manualmente na instância de servidor. Para obter informações sobre como instalar filtros adicionais, veja [Exibir ou alterar filtros registrados e separadores de palavras](view-or-change-registered-filters-and-word-breakers.md).  
  
 **Para exibir a coluna de tipo em um índice de texto completo existente**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
## <a name="see-also"></a>Consulte também  
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)   
 [Compatibilidade do FILESTREAM com outros recursos do SQL Server](../blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
