---
title: Instalar e configurar a pesquisa semântica | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], installing
- semantic search [SQL Server], configuring
ms.assetid: 2cdd0568-7799-474b-82fb-65d79df3057c
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f0c12ef425f898b8406884fef8eff27c8c80c3df
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37329326"
---
# <a name="install-and-configure-semantic-search"></a>Instalar e configurar a pesquisa semântica
  Descreve os pré-requisitos para a pesquisa semântica estatística e como instalá-los ou verificá-los.  
  
## <a name="installing-semantic-search"></a>Instalando a pesquisa semântica  
  
###  <a name="HowToCheckInstalled"></a> Como Verificar se a pesquisa semântica está instalada  
 Consulte a propriedade **IsFullTextInstalled** da função de metadados [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql).  
  
 Um valor de retorno 1 indica que a pesquisa de texto completo e a pesquisa semântica estão instaladas; um valor de retorno 0 indica que não estão instaladas.  
  
```tsql  
SELECT SERVERPROPERTY('IsFullTextInstalled');  
GO  
```  
  
###  <a name="BasicsSemanticSearch"></a> Como: Instalar a pesquisa semântica  
 Para instalar a Pesquisa Semântica, selecione **Extrações Semânticas e de Texto Completo para Pesquisa** na página **Features to Install (Recursos a serem instalados)** durante a instalação.  
  
 A pesquisa semântica estatística depende da pesquisa de texto completo. Esses dois recursos opcionais do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são instalados juntos.  
  
## <a name="installing-or-removing-the-semantic-language-statistics-database"></a>Instalando ou removendo o banco de dados de estatísticas semânticas de idioma  
 A Pesquisa Semântica tem uma dependência externa adicional denominada banco de dados de estatísticas semânticas de idioma. Esse banco de dados contém os modelos de idioma estatísticos requeridos pela pesquisa semântica. Um único banco de dados de estatísticas semânticas de idioma contém os modelos para todos os idiomas com suporte na indexação semântica.  
  
###  <a name="HowToCheckDatabase"></a> Como Verificar se o banco de dados de estatísticas semânticas de idioma está instalado  
 Consulte a exibição de catálogo [sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql).  
  
 Se o banco de dados de estatísticas semânticas de idioma for instalado e registrado para a instância, os resultados da consulta conterão uma única linha de informações sobre o banco de dados.  
  
```vb  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
###  <a name="HowToInstallModel"></a> Como: Instalar, anexar e registrar o banco de dados de estatísticas semânticas de idioma  
 O banco de dados de estatísticas semânticas de idioma não é instalado pelo programa de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para configurar o banco de dados de estatísticas semânticas de idioma como um pré-requisito para a indexação semântica, execute estas tarefas:  
  
 **1. Instale o banco de dados de estatísticas semânticas de idioma.**  
 1.  Localize o banco de dados de estatísticas semânticas de idioma nas mídias de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou baixe-o da Web.  
  
    -   Localize o pacote do Windows Installer nomeado **SemanticLanguageDatabase.msi** na mídia de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Localize a versão de 32 ou 64 bits do pacote de instalador, dependendo do sistema de destino. O nome da pasta contêiner identifica a versão de 32 ou 64 bits do arquivo; o nome do arquivo é o mesmo para ambas as versões.  
  
    -   Baixe o pacote do instalador do [estatísticas semânticas de idioma do Microsoft® SQL Server® 2014](http://go.microsoft.com/fwlink/?LinkID=296743) página de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Centro de Download.  
  
2.  Execute o pacote do Windows Installer **SemanticLanguageDatabase.msi** para extrair o banco de dados e o arquivo de log.  
  
     Se desejar, você pode alterar o diretório de destino. Por padrão, o instalador extrai os arquivos para uma pasta chamada **Microsoft Semantic Language Database** na pasta de arquivos de programa de 32 bits ou 64 bits. O arquivo MSI contém um arquivo de banco de dados compactado e um arquivo de log.  
  
3.  Mova o arquivo de banco de dados extraído e o arquivo de log para um local adequado no sistema de arquivos.  
  
     Se você deixar os arquivos no local padrão, não será possível extrair outra cópia do banco de dados para outra instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Quando o banco de dados de estatísticas semânticas de idioma é extraído, permissões restritas são atribuídas ao arquivo de banco de dados e arquivo de log no local padrão no sistema de arquivos. Como resultado, você possivelmente não terá permissão para anexar o banco de dados se deixá-lo no local padrão. Se um erro ocorrer quando você tenta anexar o banco de dados, mova os arquivos ou verifique e corrija as permissões do sistema de arquivos conforme apropriado.  
  
 **2. Anexe o banco de dados de estatísticas semânticas de idioma.**  
 Anexe o banco de dados à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou chamando [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql) com a sintaxe **FOR ATTACH**. Para obter mais informações, consulte [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md).  
  
 Por padrão, o nome do banco de dados é **semanticsdb**. Se desejar, você poderá atribuir ao banco de dados um nome diferente quando anexá-lo. Você tem que fornecer esse nome ao registrar o banco de dados na etapa subsequente.  
  
```tsql  
CREATE DATABASE semanticsdb  
            ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb.mdf' )  
            LOG ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb_log.ldf' )  
            FOR ATTACH;  
GO  
```  
  
 Esse exemplo de código pressupõe que você moveu o banco de dados de seu local padrão para um novo local.  
  
 **3. Registre o banco de dados de estatísticas semânticas de idioma.**  
 Chame o procedimento armazenado [sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql) e forneça o nome que você atribuiu ao banco de dados quando o anexou.  
  
```tsql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
GO  
```  
  
###  <a name="HowToUnregister"></a> Como: Cancelar o registro, desanexar e remover o banco de dados de estatísticas semânticas de idioma  
 **Cancelar o registro do banco de dados de estatísticas semânticas de idioma.**  
 Chame o procedimento armazenado [sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql). Você não precisa fornecer o nome do banco de dados, já que uma instância pode ter somente um banco de dados de estatísticas semânticas de idioma.  
  
```tsql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
 **Desanexe o banco de dados de estatísticas semânticas de idioma.**  
 Chame o procedimento armazenado [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql) e forneça o nome do banco de dados.  
  
```tsql  
USE master;  
GO  
  
EXEC sp_detach_db @dbname = N'semanticsdb';  
GO  
```  
  
 **Remova o banco de dados de estatísticas semânticas de idioma.**  
 Após cancelar o registro do banco de dados e desanexá-lo, você poderá simplesmente excluir o arquivo de banco de dados. Não há nenhum programa de desinstalação e nenhuma entrada em **Programas e Recursos** no Painel de Controle.  
  
###  <a name="reqinstall"></a> Requisitos e restrições para instalar e remover o banco de dados de estatísticas semânticas de idioma  
  
-   Você pode anexar e registrar somente um banco de dados de estatísticas semânticas de idioma em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
     Cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um único computador requer uma cópia física separada do banco de dados de estatísticas semânticas de idioma. Anexe uma cópia a cada instância.  
  
-   Você não pode desanexar um banco de dados de estatísticas semânticas de idioma válido e registrado, e substituí-lo por um banco de dados arbitrário que tenha o mesmo nome. Isso causará a falha de populações de índice ativas ou futuras.  
  
-   O banco de dados de estatísticas semânticas de idioma é somente leitura. Você não pode personalizar esse banco de dados. Se você alterar o conteúdo do banco de dados de alguma forma, os resultados da indexação semântica futura não serão determinísticos. Para restaurar o estado original desses dados, você poderá remover o banco de dados alterado, e baixar e anexar uma cópia nova e inalterada do banco de dados.  
  
-   É possível desanexar ou remover o banco de dados de estatísticas semânticas de idioma. Se houver alguma operação de indexação ativa que tenha bloqueios de leitura no banco de dados, a operação de desanexação ou remoção falhará ou atingirá o tempo limite. Isso é coerente com o comportamento existente. Depois que o banco de dados for removido, as operações de indexação semântica falharão.  
  
## <a name="installing-optional-support-for-newer-document-types"></a>Instalando suporte opcional para tipos de documento mais novos  
  
###  <a name="office"></a> Como: instalar os filtros mais recentes do Microsoft Office e outros tipos de documento da Microsoft  
 Esta versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala a versão mais recente [!INCLUDE[msCoName](../../../includes/msconame-md.md)] separadores de palavras e lematizadores, mas não instala os últimos filtros do word [!INCLUDE[msCoName](../../../includes/msconame-md.md)] documentos do Office e outros [!INCLUDE[msCoName](../../../includes/msconame-md.md)] tipos de documento. Esses filtros são necessários para indexação de documentos criados com versões recentes do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office e outros aplicativos [!INCLUDE[msCoName](../../../includes/msconame-md.md)] . Para baixar os filtros mais recentes, consulte [Microsoft Office 2010 Filter Packs](http://go.microsoft.com/fwlink/?LinkId=218293).  
  
  
