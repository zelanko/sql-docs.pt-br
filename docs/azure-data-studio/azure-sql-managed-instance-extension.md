---
title: Extensão Instância Gerenciada do Banco de Dados SQL do Azure
titleSuffix: Azure Data Studio
description: Usar o Azure Data Studio com a Instância Gerenciada do SQL do Azure
ms.custom: seodec18
ms.date: 10/07/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
manager: alanyu
ms.openlocfilehash: d443292fb091679d3d6a18d557a5a7aac464fdec
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041144"
---
# <a name="managed-instance-support-for-azure-data-studio-preview"></a>Suporte de Instância Gerenciada do Azure Data Studio (versão prévia)

Essa extensão permite que você trabalhe com a [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index) no [Azure Data Studio](https://github.com/Microsoft/azuredatastudio). Essa extensão fornece os seguintes recursos:

- Exibição de propriedades de instância gerenciada (vCores, armazenamento usado).
- Monitoramento do uso de CPU e armazenamento nas últimas duas horas.
- Exibição das recomendações de aviso de configuração e de ajuste.
- Exibição do estado das réplicas de bancos de dados.
- Exibição de logs de erros filtrados.

## <a name="installations"></a>Instalações

É possível instalar a versão oficial da extensão Instância Gerenciada seguindo as etapas na [documentação do Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/extensions).
No painel Extensões, pesquise e instale a extensão "Instância Gerenciada".  Você será notificado automaticamente sobre atualizações futuras de extensão!

Depois de instalar a extensão Instância Gerenciada, você verá a guia `Managed Instance` no Azure Data Studio. Nessa guia, é possível encontrar informações específicas para a Instância Gerenciada.

## <a name="properties"></a>Propriedades

Essa extensão permite ver características técnicas de sua Instância Gerenciada e do uso de alguns recursos.

![Propriedades de instâncias gerenciadas](media/azure-sql-mi-extension/ads-mi-tab1.png)

Na primeira folha, você pode ver os seguintes detalhes:

- **Propriedades básicas**, como número disponível de vCores, memória, armazenamento, geração de hardware e camada de serviço atual e características de E/S, como a taxa de transferência de gravação de log de instância ou características de E/S de arquivo/taxa de transferência.
- **Uso do armazenamento SSD local**. Na camada de serviço de Uso geral, somente os arquivos **TEMPDB** são colocados localmente. Já na camada Comercialmente crítica, todos os arquivos de bancos de dados são colocados no armazenamento SSD local. Nessa seção, você pode ver quanto espaço do armazenamento local é usado pela Instância Gerenciada.
- **Uso do Armazenamento em Disco do Azure Premium** – os bancos de dados do sistema e do usuário na camada de serviço de Uso geral são colocados no Armazenamento Premium do Azure. Aqui, você pode encontrar a quantidade de dados usada, qual é o armazenamento restante e o número de arquivos. Na camada de serviço Comercialmente crítica, essa seção fica vazia.
- O **Uso de recursos** mostra a quantidade de armazenamento e a CPU que sua instância usou nas últimas duas horas. Aumente o tamanho da instância caso você esteja atingindo o limite.

## <a name="recommendations"></a>Recomendações

Essa extensão fornece algumas recomendações e alertas que podem ajudar você a otimizar sua Instância Gerenciada.

![Recomendações para instâncias gerenciadas](media/azure-sql-mi-extension/ads-mi-tab2.png)

Algumas das recomendações mostradas nesta tabela são:

- Atingir o limite de espaço de armazenamento – você deve excluir dados desnecessários ou aumentar o tamanho do armazenamento de instância, pois os bancos de dados que atingirem o limite de armazenamento poderão falhar ao processar até mesmo consultas lidas.
- Atingir o limite geral da instância – se você estiver carregando ~22 MB/s em GP ou ~48 MB/s em BC, a instância gerenciada limitará sua carga para garantir que seja possível executar os backups.
- Demanda de memória – a Duração prevista da página baixa ou muitas estatísticas de espera de `PAGEIOLATCH` podem indicar que sua instância está removendo páginas da memória e tentando constantemente carregar mais páginas do disco.
- Limites do arquivo de log – caso os logs estejam atingindo os [limites de E/S de arquivo na camada de serviço de Uso geral](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier), talvez seja necessário aumentar o tamanho do arquivo para melhorar o desempenho.
- Limites do arquivo de dados – caso os arquivos de dados logs estejam atingindo os [limites de E/S de arquivo na camada de serviço de Uso geral](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier), talvez seja necessário aumentar o tamanho do arquivo para melhorar o desempenho. Esse problema pode causar demanda de memória e reduzir os backups.
- Problemas de disponibilidade – um grande número de arquivos de log virtuais pode impactar o desempenho e a recuperação de banco de dados mais longos em potencial na camada de serviço de Uso geral em caso de falha do processo.

Examine periodicamente essas recomendações, investigue as causas raiz e providencie ações corretivas. A extensão Instância Gerenciada fornece os scripts que você pode executar para atenuar alguns dos problemas relatados.

## <a name="replicas"></a>Réplicas

A extensão Instância Gerenciada permite que você veja o estado das réplicas de bancos de dados em sua instância gerenciada.

![Réplicas de instâncias gerenciadas](media/azure-sql-mi-extension/ads-mi-tab3.png)

Na camada de serviço de Uso geral, cada banco de dados tem uma única réplica (primária), já na instância comercialmente crítica, cada banco de dados tem uma réplica primária e três réplicas secundárias (uma é usada para cargas de trabalho somente leitura). Aqui você pode monitorar o processo de sincronização e verificar se todas as réplicas secundárias estão sincronizadas com a réplica primária.

## <a name="logs"></a>Logs

A extensão Instância Gerenciada mostra as últimas entradas de log de erros do SQL mais relevantes.

![Entradas de log de instância gerenciada](media/azure-sql-mi-extension/ads-mi-tab4.png)

A Instância Gerenciada emite um grande número de entradas de log, e a maioria contém informações internas ou do sistema. Algumas entradas de log mostram nomes de bancos de dados físicos (valores `GUID`) em vez de nomes de banco de dados lógicos reais.

A extensão Instância Gerenciada filtra e retira as entradas de log desnecessárias com base no [método Dimitri Furman](https://techcommunity.microsoft.com/t5/DataCAT/Azure-SQL-DB-Managed-Instance-sp-readmierrorlog/ba-p/305506) e exibe nomes de arquivos lógicos reais, em vez de nomes físicos.

## <a name="reporting-problems"></a>Relatar problemas

Se você tiver problemas com a extensão Instância Gerenciada, relate o problema no [projeto da extensão no GitHub](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/issues).

## <a name="maintainers"></a>Mantenedores

- [Jovan Popovic(MSFT)](https://github.com/jovanpop_msft) - [@jovanpop_msft](https://twitter.com/JovanPop_MSFT)

## <a name="code-of-conduct"></a>Código de conduta

Este projeto adotou o [Código de Conduta de Software Livre da Microsoft][conduct-code].
Para saber mais, confira as [Perguntas frequentes sobre o Código de Conduta][conduct-FAQ] ou contate o [opencode@microsoft.com][conduct-email] caso tenha outras dúvidas ou comentários.

[conduct-code]: http://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: http://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[conduct-md]: https://github.com/PowerShell/vscode-powershell/blob/master/CODE_OF_CONDUCT.md
