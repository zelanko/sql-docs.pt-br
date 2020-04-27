---
title: Criar banco de dados (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a80526b0f4a1b9f122ff79bbbb5a5a8ac08a2d07
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62893102"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>Criar banco de dados (Assistente de Importação e Exportação do SQL Server)
  Use a página **criar banco de dados** para definir um novo banco de dados para um arquivo de destino.  
  
 Essa página oferece um subconjunto das opções disponíveis por criar um novo banco de dados. Para exibir todas as opções, use [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Para obter mais informações sobre este assistente, consulte [Assistente de Importação e Exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções de inicialização do assistente e sobre as permissões necessárias para executar o assistente com êxito, consulte [executar o assistente de importação e exportação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para o banco de dados de destino do SQL Server. Certifique-se de que as convenções do SQL Server estão sendo seguidas ao nomear o banco de dados.  
  
 **Nome de arquivo de dados**  
 Exibe o nome do arquivo de dados. Esse nome é originário do nome de banco de dados definido anteriormente.  
  
 **Nome do arquivo de log**  
 Exibe o nome do arquivo de log. Esse nome é originário do nome de banco de dados definido anteriormente.  
  
 **Tamanho inicial (arquivo de dados)**  
 Especifique o número de megabytes para o tamanho inicial do arquivo de dados.  
  
 **Não são permitidos crescimentos (arquivo de dados)**  
 Indique se o arquivo de dados pode crescer além do tamanho inicial especificado.  
  
 **Crescimento por porcentagem (arquivo de dados)**  
 Especifique uma porcentagem para o crescimento do arquivo de dados.  
  
 **Crescimento por tamanho (arquivo de dados)**  
 Especifique um número de megabytes para o crescimento do arquivo de dados.  
  
 **Tamanho inicial (arquivo de log)**  
 Especifique o número de megabytes para o tamanho inicial do arquivo de log.  
  
 **Não são permitidos crescimentos (arquivo de log)**  
 Indique se o arquivo de log pode crescer além do tamanho inicial especificado.  
  
 **Crescimento por porcentagem (arquivo de log)**  
 Especifique uma porcentagem para o crescimento do arquivo de log.  
  
 **Crescimento por tamanho (arquivo de log)**  
 Especifique um número de megabytes para o crescimento do arquivo de log.  
  
  
