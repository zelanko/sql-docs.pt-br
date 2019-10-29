---
title: Extensão dacpac do SQL Server
titleSuffix: Azure Data Studio
description: Instale e use a extensão dacpac do SQL Server (versão prévia) para o Azure Data Studio
ms.custom: seodec18
ms.date: 10/21/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 769e6157e7d84702716dfce79d0217efeee83076
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783315"
---
# <a name="sql-server-dacpac-extension-preview"></a>Extensão de dacpac do SQL Server (versão prévia)

O **Assistente de Aplicativo da Camada de Dados** proporciona uma experiência fácil de usar para implantar e extrair arquivos dacpac e importar e exportar arquivos bacpac.

Atualmente, essa experiência está na versão prévia inicial. Informe sobre problemas e solicite recursos [aqui](https://github.com/microsoft/azuredatastudio/issues).


## <a name="features"></a>Recursos

* Implantar um dacpac em uma Instância do SQL Server
* Extrair uma Instância do SQL Server para um dacpac
* Criar um banco de dados a partir de um bacpac
* Exportar esquema e dados para um bacpac

![gif de demonstração da extensão dacpac](media/extensions/sql-server-dacpac-extension/dacpac-extension-demo.gif)


## <a name="why-would-i-use-the-data-tier-application-wizard"></a>Por que usar o assistente do Aplicativo da Camada de Dados?

O assistente facilita o gerenciamento de arquivos dacpac e bacpac, o que simplifica o desenvolvimento e a implantação de elementos da camada de dados que dão suporte ao seu aplicativo. Para saber mais sobre como usar os aplicativos da camada de dados, [confira nossa documentação.](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)


## <a name="install-the-extension"></a>Instalar a extensão

1. Selecione o ícone de Extensões para exibir as extensões disponíveis.

    ![ícone do gerenciador de extensões](media/extensions/extension-manager-icon.png)

2. Pesquise a extensão **dacpac do SQL Server** e selecione-a para exibir seus detalhes. Clique em **Instalar** para adicionar a extensão.

3. Após a instalação, clique em **Recarregar** para habilitar a extensão no Azure Data Studio (necessário somente ao instalar uma extensão pela primeira vez).


## <a name="launch-the-data-tier-application-wizard"></a>Iniciar o Assistente de Aplicativo da Camada de Dados

Para iniciar o assistente, clique com o botão direito do mouse na pasta Bancos de dados ou em um banco de dados específico no Pesquisador de Objetos. Em seguida, clique no **Assistente de Aplicativo da Camada de Dados**.

![menu de inicialização da extensão dacpac](media/extensions/sql-server-dacpac-extension/dacpac-extension-launch.png)


## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre dacpacs, [confira nossa documentação](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017).