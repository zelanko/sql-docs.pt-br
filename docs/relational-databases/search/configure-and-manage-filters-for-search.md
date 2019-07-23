---
title: Configurar e gerenciar filtros para pesquisa | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5dd9719ea0f10b3bbac6aae5171a2c941cdf7e1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093300"
---
# <a name="configure-and-manage-filters-for-search"></a>Configurar e gerenciar filtros para pesquisa
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A indexação de documentos em uma coluna de tipo de dados **varbinary**, **varbinary(max)** , **image** ou **xml** exige processamento extra. Esse processamento deve ser realizado por um filtro. O filtro extrai as informações textuais do documento (removendo a formatação). Em seguida, o filtro envia o texto para o componente separador de palavras do idioma associado à coluna da tabela.  
 
## <a name="filters-and-document-types"></a>Filtros e tipos de documento
Um determinado filtro é específico a um determinado tipo de documento (.doc, .pdf, .xls, .xml e assim por diante). Estes filtros implementam a interface IFilter. Para obter mais informações sobre estes tipos de documento, veja a exibição de catálogo [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) .  
  
Documentos binários podem ser armazenados em uma única coluna **varbinary(max)** ou **image** . Para cada documento, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escolhe o filtro correto com base na extensão de arquivo. Como a extensão de arquivo não é visível quando o arquivo é armazenado em uma coluna **varbinary(max)** ou **image** , a extensão de arquivo (.doc, .xls, .pdf e assim por diante) deve ser armazenada em outra coluna da tabela, chamada de coluna de tipo. Essa coluna de tipo pode ser do tipo de dados com base em quaisquer caracteres e contém a extensão do arquivo de documento, como .doc para um documento do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word. Na tabela **Document** de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], a coluna **Document** é do tipo **varbinary(max)** e a coluna de tipo **FileExtension**é do tipo **nvarchar(8)** .  

**Para exibir a coluna de tipo em um índice de texto completo existente**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
> [!NOTE]  
>  É possível que um filtro consiga processar objetos incorporados ao objeto pai, dependendo da sua implementação. No entanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não configura filtros para seguir links para outros objetos.  

## <a name="installed-filters"></a>Filtros instalados 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala seus próprios filtros XML e HTML. Além disso, qualquer filtro de formatos proprietários do [!INCLUDE[msCoName](../../includes/msconame-md.md)] (.doc, .xdoc, .ppt e assim por diante) que já esteja instalado no sistema operacional também é carregado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para identificar os filtros que estão carregados atualmente em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o procedimento armazenado [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) , da seguinte maneira:  

```sql
EXEC sp_help_fulltext_system_components 'filter';   
```  

> [!NOTE]
> Mesmo com a versão mais recente do pacote de filtro do Office que dá suporte a .xlsx, o SQL Server não oferece suporte a planilhas Open XML estritas.  Nenhum erro será retornado, SQL Server simplesmente falhará em indexar o conteúdo de qualquer Planilha Open XML Estrita.

## <a name="non-microsoft-filters"></a>Atualizações que não são da Microsoft
Antes que seja possível usar filtros para formatos que não são [!INCLUDE[msCoName](../../includes/msconame-md.md)], é necessário, contudo, carregá-los manualmente na instância de servidor. Para obter informações sobre como instalar filtros adicionais, veja [Exibir ou alterar filtros registrados e separadores de palavras](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
  
## <a name="see-also"></a>Consulte Também  
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [Compatibilidade do FILESTREAM com outros recursos do SQL Server](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
