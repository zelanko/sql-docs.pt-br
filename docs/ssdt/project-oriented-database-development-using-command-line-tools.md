---
title: Desenvolvimento de banco de dados orientado a projetos usando ferramentas de linha de comando| Microsoft Docs
ms.custom:
- SSDT
ms.date: 04/26/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9a26def9-8fbd-43e4-9e57-414840b73ed8
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 157aa8f1aca7fac32f7c7606c4681b2e27db1d37
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39087928"
---
# <a name="project-oriented-database-development-using-command-line-tools"></a>Desenvolvimento de banco de dados orientado a projetos usando ferramentas de linha de comando
O SQL Server Data Tools prova ferramentas de linha de comando que permitem vários cenários de desenvolvimento orientados a projeto.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|||  
|-|-|  
|[SqlPackage.exe](../tools/sqlpackage.md)|Este tópico descreve o utilitário SQLPackage.exe, usado para as seguintes tarefas:<br /><br />-   Extrair um arquivo .dacpac de um banco de dados dinâmico do SQL Server.<br />-   Publicar um arquivo .dacpac em um banco de dados dinâmico do SQL Server para atualizar incrementalmente o esquema do banco de dados dinâmico para que corresponda ao .dacpac.<br />-   Comparar um arquivo .dacpac com um banco de dados dinâmico do SQL Server e gerar um script Transact\-SQL de atualização incremental sem atualizar o banco de dados dinâmico.<br />-   Comparar dois arquivos .dacpac para gerar um script Transact\-SQL de atualização incremental.<br />-   Gerar um relatório XML que resume as alterações da atualização incremental que ocorreriam se o banco de dados fosse atualizado incrementalmente.|  
|[Usar o MSDeploy com o provedor do dbSqlPackage](../ssdt/using-msdeploy-with-dbsqlpackage-provider.md)|Este tópico descreve o provedor da [Ferramenta de Implantação da Web](http://go.microsoft.com/fwlink/?LinkId=231798), denominado dbSqlPackage, incluído no SSDT, que funciona com a Ferramenta de Desenvolvimento da Web da Microsoft (MSDeploy.exe) do IIS (Serviços de Informações da Internet), usada para as seguintes tarefas:<br /><br />-   Extrair um arquivo .dacpac de um banco de dados remoto/local do SQL Server ou do SQL Azure.<br />-   Publicar um .dacpac em um banco de dados remoto/local do SQL Server ou do SQL Azure para atualizá-lo incrementalmente.<br />-   Publicar a partir de um banco de dados local do SQL Server em um banco de dados remoto do SQL Server ou do SQL Azure para atualizar o banco de dados remoto incrementalmente.<br />-   Comparar um .dacpac com um banco de dados remoto/local do SQL Server ou do SQL Azure para gerar um script Transact\-SQL de atualização incremental sem atualizar o banco de dados dinâmico.<br />-   Gerar um relatório XML que resume as alterações da atualização incremental que ocorreriam se o banco de dados fosse atualizado incrementalmente.|  
  
## <a name="related-sections"></a>Seções relacionadas  
[Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md)  
  
