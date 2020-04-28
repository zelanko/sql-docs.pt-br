---
title: O que há de novo no Assistente de Migração de Dados (SQL Server) | Microsoft Docs
description: Saiba mais sobre os novos recursos em cada versão do Assistente de Migração de Dados para SQL Server e o banco de dados SQL do Azure.
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: b5caa8b63175447daa04198768a67e7fe5e59c81
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78896802"
---
# <a name="whats-new-in-data-migration-assistant"></a>Novidades do Assistente de Migração de Dados

Este artigo lista as adições em cada versão do Assistente de Migração de Dados.

## <a name="data-migration-assistant-v-50"></a>Assistente de Migração de Dados v 5,0

A versão v 5.0 do Assistente de Migração de Dados fornece suporte para:

- SQL Server 2019 para Windows e SQL Server 2019 para Linux como destinos para avaliação e atualização.
- Salvar e carregar avaliações, incluindo suporte para salvar e carregar avaliações criadas em versões anteriores do Assistente de Migração de Dados.
- Avaliando projetos do SQL Server Integration Services (SSIS) hospedados em pacotes SSISDB e SSIS hospedados no repositório de pacotes. O Assistente de Migração de banco de dados detecta recursos sem suporte, parcialmente suportados ou preteridos e problemas de compatibilidade que são usados em pacotes de origem e fornece recomendações para ajudá-lo a resolver esses problemas.
- Avaliando consultas SQL de aplicativo externo, por exemplo, consultas SQL no código-fonte C#. Os usuários podem usar o kit de ferramentas de migração de acesso a dados para gerar um relatório JSON completo para as consultas SQL usadas no código-fonte C# e, em seguida, carregar o relatório para Assistente de Migração de Dados.

Além disso, esta versão do Assistente de Migração de Dados fornece aprimoramentos adicionais e correções de bugs, e a ferramenta foi atualizada para o .NET 4.7.2.

## <a name="data-migration-assistant-v45"></a>Assistente de Migração de Dados v 4.5

A versão v 4.5 do Assistente de Migração de Dados fornece suporte para a avaliação da migração de pacotes SQL Server Integration Services (SSIS) hospedados no sistema de arquivos para o banco de dados SQL do Azure ou a instância gerenciada do banco de dados SQL do Azure.

## <a name="data-migration-assistant-v44"></a>Assistente de Migração de Dados v 4.4

A versão v 4.4 do Assistente de Migração de Dados fornece suporte para upload de Avaliações para migrações do Azure.

## <a name="data-migration-assistant-v43"></a>Assistente de Migração de Dados v 4.3

A versão v 4.3 do Assistente de Migração de Dados fornece suporte para:

- Recomendações de SKU para instâncias gerenciadas do banco de dados SQL do Azure baseadas na avaliação de carga de trabalho
- RDS SQL Server como uma fonte para avaliações.
- Avaliações de trabalho do agente para instância gerenciada do banco de dados SQL do Azure como um destino.
- A capacidade de ignorar determinadas regras de avaliação; a lista de códigos de erro especificados na propriedade ' ignoreErrorCodes ' configurada no DMA não aparecerá nos resultados da avaliação de DMA.
- Avaliação de consultas T-SQL em etapas de atividade de trabalho e fornecimento de recomendações apropriadas
- Avaliações de eventos estendidos (visualização pública).

Além disso, esta versão do DMA fornece um desempenho aprimorado para lidar com um grande número de objetos de esquema em bancos de dados, bem como correções de bugs relacionadas a:

- Procedimentos compilados com compilação nativa, em alguns casos.
- Esquemas de banco de dados complicados.

## <a name="data-migration-assistant-v42"></a>Assistente de Migração de Dados v 4.2

A versão v 4.2 do Assistente de Migração de Dados fornece suporte de linha de comando para avaliação de prontidão de destino para uma ou mais instâncias de servidor ao migrar do SQL Server local para uma instância gerenciada do banco de dados SQL do Azure. Agora, os clientes podem usar a linha de comando Assistente de Migração de Dados para coletar metadados sobre seu esquema de banco de dados, detectar os bloqueadores e saber mais sobre recursos com suporte parcial ou sem suporte que afetam a migração para uma instância gerenciada do banco de dados SQL do Azure. Os resultados podem ser renderizados usando o modelo de Power BI fornecido.

## <a name="data-migration-assistant-v41"></a>Assistente de Migração de Dados v 4.1

A versão v 4.1 do Assistente de Migração de Dados introduz o suporte para uma avaliação abrangente de bancos de dados de SQL Server locais migrando para a instância gerenciada do Azure SQL Database.

O fluxo de trabalho de avaliação ajuda a detectar os seguintes problemas, o que pode afetar sua migração para a instância gerenciada do banco de dados SQL do Azure:

- **Recursos sem suporte ou com suporte parcial**. Assistente de Migração de Dados avalia seu banco de dados de SQL Server de origem para recursos em uso que têm suporte parcial ou sem suporte no Instância Gerenciada do Banco de Dados SQL do Azure de destino. Em seguida, a ferramenta fornece um conjunto abrangente de recomendações, abordagens alternativas disponíveis no Azure e etapas de mitigação para que os clientes possam levar essas informações em conta ao planejar seus projetos de migração.

- **Problemas de compatibilidade**. Assistente de Migração de Dados também identifica problemas de compatibilidade relacionados às seguintes áreas:

  - Alterações significativas: os objetos de esquema específicos que podem interromper a funcionalidade que está migrando para o banco de dados de destino.  É recomendável corrigir esses objetos de esquema após a migração do banco de dados.
  - Alterações comportamentais: os objetos de esquema relatados podem continuar a funcionar, mas podem apresentar um comportamento diferente, por exemplo, degradação de desempenho.
  - Problemas informativos: esses objetos não afetarão a migração, mas podem ter sido preteridos do recurso SQL Server versões.

Após a conclusão da avaliação, use o [serviço de migração de banco de dados do Azure](https://azure.microsoft.com/services/database-migration/) (DMS) para executar a migração de seus bancos de dados do SQL Server para instância gerenciada do banco de dados SQL do Azure.  O DMS dá suporte a migrações de banco de dados [offline](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance) (única) e [online](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online) (tempo de inatividade mínimo) para instância gerenciada do banco de dados SQL do Azure.

## <a name="data-migration-assistant-v40"></a>Assistente de Migração de Dados v 4.0

A versão v 4.0 do Assistente de Migração de Dados introduz o recurso recomendações de SKU do banco de dados SQL do Azure, que permite aos usuários identificar o SKU mínimo recomendado do banco de dados SQL do Azure com base em contadores de desempenho coletados do (s) computador (es) que hospedam seus bancos de dados. Esse recurso fornece recomendações relacionadas ao tipo de preço, nível de computação e tamanho máximo de dados, bem como ao custo estimado por mês. Ele também oferece a capacidade de provisionar todos os seus bancos de dados no Azure em massa.

> [!NOTE]
> Essa funcionalidade está disponível no momento apenas por meio da CLI (interface de linha de comando).

Para obter mais detalhes, consulte o artigo [identificar o SKU do banco de dados SQL do Azure correto para seu banco de dados local](dma-sku-recommend-sql-db.md).

## <a name="data-migration-assistant-v36"></a>Assistente de Migração de Dados v 3.6

A versão v 3.6 do Assistente de Migração de Dados apresenta a "correção automática" para os objetos de esquema que são afetados pelos bloqueadores de migração mais comuns.

Esta versão fornece AutoFix para o seguinte bloqueador de migração e problemas de alteração de comportamento:

- Os objetos de esquema que usam sintaxe de junção não qualificada.
- Os objetos de esquema que usam a instrução RAISEERROR herdada.
- Instruções SQL que usam o valor de literal de ordem por inteiro.

Assistente de Migração de Dados executa a conversão automática de esquema para os objetos afetados pelos problemas listados e solicita a confirmação do usuário antes de prosseguir com a conversão do esquema. Os usuários podem revisar as alterações de código sugeridas e aceitar ou rejeitar todas as conversões para qualquer objeto de banco de dados específico.

O Assistente de Migração de Dados usa a tecnologia de síntese de programa da Microsoft (PROSEWARE) para sugerir as correções de código. Saiba mais sobre o [Proseware](https://microsoft.github.io/prose/).

## <a name="data-migration-assistant-v35"></a>Assistente de Migração de Dados v 3.5

A versão v 3.5 do Assistente de Migração de Dados inclui as seguintes adições:

- Melhorias significativas de desempenho para migrar para o banco de dados SQL do Azure (testes de benchmark indicam que o processo é quatro vezes mais rápido do que com as versões anteriores do Assistente de Migração de Dados).
- O volume de memória é otimizado para melhorar a estabilidade do fluxo de trabalho de migração.
- A capacidade de ignorar avaliações durante as migrações de esquema e dados (se você já realizou a avaliação e resolveu quaisquer objetos de esquema de quebra antes da migração).
- Uma correção para resolver um problema com a ferramenta falha quando um caminho de compartilhamento de rede inválido é fornecido para arquivos de backup, ao executar uma atualização de uma versão herdada do SQL Server local para uma versão posterior ou para SQL Server em VMs do Azure.

## <a name="data-migration-assistant-v34"></a>Assistente de Migração de Dados v 3.4

A versão v 3.4 do Assistente de Migração de Dados inclui as seguintes adições:

- Suporte para SQL Server 2017 como uma fonte de migrações para o banco de dados SQL do Azure.
- Aprimoramentos em estabilidade, desempenho e exatidão da regra de avaliação.

## <a name="ddata-migration-assistant-v33"></a>Repositório Assistente de Migração v 3.3

A versão v 3.3 do Assistente de Migração de Dados permite a migração de uma instância de SQL Server local para a nova versão do SQL Server 2017, no Windows e no Linux. Embora o fluxo de trabalho de migração geral para Windows e Linux seja o mesmo, a mudança para o SQL Server 2017 para Linux requer algumas considerações adicionais.

### <a name="specifying-the-back-up-path"></a>Especificando o caminho de backup

O Linux e o Windows usam formatos de caminho diferentes. Como resultado, migrar para o SQL Server 2017 no Linux requer que o usuário forneça as versões Windows e Linux do caminho para o local do arquivo físico. Você pode fornecer as duas versões do caminho de maneiras diferentes, dependendo do local do arquivo físico.
Se o arquivo de backup físico estiver em um computador que executa o:

- Linux, use um compartilhamento ' samba ' para compartilhar o arquivo com outros computadores na rede.
- Windows, use o comando ' mnt ' para montar o compartilhamento no computador que executa o Linux.

> [!NOTE]
> Os detalhes do uso de um compartilhamento ' samba ' ou do comando ' mnt ' estão além do escopo deste artigo.

### <a name="migrating-windows-logins"></a>Migrando logons do Windows

Embora a migração de logons do Active Directory (AD) seja oficialmente suportada pelo SQL Server 2017 no Linux, ela requer configuração adicional para funcionar com êxito. Consulte o artigo [Active Directory autenticação com SQL Server em Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication) para obter informações detalhadas sobre como configurar Active Directory logons no SQL Server 2017 no Linux. Depois de executar a configuração necessária, a instalação será concluída e você poderá migrar Active Directory logons como de costume. A autenticação padrão do SQL funciona conforme o esperado sem nenhuma configuração adicional.

## <a name="data-migration-assistant-v32"></a>Assistente de Migração de Dados v 3.2

A versão v 3.2 do Assistente de Migração de Dados inclui as seguintes adições:

- A migração de esquema e de dados é habilitada no local SQL Server bancos de dados para o banco de dado SQL do Azure com um novo fluxo de trabalho de migração.
- Durante a migração de esquema para o banco de dados SQL do Azure, os scripts de DMA de seus objetos de banco de dados de origem, fornecem orientação sobre como corrigir possíveis problemas de compatibilidade e, em seguida, implanta seu esquema no Azure.

## <a name="data-migration-assistant-v31"></a>Assistente de Migração de Dados v 3.1

A versão v 3.1 do Assistente de Migração de Dados inclui as seguintes adições:

- Recomendações de avaliação aprimoradas para bancos de dados SQL do Azure em termos de agrupamentos de banco de dados, uso de procedimentos armazenados do sistema sem suporte e objetos CLR.
- Diretrizes de avaliação para os níveis de compatibilidade 130, 120, 110 e 100 ao migrar para bancos de dados SQL do Azure.

## <a name="data-migration-assistant-v30"></a>Assistente de Migração de Dados v 3.0

A versão v 3.0 do Assistente de Migração de Dados estende a avaliação do banco de dados SQL do Azure para fornecer recomendações abrangentes para ajudar a corrigir problemas relacionados a:

- Problemas de bloqueio de migração.
- Funções e recursos parcialmente ou sem suporte.

## <a name="data-migration-assistant-v21"></a>Assistente de Migração de Dados v 2.1

A versão v 2.1 do Assistente de Migração de Dados inclui as seguintes adições:

- Suporte de linha de comando para executar avaliações em um modo autônomo, o que ajuda a executar avaliações em escala. Para obter detalhes adicionais, consulte o artigo [executar assistente de migração de dados na linha de comando](dma-commandline.md).
- Melhorias de desempenho quando os usuários iniciam e fecham o DMA.
- A capacidade de configurar o tempo limite da conexão SQL. Para obter mais detalhes, consulte as [definições de configuração do artigo para assistente de migração de dados](dma-configurationsettings.md).

## <a name="data-migration-assistant-v20"></a>Assistente de Migração de Dados v 2.0

A versão v 2.0 do Assistente de Migração de Dados inclui recomendações de recurso de Stretch Database aprimoradas para fornecer tabelas priorizadas adequadas que maximizam a economia de armazenamento.

## <a name="data-migration-assistant-v10"></a>Assistente de Migração de Dados v 1.0

A versão v 1.0 do Assistente de Migração de Dados é a versão inicial e fornece para:

- Descoberta de problemas que podem afetar uma atualização para uma versão local do SQL Server. Quaisquer descobertas são descritas como problemas de compatibilidade e elas são categorizadas nas seguintes áreas:
  - Alterações de quebra
  - Alterações de comportamento
  - Recursos preteridos
- Descoberta de novos recursos na plataforma de SQL Server de destino para as quais o banco de dados pode se beneficiar após uma atualização. Quaisquer descobertas são descritas como recomendações de recurso e elas são categorizadas nas seguintes áreas:
  - Desempenho
  - Segurança
  - Armazenamento
- Experiência de usuário moderna para realizar avaliações.

## <a name="see-also"></a>Confira também

[Visão geral do Assistente de Migração de Dados](../dma/dma-overview.md)
