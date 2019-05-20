---
title: Criar banco de dados (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b051e5f2dc951eb07d4a23a5a22e15f1b2cc071
ms.sourcegitcommit: 8d288ca178e30549d793c40510c4e1988130afb0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65805122"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>Criar banco de dados (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Se você selecionar **Novo** na página **Escolher um Destino** para criar um novo banco de dados de destino do SQL Server, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará a caixa de diálogo **Criar Banco de Dados** . Nessa página, você deve fornecer um nome para o novo banco de dados. Você também pode alterar as configurações para o tamanho inicial e o aumento automático do novo banco de dados e seu arquivo de log. 

A caixa de diálogo **Criar Banco de Dados** do assistente oferece apenas as opções básicas que estão disponíveis para criar um novo banco de dados do SQL Server. Para ver e configurar todas as opções para um novo banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar o banco de dados ou para configurá-lo após a criação dele pelo assistente. 

> [!NOTE]
> Se você estiver procurando informações sobre a instrução CREATE DATABASE do [!INCLUDE[tsql](../../includes/tsql-md.md)], não sobre a caixa de diálogo **Criar Banco de Dados** do Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  

## <a name="screen-shot-of-the-create-database-page"></a>Captura de tela da página Criar Banco de Dados  
A captura de tela a seguir mostra a caixa de diálogo **Criar Banco de Dados** do assistente.  

![Página Criar banco de dados do Assistente de Importação e Exportação](../../integration-services/import-export-data/media/create-database.png "Página Criar banco de dados do Assistente de Importação e Exportação")  

## <a name="provide-a-name-for-the-new-database"></a>Fornecer um nome para o novo banco de dados  
**Nome**  
 Forneça um nome para o banco de dados de destino do SQL Server.
 
### <a name="naming-requirements"></a>Requisitos de nomenclatura
Siga as convenções de nomenclatura do SQL Server ao nomear o banco de dados.  
  
-   O nome do banco de dados deve ser exclusivo em uma instância do SQL Server.  
  
-   O nome do banco de dados pode ter um máximo 123 caracteres. (Isso permite 5 caracteres para os sufixos que o SQL Server acrescenta ao arquivo de dados e ao arquivo de log, dentro do máximo de 128 caracteres).  
  
-   O nome do banco de dados deve obedecer às regras para identificadores no SQL Server. Veja os requisitos mais importantes.  
  
    -   O primeiro caractere deve ser uma letra, um sublinhado (_), sinal de arroba (@) ou o sinal de número (#).  
  
    -   Os caracteres subsequentes podem ser letras, números, uma arroba, o sinal de cifrão ($), sinal de número ou sublinhado.  
  
    -   Você não pode usar espaços ou outros caracteres especiais.  
  
Para obter informações detalhadas sobre esses requisitos, consulte [Identificadores de banco de dados](../../relational-databases/databases/database-identifiers.md).  

## <a name="optionally-specify-data-file-and-log-file-options"></a>Especificar opções de arquivo de dados e de log como opção

> [!TIP]
> Você deve fornecer um nome para o novo banco de dados no campo **Nome** , mas normalmente pode deixar as outras configurações de tamanho e crescimento de arquivo com os valores padrão.

### <a name="data-file-options"></a>Opções de arquivo de dados  
 **Tamanho inicial**  
 Especifique o número de megabytes para o tamanho inicial do arquivo de dados.  
  
 **Não é permitido crescimento**  
 Indique se o arquivo de dados pode crescer além do tamanho inicial especificado.  
  
 **Crescimento por percentual**  
 Especifique uma porcentagem para o crescimento do arquivo de dados.  
  
 **Crescimento por tamanho**  
 Especifique um número de megabytes para o crescimento do arquivo de dados.  
  
### <a name="log-file-options"></a>Opções de arquivo de log  
 **Tamanho inicial**  
 Especifique o número de megabytes para o tamanho inicial do arquivo de log.  
  
 **Não é permitido crescimento**  
 Indique se o arquivo de log pode crescer além do tamanho inicial especificado.  
  
 **Crescimento por percentual**  
 Especifique uma porcentagem para o crescimento do arquivo de log.  
  
 **Crescimento por tamanho**  
 Especifique um número de megabytes para o crescimento do arquivo de log.  

### <a name="more-info"></a>Obter mais informações
Para obter mais informações sobre as opções de tamanho do arquivo que você vê nessa página, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md). 

## <a name="whats-next"></a>O que vem a seguir?  
 Depois que você fornecer um nome para o novo banco de dados que o assistente criará e clicar em **OK**, a caixa de diálogo **Criar Banco de Dados** retornará a página **Escolher um destino** . Para obter mais informações, consulte [Escolher um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).  

