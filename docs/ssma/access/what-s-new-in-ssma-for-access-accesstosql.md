---
title: Novidades no SSMA for Access (AccessToSQL) | Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
ms.author: jtoland;alexiva
ms.openlocfilehash: 2fd3da31e6a635a65f3d2a2f75320dd0586159d9
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625578"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>O que há de novo no SSMA para acesso (AccessToSQL)

Este artigo lista o SQL Server Migration Assistant (SSMA) para alterações de acesso em cada versão.

## <a name="ssma-v88"></a>SSMA v8.8

A versão v8.8 do SSMA for Access inclui:

* Melhorias na estabilidade da sincronização de objetos sql
* Melhorias no desempenho da GUI durante a avaliação e conversão
* Novo analisador de sintaxe access para melhorar ainda mais o desempenho de conversão

## <a name="ssma-v87"></a>SSMA v8.7

A versão v8.7 do SSMA for `IIF` Access melhorou a conversão para função em consultas, bem como pequenas correções e melhorias de desempenho na interface gráfica do usuário.

> [!IMPORTANT]
> Com o SSMA v8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v8.6

Além de um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho, a versão v8.6 do SSMA for Access foi aprimorada adicionando uma configuração que permite que os usuários omitam propriedades estendidas sSMA no código convertido.

Para aproveitar essa configuração, no SSMA for Access, navegue até as**configurações** > gerais do projeto **de ferramentas** > **conversão****geral** > e, em seguida, em **Misc,** atualize o valor da configuração **Propriedades Estendidas omitis** para **Sim**.

![Omita configuração de propriedades estendidas](../access/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> Com o SSMA v8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v8.5

A versão v8.5 do SSMA for Access é aprimorada com suporte para autenticação do Azure Active Directory e suporte básico para recursos JSON no servidor SQL, juntamente com um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho.

Além disso, o SSMA for Access agora suporta`ISNULL` `IIF`a conversão de múltiplas funções padrão (, etc.).

> [!IMPORTANT]
> Com o SSMA v8.5, .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v8.4

A versão v8.4 do SSMA for Access é aprimorada com correções direcionadas que são projetadas para resolver problemas de acessibilidade e corrigir um bug relacionado às colunas de índice max (para permitir 32 em vez de 16) para as versões SQL Server 2016 e posteriores.

> [!IMPORTANT]
> Com as versões SSMA 7.4 embora 8.4, .NET 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v83"></a>SSMA v8.3

A versão v8.3 do SSMA for Access é aprimorada com correções direcionadas que são projetadas para melhorar as métricas de qualidade e conversão. Além disso, esta versão do SSMA for Access fornece correções que:

* Abordar problemas de acessibilidade.
* Adicione suporte `hierarchyid` básico para o tipo no SQL Server.

## <a name="ssma-v82"></a>SSMA v8.2

A versão v8.2 do SSMA for Access é aprimorada com correções direcionadas que são projetadas para melhorar as métricas de qualidade e conversão.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v8.1 para o v8.2. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

A versão v8.1 do SSMA for Access é aprimorada com correções direcionadas que são projetadas para melhorar as métricas de qualidade e conversão.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v8.0 para v8.1. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

A versão v8.0 do SSMA for Access é aprimorada com correções direcionadas projetadas para melhorar as métricas de qualidade e conversão. Esta versão também oferece os seguintes novos recursos:

* Suporte à instância gerenciada do banco de **dados SQL do Azure** como alvo. Agora você pode criar novos projetos direcionados à instância gerenciada do banco de dados SQL do Azure:

  ![Projeto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Orientador de **correção pós-conversão**. Saiba mais sobre isso [aqui](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Accelerate-your-Oracle-migrations-with-new-machine-learning/ba-p/368733).

* Base de dados preliminar/seleção de esquemas.

    Ao se conectar à fonte, o usuário agora pode selecionar bancos de dados/esquemas de interesse. Selecionar apenas os esquemas que você planeja migrar economizará tempo durante a conexão inicial e melhorará o desempenho geral do SSMA.

   ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

A versão v7.10 do SSMA for Access é aprimorada com correções direcionadas projetadas para fornecer proteções adicionais de segurança e privacidade para atender às mudanças nos requisitos globais.

## <a name="ssma-v79"></a>SSMA v7.9

A versão v7.9 do SSMA for Access contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Suporte na linha de comando SSMA para alterar mapeamento de tipo de dados e preferências de projeto.
* A caixa de diálogo de conexão Banco de dados Azure SQL no SSMA também foi alterada para especificar o nome do servidor totalmente qualificado. Nas versões anteriores do SSMA, o prefixo do Banco de Dados SQL do Azure tinha que ser explicitamente mencionado dentro das configurações dos projetos.

## <a name="ssma-v78"></a>SSMA v7.8

A versão v7.8 do SSMA for Access contém as seguintes alterações:

* Alterar mapeamento de tipo destacado nas Configurações do projeto.
* A capacidade dos usuários de desativar a telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

A versão v7.7 do SSMA for Access contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Com base na demanda popular, a versão de 32 bits do SSMA for Access está de volta. Em comparação com a implementação anterior (antes do v7.4), existem dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base nos componentes de conectividade que você tem. É sempre preferível usar a versão de 64 bits, se possível.

## <a name="ssma-v76"></a>SSMA v7.6

A versão v7.6 do SSMA for Access é aprimorada com correções direcionadas que melhoram as métricas de qualidade e conversão e com suporte para o SQL Server 2017 (visualização pública). O suporte ao SQL Server 2017 no Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

## <a name="ssma-v75"></a>SSMA v7.5

A versão v7.5 do SSMA for Access é aprimorada com várias melhorias para garantir maior acessibilidade para pessoas com deficiência.

## <a name="ssma-v74"></a>SSMA v7.4

A versão v7.4 do SSMA for Access contém as seguintes alterações:

* A **opção de tempo de tempo de consulta** está agora disponível durante a descoberta de objetos de esquema na origem e no destino.

  ![opção de tempo de consulta](../media/query-timeout_red.png)

* A métrica de qualidade e conversão foi melhorada com correções direcionadas, com base no feedback do cliente.

  > [!IMPORTANT]
  > .NET 4.5.2 é um pré-requisito para instalar o SSMA v7.4. Além disso, começando com o v7.4, a versão de 32 bits do SSMA foi descontinuada.

## <a name="ssma-v73"></a>SSMA v7.3

A versão v7.3 do SSMA for Access contém as seguintes alterações:

* Melhor qualidade e métrica de conversão com correções direcionadas com base no feedback do cliente.
* Estrutura de extensibilidade ssma exposta através dos seguintes itens:
  * Exportar funcionalidade para um projeto SSDT (SSDT) de SQL Server Data Tools.
    * Agora você pode exportar scripts de esquema de SSMA para um projeto SSDT. Você pode usar os scripts do esquema para fazer alterações adicionais de esquema e implantar seu banco de dados.

        ![Salvar como comando de projeto SSDT](../media/export-schema-scripts_red.png)
  * Bibliotecas que podem ser consumidas pela SSMA para realizar conversões personalizadas.
    * Agora você pode construir códigos que podem lidar com conversões e conversões de sintaxe personalizadas que não foram tratadas anteriormente pela SSMA.
      * Instruções sobre como construir um conversor personalizado, juntamente com um projeto de amostra para conversão, estão disponíveis no post do blog Estendendo os [recursos de conversão do SQL Server Migration Assistant](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Extending-SQL-Server-Migration-Assistant-s-conversion/ba-p/1004181).

## <a name="ssma-v72"></a>SSMA v7.2

A versão v7.2 do SSMA for Access contém as seguintes alterações:

* Melhor qualidade e métrica de conversão com correções direcionadas com base no feedback do cliente.
* Melhorias na telemetria para fornecer melhores pontos de dados para solucionar problemas dos clientes e melhorar as taxas de conversão da SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

A versão v7.1 do SSMA for Access contém as seguintes alterações:

* O SQL Server 2017 no Windows e linux CTP1 é agora uma plataforma-alvo suportada para migração. Esse recurso está na pré-visualização técnica e suporta esquema e movimentação de dados para direcionar servidores SQL.
* O SSMA agora suporta atualizações automáticas para baixar a versão mais recente do SSMA assim que estiver disponível.
* Binários instalados do SSMA agora são entregues através de arquivos de pacote do Windows Installer (.msi).

## <a name="may-2016"></a>Maio de 2016

A versão de maio de 2016 do SSMA for Access contém as seguintes alterações:

* Adicionado suporte oficial ao SQL Server 2016.
* Verificação do instalador removido para .NET 2.0.
* Fixo `save-project` `open-project` e comandos para console SSMA.
* Comando `securepassword` fixo para console SSMA.
* Contagem fixa de objetos para carregamento inicial.
* Corrigimos o carregamento de dados de tabelas para guias de ia livre para acesso.
* Corrigido bug em configurações globais.

## <a name="march-2016"></a>Março de 2016

A versão de pré-visualização de março de 2016 do SSMA for Access adiciona suporte para migração para o SQL Server 2016.

## <a name="january-2016"></a>Janeiro de 2016

A versão de manutenção de janeiro de 2016 do SSMA for Access contém as seguintes alterações:

* Corrigida função inválida para padrão de um campo GUID (RFC 3894811).
* Fixo hang on importing records to SQL Database (Azure) (RFC 4919573).
* Adicionado Ver o item do menu de log ao SSMA (RFC 5706203).
* Adicionado Telemetria.

## <a name="july-2014"></a>Julho de 2014

A versão de julho de 2014 do SSMA for Access contém as seguintes alterações:

* Conversão aprimorada do código Azure SQL DB.
* Mudou a funcionalidade do pacote de extensão para esquema para suportar o Azure SQL DB.
* Testei melhorias de desempenho para bancos de dados com mais de 10k objetos.
* Adicionamos melhorias de IU para lidar com um grande número de objetos.
* Adicionado suporte para destacar de esquemas LOB "bem conhecidos" (para que possam ser ignorados na conversão).
* Adicionado melhorias na velocidade de conversão.
* Suporte adicionado para mostrar contagens de objetos em UI.
* Tamanho do relatório reduzido em mais de 25%.
* Mensagens de erro melhoradas para construções não parsed.

## <a name="april-2014"></a>Abril de 2014

A versão de abril de 2014 do SSMA for Access contém as seguintes alterações:

* Suporte adicionado ao MS SQL Server 2014.
* Corrigimos bugs relacionados à conversão para o Azure.
* Corrigimos bugs relacionados a páginas de relatórios invisíveis no IE 10.

## <a name="january-2012"></a>Janeiro de 2012

A versão de janeiro de 2012 do SSMA for Access contém as seguintes alterações:

* Desde que não persista o nome de usuário e a senha para tabelas vinculadas ao MS Access após a migração.
* Defina ações em cascata para referências circulares ao No Action.
* Desde que as mensagens adequadas que indiquem ações em cascata para referências circulares foram definidas como Nenhuma Ação.

## <a name="july-2011"></a>julho de 2011

A versão de julho de 2011 do SSMA for Access adiciona relatórios de erro melhorados durante a migração de dados.

## <a name="april-2011"></a>abril de 2011

A versão de abril de 2011 do SSMA for Access contém as seguintes alterações:

* Adicionada uma única instalação de "SSMA for [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]Access", que suporta , e [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] Azure SQL.
* Adicionada a capacidade [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]de se conectar a .
* Adicionado SSMA para suporte à versão access console para compatibilidade retrógrada. Você pode abrir os projetos criados por versões anteriores ao SSMA v5.0.
* Adicionada a capacidade de instalar o produto SSMA v5.0 lado a lado (SxS) com versões mais antigas do Produto SSMA.

## <a name="july-2010"></a>Julho de 2010

A versão de julho de 2010 do SSMA for Access contém as seguintes alterações:

* Suporte adicionado para migrar para o SQL Server 2008 R2 e Azure SQL.
* Adicionada uma conexão segura ao SQL Server e ao Azure SQL.
* Suporte adicionado aos bancos de dados access 2010.
* Adicionou um novo aplicativo ssma console para execução de linha de comando.
* Adicionado suporte para o `DateTime2` tipo de dados do SQL Server.

## <a name="june-2008"></a>junho de 2008

A versão de junho de 2008 do SSMA for Access adiciona suporte para bancos de dados access 2007.

## <a name="may-2007"></a>maio de 2007

A versão de maio de 2007 do SSMA for Access contém as seguintes alterações:

* Adicionado suporte para bancos de dados de acesso que usam políticas de grupo de trabalho.
* Desde que seja possível excluir objetos convertidos do explorador de metadados do SQL Server.
* Adicionado suporte para comentários inseridos pelo usuário no modo SQL formatado do SQL Server.
* Adicionado melhorias na conversão de objetos.

## <a name="november-2006"></a>novembro de 2006

A versão de novembro de 2006 do SSMA for Access contém as seguintes alterações:

* Adicionada um novo Assistente de Migração de Banco de [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]Dados que o guia através da migração de um único banco de dados do Access to .
* Adicionou um novo comando Converter, Carregar e Migrar que converte bancos de dados access, carrega os objetos convertidos em [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]e migra dados para [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] todos em uma etapa.
* Migração de consulta melhorada. A migração de consulta agora converte mais consultas SELECT em exibições. Para obter mais informações, consulte [Convertendo Objetos do Banco de Dados de Acesso](converting-access-database-objects-accesstosql.md).
* Adicionada a capacidade de editar propriedades [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] de tabela e índice na guia **Tabela.**
* Adicionado novas configurações globais:
  * Você pode optar por mostrar números de linha nas janelas do editor.
  * Você pode configurar o SSMA para solicitar a substituição de objetos duplicados, ou sempre ou nunca substituir objetos duplicados durante a conversão de esquemas.
* Adicionada uma nova opção de conversão que permite especificar se o SSMA exibe um aviso quando uma consulta complexa contém um curinga.

## <a name="july-2006"></a>julho de 2006

O lançamento em julho de 2006 do SSMA for Access foi o lançamento inicial.
