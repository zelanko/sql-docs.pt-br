---
title: O que há de novo no SSMA for Access (AccessToSQL) | Microsoft Docs
description: Saiba mais sobre as alterações feitas no Assistente de Migração do SQL Server (SSMA) for Access (AccessToSQL) para cada versão.
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 7/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
ms.author: alexiva
ms.openlocfilehash: e2c45c4aea17448af7ed496c1c56b8629c30e429
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85978818"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>O que há de novo no SSMA for Access (AccessToSQL)

Este artigo lista Assistente de Migração do SQL Server (SSMA) para acessar alterações em cada versão.

## <a name="ssma-v811"></a>8.11 do SSMA v

A versão v 8.11 do SSMA para Access contém as seguintes alterações:

* Usar a biblioteca MSAL.NET para autenticação de Azure Active Directory interativa

## <a name="ssma-v810"></a>SSMA v 8.10

A versão v 8.10 do SSMA para Access contém pequenas melhorias de desempenho e correções de bugs.

## <a name="ssma-v89"></a>8.9 do SSMA v

A versão v 8.9 do SSMA para Access contém as seguintes alterações:

* Conversão aprimorada para consultas de auto-referência
* Correção do problema com caracteres especiais no nome do projeto

## <a name="ssma-v88"></a>8.8 do SSMA v

A versão v 8.8 do SSMA para o Access inclui:

* Melhorias na estabilidade da sincronização de objetos do SQL Server
* Melhorias de desempenho de GUI durante a avaliação e conversão
* Novo analisador de sintaxe de acesso para melhorar ainda mais o desempenho da conversão

## <a name="ssma-v87"></a>SSMA v 8.7

A versão v 8.7 do SSMA para Access tem uma conversão aprimorada para `IIF` funções em consultas, bem como correções secundárias e melhorias de desempenho na interface gráfica do usuário.

> [!IMPORTANT]
> Com o SSMA v 8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se precisar instalar essa versão, você poderá baixar o arquivo de tempo de execução [aqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v 8.6

Além de um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho, a versão do v 8.6 do SSMA para acesso foi aprimorada com a adição de uma configuração que permite aos usuários omitir as propriedades estendidas do SSMA no código convertido.

Para aproveitar essa configuração, no SSMA para acesso, navegue até **ferramentas**  >  **configurações do projeto**  >  **General**  >  **conversão**geral e **, em**seguida, atualize o valor da configuração **omitir propriedades estendidas** para **Sim**.

![Omitir a configuração de propriedades estendidas](../access/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> Com o SSMA v 8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se precisar instalar essa versão, você poderá baixar o arquivo de tempo de execução [aqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v 8.5

A versão v 8.5 do SSMA para acesso é aprimorada com suporte para autenticação Azure Active Directory e suporte básico para recursos JSON no SQL Server, junto com um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho.

Além disso, o SSMA para Access agora dá suporte à conversão de várias funções padrão ( `ISNULL` , `IIF` , etc.).

> [!IMPORTANT]
> Com o SSMA v 8.5, o .NET 4.7.2 é um pré-requisito de instalação. Se precisar instalar essa versão, você poderá baixar o arquivo de tempo de execução [aqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v 8.4

A versão v 8.4 do SSMA para acesso é aprimorada com correções direcionadas que foram projetadas para resolver problemas de acessibilidade e corrigir um bug relacionado a colunas de índice máximo (para permitir 32 em vez de 16) para SQL Server 2016 e versões posteriores.

> [!IMPORTANT]
> Com o SSMA versões 7,4, embora 8,4, o .NET 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v83"></a>SSMA v 8.3

A versão v 8.3 do SSMA para acesso é aprimorada com correções direcionadas que foram projetadas para melhorar a qualidade e a conversão de métricas. Além disso, esta versão do SSMA para Access fornece correções que:

* Solucionar problemas de acessibilidade.
* Adicione suporte básico para o `hierarchyid` tipo em SQL Server.

## <a name="ssma-v82"></a>SSMA v 8.2

A versão v 8.2 do SSMA para acesso é aprimorada com correções direcionadas que foram projetadas para melhorar a qualidade e a conversão de métricas.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v 8.1 para v 8.2. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v81"></a>SSMA v 8.1

A versão v 8.1 do SSMA para acesso é aprimorada com correções direcionadas que foram projetadas para melhorar a qualidade e a conversão de métricas.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v 8.0 para o v 8.1. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v80"></a>SSMA v 8.0

A versão v 8.0 do SSMA para acesso é aprimorada com correções direcionadas projetadas para melhorar a qualidade e a conversão de métricas. Esta versão também oferece os seguintes novos recursos:

* Suporte para **instância gerenciada do banco de dados SQL do Azure** como um destino. Agora você pode criar novos projetos destinados a Instância Gerenciada do Banco de Dados SQL do Azure:

  ![Projeto MI do BD SQL](../media/ssma-newproject-sqldbmi.png)

* **Supervisor de correção**após a conversão. Saiba mais sobre isso [aqui](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Accelerate-your-Oracle-migrations-with-new-machine-learning/ba-p/368733).

* Seleção preliminar de banco de dados/esquema.

    Ao se conectar à fonte, o usuário agora pode selecionar bancos de dados/esquemas de interesse. Selecionar somente os esquemas que você planeja migrar economizará tempo durante a conexão inicial e melhorará o desempenho geral do SSMA.

   ![Objetos de filtro do SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>7.10 do SSMA v

A versão v 7.10 do SSMA para acesso é aprimorada com correções direcionadas projetadas para fornecer proteção adicional e proteções de privacidade para atender às alterações nos requisitos globais.

## <a name="ssma-v79"></a>7.9 do SSMA v

A versão v 7.9 do SSMA para Access contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Suporte na linha de comando do SSMA para alterar o mapeamento de tipo de dados e as preferências do projeto.
* A caixa de diálogo conexão do banco de dados SQL do Azure no SSMA também foi alterada para especificar o nome do servidor totalmente qualificado. Nas versões anteriores do SSMA, o prefixo do banco de dados SQL do Azure tinha que ser explicitamente mencionado dentro das configurações de projetos.

## <a name="ssma-v78"></a>SSMA v 7.8

A versão v 7.8 do SSMA para Access contém as seguintes alterações:

* Alterar o mapeamento de tipo realçado nas configurações do projeto.
* A capacidade dos usuários de desabilitar a telemetria.

## <a name="ssma-v77"></a>7.7 do SSMA v

A versão v 7.7 do SSMA para Access contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Com base na demanda popular, a versão de 32 bits do SSMA para acesso é de volta. Em comparação com a implementação anterior (antes da v 7.4), há dois pacotes do instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base nos componentes de conectividade que tem. É sempre preferível usar a versão de 64 bits, se possível.

## <a name="ssma-v76"></a>SSMA v 7.6

A versão v 7.6 do SSMA para acesso é aprimorada com correções direcionadas que melhoram as métricas de qualidade e conversão e com suporte para SQL Server 2017 (visualização pública). O suporte para SQL Server 2017 no Windows e no Linux está em visualização pública e não deve ser usado para migrações de produção.

## <a name="ssma-v75"></a>SSMA v 7.5

A versão v 7.5 do SSMA para acesso é aprimorada com várias melhorias para garantir maior acessibilidade para pessoas com deficiências.

## <a name="ssma-v74"></a>SSMA v 7.4

A versão v 7.4 do SSMA para Access contém as seguintes alterações:

* A opção de **tempo limite de consulta** agora está disponível durante a descoberta de objeto de esquema na origem e no destino.

  ![opção de tempo limite de consulta](../media/query-timeout_red.png)

* A métrica de qualidade e conversão foi aprimorada com correções direcionadas, com base nos comentários dos clientes.

  > [!IMPORTANT]
  > O .NET 4.5.2 é um pré-requisito para a instalação do SSMA v 7.4. Além disso, a partir da v 7.4, a versão de 32 bits do SSMA foi descontinuada.

## <a name="ssma-v73"></a>SSMA v 7.3

A versão v 7.3 do SSMA para Access contém as seguintes alterações:

* Métrica de qualidade e conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
* Estrutura de extensibilidade do SSMA exposta por meio dos seguintes itens:
  * Exporte a funcionalidade para um projeto SQL Server Data Tools (SSDT).
    * Agora você pode exportar scripts de esquema do SSMA para um projeto SSDT. Você pode usar os scripts de esquema para fazer alterações de esquema adicionais e implantar seu banco de dados.

        ![Comando Save as SSDT Project](../media/export-schema-scripts_red.png)
  * Bibliotecas que podem ser consumidas pelo SSMA para executar conversões personalizadas.
    * Agora você pode construir código que pode manipular conversões e conversões de sintaxe personalizadas que não eram previamente tratadas pelo SSMA.
      * As instruções sobre como construir um conversor personalizado, juntamente com um projeto de exemplo para conversão, estão disponíveis na postagem do blog que [estende os recursos de conversão do assistente de migração do SQL Server](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Extending-SQL-Server-Migration-Assistant-s-conversion/ba-p/1004181).

## <a name="ssma-v72"></a>SSMA v 7.2

A versão v 7.2 do SSMA para Access contém as seguintes alterações:

* Métrica de qualidade e conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
* Aprimoramentos de telemetria para fornecer melhores pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>SSMA v 7.1

A versão v 7.1 do SSMA para Access contém as seguintes alterações:

* SQL Server 2017 no Windows e Linux CTP1 agora é uma plataforma de destino com suporte para migração. Esse recurso está em visualização técnica e dá suporte à movimentação de esquema e dados para servidores SQL de destino.
* O SSMA agora dá suporte a atualizações automáticas para baixar a versão mais recente do SSMA assim que estiver disponível.
* Os binários instaláveis do SSMA agora são entregues por meio de arquivos de pacote Windows Installer (. msi).

## <a name="may-2016"></a>Maio de 2016

A versão de maio de 2016 do SSMA para Access contém as seguintes alterações:

* Adicionado suporte oficial para o SQL Server 2016.
* Verificação do instalador removida para .NET 2,0.
* Corrigidos `save-project` e `open-project` comandos para o console do SSMA.
* `securepassword`Comando fixo para o console do SSMA.
* Contagem fixa de objetos para carregamento inicial.
* Carregamento de dados de tabelas fixas para guias de interface do usuário para acesso.
* Corrigido o bug nas configurações globais.

## <a name="march-2016"></a>Março de 2016

A versão de visualização de março de 2016 do SSMA para Access adiciona suporte para migração para o SQL Server 2016.

## <a name="january-2016"></a>Janeiro de 2016

A versão de manutenção de janeiro de 2016 do SSMA para Access contém as seguintes alterações:

* Função inválida corrigida para o padrão de um campo GUID (RFC 3894811).
* Foi corrigido um travamento ao importar registros para o banco de dados SQL (Azure) (RFC 4919573).
* Item de menu Exibir log adicionado ao SSMA (RFC 5706203).
* Telemetria adicionada.

## <a name="july-2014"></a>Julho de 2014

A versão de julho de 2014 do SSMA para Access contém as seguintes alterações:

* Conversão de código do BD SQL do Azure aprimorada.
* Funcionalidade do pacote de extensão movida para o esquema para dar suporte ao BD SQL do Azure.
* Aprimoramentos de desempenho testados para bancos de dados com mais de 10 mil objetos.
* Foram adicionadas melhorias na interface do usuário para lidar com um grande número de objetos.
* Adicionado suporte para realce de esquemas LOB "bem conhecidos" (para que eles possam ser ignorados na conversão).
* Melhorias na velocidade de conversão adicionada.
* Adicionado suporte para mostrar contagens de objeto na interface do usuário.
* Tamanho de relatório reduzido em mais de 25%.
* Mensagens de erro aprimoradas para construções não analisadas.

## <a name="april-2014"></a>Abril de 2014

A versão de abril de 2014 do SSMA para Access contém as seguintes alterações:

* Adicionado suporte para MS SQL Server 2014.
* Correção de bugs relacionados à conversão no Azure.
* Correção de bugs relacionados a páginas de relatório invisíveis no IE 10.

## <a name="january-2012"></a>Janeiro de 2012

A versão de janeiro de 2012 do SSMA para Access contém as seguintes alterações:

* Forneceu a opção de não persistir o nome de usuário e a senha para tabelas vinculadas do MS Access após a migração.
* Defina ações em cascata para referências circulares para nenhuma ação.
* Foram fornecidas mensagens apropriadas indicando que as ações em cascata para referências circulares foram definidas como nenhuma ação.

## <a name="july-2011"></a>julho de 2011

A versão de julho de 2011 do SSMA para Access adiciona relatórios de erros aprimorados durante a migração de dados.

## <a name="april-2011"></a>Abril de 2011

A versão de abril de 2011 do SSMA para Access contém as seguintes alterações:

* Adicionada uma única instalação do "SSMA para acesso", que dá suporte ao [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] , ao [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] e ao [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] SQL do Azure.
* Adicionada a capacidade de se conectar ao [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] .
* Adicionado suporte à versão do console do SSMA para Access para compatibilidade com versões anteriores. Você pode abrir os projetos criados por versões anteriores ao SSMA v 5.0.
* Foi adicionada a capacidade de instalar o produto SSMA v 5.0 lado a lado (SxS) com versões mais antigas do produto SSMA.

## <a name="july-2010"></a>Julho de 2010

A versão de julho de 2010 do SSMA para Access contém as seguintes alterações:

* Adicionado suporte para migrar para o SQL Server 2008 R2 e o SQL do Azure.
* Adicionada uma conexão segura ao SQL Server e ao SQL do Azure.
* Adicionado suporte para bancos de dados do Access 2010.
* Adicionou um novo aplicativo de console do SSMA para execução de linha de comando.
* Adicionado suporte para o `DateTime2` tipo de dados SQL Server.

## <a name="june-2008"></a>Junho de 2008

A versão de junho de 2008 do SSMA para Access adiciona suporte para bancos de dados do Access 2007.

## <a name="may-2007"></a>Maio de 2007

A versão de maio de 2007 do SSMA para Access contém as seguintes alterações:

* Adicionado suporte para bancos de dados do Access que usam políticas de grupo de trabalho.
* Fornecida a capacidade de excluir objetos convertidos do SQL Server Gerenciador de metadados.
* Adicionado suporte para comentários inseridos pelo usuário no modo SQL SQL Server formatado.
* Melhorias adicionadas na conversão de objetos.

## <a name="november-2006"></a>Novembro de 2006

A versão de novembro de 2006 do SSMA para Access contém as seguintes alterações:

* Foi adicionado um novo assistente de migração de banco de dados que o orienta pela migração de um banco de dados individual do acesso ao [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] .
* Adicionado um novo comando converter, carregar e migrar que converte bancos de dados do Access, carrega os objetos convertidos em [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] e os migra para [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] todos em uma só etapa.
* Migração de consulta aprimorada. A migração de consulta agora converte mais consultas SELECT em exibições. Para obter mais informações, consulte [convertendo objetos de banco de dados do Access](converting-access-database-objects-accesstosql.md).
* Adicionada a capacidade de editar propriedades de tabela e índice na [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] guia **tabela** .
* Novas configurações globais foram adicionadas:
  * Você pode optar por Mostrar números de linha nas janelas do editor.
  * Você pode configurar o SSMA para solicitar a substituição de objetos duplicados ou sempre ou nunca substituir objetos duplicados durante a conversão do esquema.
* Adicionada uma nova opção de conversão que permite especificar se o SSMA exibe um aviso quando uma consulta complexa contém um curinga.

## <a name="july-2006"></a>Julho de 2006

A versão de julho de 2006 do SSMA para acesso foi a versão inicial.
