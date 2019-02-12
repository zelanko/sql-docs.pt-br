---
title: Fonte do Power Query | Microsoft Docs
description: Saiba como configurar a Fonte do Power Query no fluxo de dados do SQL Server Integration Services
ms.date: 02/02/2019
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql14.ssis.designer.powerqueryconnmgr.f1
- sql14.ssis.designer.powerquerysource.queries.f1
- sql14.ssis.designer.powerquerysource.connmgrs.f1
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 00b24bdc5da2c717f43ca30e9159aa845faf171b
ms.sourcegitcommit: 7c052fc969d0f2c99ad574f99076dc1200d118c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570699"
---
# <a name="power-query-source-preview"></a>Fonte do Power Query (versão prévia)

Este artigo descreve como configurar as propriedades da Fonte do Power Query no fluxo de dados do SQL Server Integration Services (SSIS). O Power Query é uma tecnologia que permite conectar-se a várias fontes de dados e transformar dados usando o Excel/Power BI Desktop. Para saber mais, confira o artigo [Power Query - visão geral e aprendizagem](https://support.office.com/article/power-query-overview-and-learning-ed614c81-4b00-4291-bd3a-55d80767f81d). O script gerado pelo Power Query pode ser copiado e colado na Origem do Power Query no fluxo de dados do SSIS para configurá-lo.
  
> [!NOTE]
> Para a versão prévia atual, a fim de facilitar a rápida coleta de comentários e aprimoramentos frequentes de recursos, a Fonte do Power Query só pode ser usada no SSDT (SQL Server Data Tools) e no IR (Azure-SSIS Integration Runtime) no Azure Data Factory (ADF). Você pode fazer o download do SSDT mais recente que dê suporte à Origem do Power Query [aqui](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017). Para provisionar o Azure-SSIS IR, confira o artigo [Provisionar o SSIS no ADF](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure).

## <a name="configure-the-power-query-source"></a>Configurar a Fonte do Power Query

Para abrir o **Editor de Fonte do Power Query** no SSDT, arraste e solte a **Fonte do Power Query** da Caixa de Ferramentas do SSIS para o designer de fluxo de dados e clique duas vezes.  

![Fonte do PQ](media/power-query-source/pq-source.png)

Três guias são mostradas no lado esquerdo. Na guia **Consultas**, você pode selecionar o seu modo de consulta no menu suspenso.
-   O modo **Consulta Única** permite que você copie e cole um único script do Power Query do Excel/Power BI Desktop.
-   O modo **Consulta Única da Variável** permite que você especifique uma variável de cadeia de caracteres que contém sua consulta a ser executada.

![Guia Consultas da Fonte do PQ Individual](media/power-query-source/pq-source-queries-tab-single.png)

Na guia **Gerenciadores de Conexões**, você pode adicionar ou remover gerenciadores de conexões do Power Query que contêm credenciais de acesso à fonte de dados. Selecionar o botão **Detectar Fonte de Dados** identifica as fontes de dados referenciadas na sua consulta e as lista para você atribuir os gerenciadores de conexões do Power Query existentes ou criar novos.

![Detectar Guia Gerenciadores de Conexões da Fonte do PQ](media/power-query-source/pq-source-connection-managers-tab-detect.png)

![Adicionar Guia Gerenciadores de Conexões da Fonte do PQ](media/power-query-source/pq-source-connection-managers-tab-add.png)

Por fim, na guia **Colunas**, você pode editar as informações da coluna de saída.

![Guia Colunas da Fonte do PQ](media/power-query-source/pq-source-columns-tab.png)

## <a name="configure-the-power-query-connection-manager"></a>Configurar o Gerenciador de Conexões do Power Query

Ao projetar seu fluxo de dados com a Fonte do Power Query no SSDT, você pode criar um novo Gerenciador de Conexões do Power Query das seguintes maneiras:
- Crie-o indiretamente na guia **Gerenciadores de Conexões** da Fonte do Power Query depois de selecionar **Adicionar**/ **Detectar Fonte de Dados** e selecionar **<New connection...>** no menu suspenso, conforme descrito acima.
- Crie-o diretamente clicando com o botão direito do mouse no painel **Gerenciadores de Conexões** do seu pacote e selecionando **Nova Conexão...**  no menu suspenso.

![Adicionar Painel de Gerenciadores de Conexões da Fonte do PQ](media/power-query-source/pq-source-connection-managers-panel-add.png)

Na caixa de diálogo **Adicionar Gerenciador de Conexões SSIS**, clique duas vezes em **PowerQuery** na lista de tipos de gerenciadores de conexões.

![Caixa de diálogo Adicionar Painel de Gerenciadores de Conexões da Fonte do PQ](media/power-query-source/pq-source-connection-managers-panel-add-dialog.png)

No **Editor do Gerenciador de Conexões do Power Query**, você precisa especificar o **Tipo de Fonte de Dados**, **Caminho da Fonte de Dados** e **Tipo de Autenticação**, bem como atribuir as credenciais de acesso apropriadas. Para **Tipo de Fonte de Dados**, você pode selecionar atualmente um dos 22 tipos no menu suspenso.

![Tipo de Editor do Gerenciador de Conexões da Fonte do PQ](media/power-query-source/pq-source-connection-manager-editor-kind.png)

Algumas dessas fontes (**Oracle**, **DB2**, **MySQL**, **PostgreSQL**, **Teradata**, **Sybase**) requerem instalações adicionais de drivers do ADO.NET que podem ser obtidas no artigo [Pré-requisitos do Power Query](https://support.office.com/article/data-source-prerequisites-power-query-6062cf52-c764-45d0-a1c6-fbf8fc05b05a). Você pode usar a interface de configuração personalizada para instalá-los em seu Azure-SSIS IR, confira o artigo [Personalizar o Azure-SSIS IR](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup).

> [!NOTE]
> Para a fonte de dados **Oracle**, o driver da Oracle ADO.NET não pode atualmente ser instalado no Azure-SSIS IR, portanto instale o driver ODBC da Oracle e use a fonte de dados **ODBC** para conectar-se à Oracle. Agora, confira o exemplo **ORACLE STANDARD ODBC** no artigo [Personalizar o Azure-SSIS IR](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup).

Para **Caminho da Fonte de Dados** , você pode inserir propriedades específicas da fonte de dados formando uma cadeia de conexão sem as informações de autenticação. Por exemplo, o caminho para a fonte de dados **SQL** é formado como `<Server>;<Database>`. Você pode selecionar o botão **Editar** para atribuir valores a propriedades específicas da fonte de dados que formam o caminho.

![Caminho do Editor do Gerenciador de Conexões da Fonte do PQ](media/power-query-source/pq-source-connection-manager-editor-path.png)

Finalmente, para **Tipo de Autenticação**, você pode selecionar **Anônimo**/**Autenticação do Windows**/**Nome de usuário/senha**/**chave** no menu suspenso, insira as credenciais de acesso apropriadas e selecione o botão **Conexão de Teste** para garantir que a Fonte do Power foi configurada corretamente.

![Autenticação do Editor do Gerenciador de Conexões da Fonte do PQ](media/power-query-source/pq-source-connection-manager-editor-authentication.png)

## <a name="next-steps"></a>Próximas etapas
Saiba como executar pacotes SSIS no Azure-SSIS IR como atividades de primeira classe em pipelines do ADF. Confira o artigo [Executar o tempo de execução da atividade do pacote SSIS](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity).
