---
title: Validar pacotes do SSIS implantados no Azure | Microsoft Docs
description: Saiba como o Assistente de Implantação de Pacote do SSIS verifica pacotes em busca de problemas conhecidos que podem impedir que os pacotes sejam executados conforme esperado no Azure.
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: fd6c55f439b9d95473c5e36ea88cc7c5e1fb555e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72915989"
---
# <a name="validate-sql-server-integration-services-ssis-packages-deployed-to-azure"></a>Validar pacotes SSIS (SQL Server Integration Services) implantados no Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Quando você implanta um projeto do SSIS (SQL Server Integration Services) no SSISDB (Catálogo do SSIS) em um servidor do Azure, o assistente de implantação do pacote adiciona uma etapa de validação adicional após a página **Análise**. Essa etapa de validação verifica se há problemas conhecidos nos pacotes do projeto que possam impedir que os pacotes sejam executados conforme o esperado no Azure SSIS Integration Runtime. Em seguida, o assistente exibe avisos aplicáveis na página **Validar**.

> [!IMPORTANT]
> A validação descrita neste artigo ocorre quando você implanta um projeto com o SSDT (SQL Server Data Tools) versão 17.4 ou posterior. Para obter a versão mais recente do SSDT, consulte [Baixar o SSDT (SQL Server Data Tools)](../../ssdt/download-sql-server-data-tools-ssdt.md).

Para obter mais informações sobre o Assistente de Implantação de Pacotes, consulte [Deploy Integration Services (SSIS) Projects and Packages](../packages/deploy-integration-services-ssis-projects-and-packages.md) (Implantar projetos e pacotes do SSIS (Integration Services)).

## <a name="validate-connection-managers"></a>Validar gerenciadores de conexões

O assistente verifica se os seguintes problemas, que podem fazer a conexão falhar, ocorrem em determinados gerenciadores de conexão:
- **Autenticação do Windows**. Se uma cadeia de conexão usar a autenticação do Windows, a validação emitirá um aviso. A autenticação do Windows exige etapas de configuração adicionais. Para obter mais informações, confira [Conectar-se a dados e a compartilhamentos de arquivos com a Autenticação do Windows](ssis-azure-connect-with-windows-auth.md).
- **Caminho do arquivo**. Se uma cadeia de conexão contiver um caminho de arquivo local embutido em código como `C:\\...`, a validação emitirá um aviso. Os pacotes que contêm um caminho absoluto podem falhar.
- **Caminho UNC**. Se uma cadeia de conexão contiver um caminho UNC, a validação gerará um aviso. Os pacotes que contêm um caminho UNC poderão falhar, geralmente porque um caminho UNC exige a autenticação do Windows para obter acesso.
- **Nome do host**. Se uma propriedade de servidor contiver o nome do host em vez do endereço IP, a validação emitirá um aviso. Os pacotes que contêm o nome do host podem falhar, geralmente porque a rede virtual do Azure exige a configuração correta do DNS para ser compatível com a resolução de nome DNS.
- **Provedor ou driver**. Se um provedor ou driver não for compatível, a validação emitirá um aviso. Somente um pequeno número de drivers e provedores internos são compatíveis no momento.

O assistente faz as seguintes verificações de validação nos gerenciadores de conexão na lista.

| Gerenciador de Conexões | Autenticação do Windows | Caminho do arquivo | Caminho UNC | Nome do host | Provedor ou driver |
|--------------------|----------|-----------|-----|-----------|-------------------|
| Ado                | âœ“        |           |     | âœ“         | âœ“                 |
| AdoNet             | âœ“        |           |     | âœ“         | âœ“                 |
| Cache              |          | âœ“         | âœ“   |           |                   |
| Excel              |          | âœ“         | âœ“   |           |                   |
| Arquivo               |          | âœ“         | âœ“   |           |                   |
| FlatFile           |          | âœ“         | âœ“   |           |                   |
| Ftp                |          |           |     | âœ“         |                   |
| MsOLAP100          |          |           |     | âœ“         | âœ“                 |
| MultiFile          |          | âœ“         | âœ“   |           |                   |
| MultiFlatFile      |          | âœ“         | âœ“   |           |                   |
| OData              | âœ“        |           |     | âœ“         |                   |
| Odbc               | âœ“        |           |     | âœ“         | âœ“                 |
| OleDb              | âœ“        |           |     | âœ“         | âœ“                 |
| SmoServer          | âœ“        |           |     | âœ“         |                   |
| Smtp               | âœ“        |           |     | âœ“         |                   |
| SqlMobile          |          | âœ“         | âœ“   |           |                   |
| Wmi                | âœ“        |           |     |           |                   |
|||||||

## <a name="validate-sources-and-destinations"></a>Validar origens e destinos
As seguintes origens e destinos de terceiros não são compatíveis:

-   Origem e destino da Oracle por Attunity
-   Origem e destino do Teradata por Attunity
-   Origem e destino do SAP BI

## <a name="validate-tasks-and-components"></a>Validar tarefas e componentes

### <a name="execute-process-task"></a>Tarefa Executar Processo

A validação emitirá um aviso se um comando apontar para um arquivo local com um caminho absoluto ou para um arquivo com um caminho UNC. Esses caminhos podem fazer com que a execução no Azure falhe.

### <a name="script-task-and-script-component"></a>Tarefa Script e Componente Script

A validação emitirá um aviso se um pacote contiver uma tarefa de script ou um componente de script, que possa referenciar ou chamar assemblies incompatíveis. Essas referências ou chamadas podem causar a falha da execução.

### <a name="other-components"></a>Outros componentes

O formato de Orc não é compatível com o destino do HDFS e com o destino do Azure Data Lake Store.

## <a name="next-steps"></a>Próximas etapas
Para saber como agendar a execução de pacotes no Azure, consulte [Agendar pacotes SSIS no Azure](ssis-azure-schedule-packages.md).
