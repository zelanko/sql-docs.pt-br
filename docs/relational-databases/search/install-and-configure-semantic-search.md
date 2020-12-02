---
description: Instalar e configurar a pesquisa semântica
title: Instalar e configurar a pesquisa semântica | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], installing
- semantic search [SQL Server], configuring
ms.assetid: 2cdd0568-7799-474b-82fb-65d79df3057c
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 9d3339525dbf67ee6dd1a4e4ae3b75215dd2c05d
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91868059"
---
# <a name="install-and-configure-semantic-search"></a>Instalar e configurar a pesquisa semântica
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Descreve os pré-requisitos para a pesquisa semântica estatística e como instalá-los ou verificá-los.  
  
## <a name="install-semantic-search"></a>Instalar a pesquisa semântica  
  
###  <a name="check-whether-semantic-search-is-installed"></a><a name="HowToCheckInstalled"></a> Verificar se a pesquisa semântica está instalada  
 Consulte a propriedade **IsFullTextInstalled** da função de metadados [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md).  
  
 Um valor de retorno 1 indica que a pesquisa de texto completo e a pesquisa semântica estão instaladas; um valor de retorno 0 indica que não estão instaladas.  
  
```sql  
SELECT SERVERPROPERTY('IsFullTextInstalled');  
GO  
```  
  
###  <a name="install-semantic-search"></a><a name="BasicsSemanticSearch"></a> Instalar a pesquisa semântica  
 Para instalar a Pesquisa Semântica, selecione **Extrações Semânticas e de Texto Completo para Pesquisa** na página **Recursos a serem instalados** durante a instalação do SQL Server.  
  
 A pesquisa semântica estatística depende da pesquisa de texto completo. Esses dois recursos opcionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são instalados juntos.  
  
## <a name="install-the-semantic-language-statistics-database"></a>Instale o banco de dados de estatísticas semânticas de idioma  
 A Pesquisa Semântica tem uma dependência externa adicional denominada banco de dados de estatísticas semânticas de idioma. Esse banco de dados contém os modelos de idioma estatísticos requeridos pela pesquisa semântica. Um único banco de dados de estatísticas semânticas de idioma contém os modelos para todos os idiomas com suporte na indexação semântica.  
  
###  <a name="check-whether-the-semantic-language-statistics-database-is-installed"></a><a name="HowToCheckDatabase"></a> Verificar se o banco de dados de estatísticas semânticas de idioma está instalado  
 Consulte a exibição de catálogo [sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
 Se o banco de dados de estatísticas semânticas de idioma for instalado e registrado para a instância, os resultados da consulta conterão uma única linha de informações sobre o banco de dados.  
  
```sql  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
###  <a name="install-attach-and-register-the-semantic-language-statistics-database"></a><a name="HowToInstallModel"></a> Instalar, anexar e registrar o banco de dados de estatísticas semânticas de idioma  
 O banco de dados de estatísticas semânticas de idioma não é instalado pelo programa de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para configurar o banco de dados de estatísticas semânticas de idioma como um pré-requisito para a indexação semântica, execute estas tarefas:  
  
 **1. Instale o banco de dados de estatísticas semânticas de idioma.**  
 
 1.  Localize o banco de dados de estatísticas semânticas de idioma nas mídias de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou baixe-o da Web.  
  
        1.  Localize o pacote do Windows Installer nomeado **SemanticLanguageDatabase.msi** na mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
        2.  Baixe o pacote de instalador da página [Estatísticas semânticas de idioma do Microsoft® SQL Server® 2016](https://www.microsoft.com/download/details.aspx?id=52681) no Centro de Download da [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
2.  Execute o pacote do Windows Installer **SemanticLanguageDatabase.msi** para extrair o banco de dados e o arquivo de log.  
  
     Se desejar, você pode alterar o diretório de destino. Por padrão, o instalador extrai os arquivos para uma pasta chamada **Microsoft Semantic Language Database** na pasta Arquivos de Programas. O arquivo MSI contém um arquivo de banco de dados compactado e um arquivo de log.  
  
3.  Mova o arquivo de banco de dados extraído e o arquivo de log para um local adequado no sistema de arquivos.  
  
     Se você deixar os arquivos no local padrão, não será possível extrair outra cópia do banco de dados para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!IMPORTANT]  
    >  Quando o banco de dados de estatísticas semânticas de idioma é extraído, permissões restritas são atribuídas ao arquivo de banco de dados e arquivo de log no local padrão no sistema de arquivos. Como resultado, você possivelmente não terá permissão para anexar o banco de dados se deixá-lo no local padrão. Se um erro ocorrer quando você tenta anexar o banco de dados, mova os arquivos ou verifique e corrija as permissões do sistema de arquivos conforme apropriado.  
  
 **2. Anexe o banco de dados de estatísticas semânticas de idioma.**
   
 Anexe o banco de dados à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou chamando [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md) com a sintaxe **FOR ATTACH**. Para obter mais informações, consulte [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
 Por padrão, o nome do banco de dados é **semanticsdb**. Se desejar, você poderá atribuir ao banco de dados um nome diferente quando anexá-lo. Você tem que fornecer esse nome ao registrar o banco de dados na etapa subsequente.  
  
```sql  
CREATE DATABASE semanticsdb  
            ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb.mdf' )  
            LOG ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb_log.ldf' )  
            FOR ATTACH;  
GO  
```  
  
 Esse exemplo de código pressupõe que você moveu o banco de dados de seu local padrão para um novo local.  
  
 **3. Registre o banco de dados de estatísticas semânticas de idioma.** 
  
 Chame o procedimento armazenado [sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md) e forneça o nome que você atribuiu ao banco de dados quando o anexou.  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
GO  
```  

##  <a name="requirements-and-restrictions-for-the-semantic-language-statistics-database"></a><a name="reqinstall"></a> Requisitos e restrições para o banco de dados de estatísticas semânticas de idioma  
  
-   Você pode anexar e registrar somente um banco de dados de estatísticas semânticas de idioma em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um único computador requer uma cópia física separada do banco de dados de estatísticas semânticas de idioma. Anexe uma cópia a cada instância.  
  
-   Você não pode desanexar um banco de dados de estatísticas semânticas de idioma válido e registrado, e substituí-lo por um banco de dados arbitrário que tenha o mesmo nome. Isso causará a falha de populações de índice ativas ou futuras.  
  
-   O banco de dados de estatísticas semânticas de idioma é somente leitura. Você não pode personalizar esse banco de dados. Se você alterar o conteúdo do banco de dados de alguma forma, os resultados da indexação semântica futura não serão determinísticos. Para restaurar o estado original desses dados, você poderá remover o banco de dados alterado, e baixar e anexar uma cópia nova e inalterada do banco de dados.  
  
-   É possível desanexar ou remover o banco de dados de estatísticas semânticas de idioma. Se houver alguma operação de indexação ativa que tenha bloqueios de leitura no banco de dados, a operação de desanexação ou remoção falhará ou atingirá o tempo limite. Isso é coerente com o comportamento existente. Depois que o banco de dados for removido, as operações de indexação semântica falharão.  
 
##  <a name="remove-the-semantic-language-statistics-database"></a><a name="HowToUnregister"></a> Remova o banco de dados de estatísticas semânticas de idioma  

###  <a name="unregister-detach-and-remove-the-semantic-language-statistics-database"></a>Cancelar o registro do banco de dados de estatísticas semânticas de idioma, desanexá-lo e removê-lo 

 **1. Cancelar o registro do banco de dados de estatísticas semânticas de idioma.**
   
 Chame o procedimento armazenado [sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md). Você não precisa fornecer o nome do banco de dados, já que uma instância pode ter somente um banco de dados de estatísticas semânticas de idioma.  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
 **2. Desanexar o banco de dados de estatísticas semânticas de idioma.**  
 
 Chame o procedimento armazenado [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) e forneça o nome do banco de dados.  
  
```sql  
USE master;  
GO  
  
EXEC sp_detach_db @dbname = N'semanticsdb';  
GO  
```  
  
 **3. Remova o banco de dados de estatísticas semânticas de idioma.**  
 
 Após cancelar o registro do banco de dados e desanexá-lo, você poderá simplesmente excluir o arquivo de banco de dados. Não há nenhum programa de desinstalação e nenhuma entrada em **Programas e Recursos** no Painel de Controle.  
  
## <a name="install-optional-support-for-newer-document-types"></a>Instalar suporte opcional para tipos de documento mais novos  
  
###  <a name="install-the-latest-filters-for-microsoft-office-and-other-microsoft-document-types"></a><a name="office"></a> Instalar os filtros mais recentes para Microsoft Office e outros tipos de documento Microsoft  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala os separadores de palavras e lematizadores mais recentes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] , mas não instala os últimos filtros de documentos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office e outros tipos de documento [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Esses filtros são necessários para indexação de documentos criados com versões recentes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office e outros aplicativos [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para baixar os filtros mais recentes, consulte [Microsoft Office 2010 Filter Packs](https://www.microsoft.com/download/details.aspx?id=17062). (Não parece haver uma versão do pacote de filtro para Office 2013 ou Office 2016.)
  
