---
title: O que há de novo no Assistente de migração de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2019
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
ms.openlocfilehash: 5251b4da6334e8aeba1c467ff921f6f25b2ab26a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008373"
---
# <a name="whats-new-in-data-migration-assistant"></a>Novidades do Assistente de Migração de Dados
Este artigo lista as adições em cada versão de DMA Data Migration Assistant ().

## <a name="dma-v43"></a>V DMA 4.3

A versão v 4.3 de DMA oferece suporte para:

* Recomendações de SKU para o banco de dados SQL gerenciados instâncias com base na avaliação da carga de trabalho.
* RDS SQL Server como uma fonte para avaliações.
* Avaliações de trabalho do agente para o banco de dados SQL, a instância é gerenciada como um destino.
* A capacidade de ignorar determinadas regras de avaliação. a lista de códigos de erro especificada na propriedade 'ignoreErrorCodes' configurada no DMA não aparecerão nos resultados da avaliação de DMA.
* Avaliação de consultas do T-SQL em etapas da atividade de trabalho e fornecer recomendações apropriadas
* Avaliações de eventos estendidos (visualização pública).

Além disso, esta versão de DMA fornece melhor desempenho para lidar com um grande número de objetos de esquema em bancos de dados, bem como correções de bugs relacionadas a:

* Procedimentos compilados com compilação nativa, em alguns casos.
* Esquemas de banco de dados complexos.

## <a name="dma-v42"></a>O DMA v4.2

A versão v4.2 de DMA fornece suporte de linha de comando para avaliação de prontidão para uma ou mais instâncias do servidor de destino quando a instância gerenciada do Migrando do SQL Server no local para um banco de dados do SQL Azure. Os clientes agora podem usar a linha de comando DMA para reunir metadados sobre seu esquema de banco de dados, detectar os bloqueadores e saiba mais sobre recursos parcialmente compatíveis ou não que afetam a migração para uma instância gerenciada do banco de dados SQL. Os resultados podem então ser processados usando o modelo do Power BI fornecido.

## <a name="dma-v41"></a>V 4.1 DMA

A versão v 4.1 de DMA introduz suporte para uma avaliação abrangente dos bancos de dados do SQL Server local migrando para o banco de dados de instância gerenciada do SQL.

O fluxo de trabalho de avaliação ajuda a detectar os problemas a seguir, que podem afetar sua migração para o banco de dados de instância gerenciada do SQL:

* **Sem suporte ou recursos parcialmente suportados**. O DMA avalia seu banco de dados do SQL Server de origem para os recursos em uso que são parcialmente compatível ou não no destino de banco de dados de instância gerenciada do SQL. A ferramenta, em seguida, fornece um conjunto abrangente de recomendações, abordagens alternativas disponíveis no Azure e etapas de mitigação para que os clientes podem tirar essas informações em consideração ao planejar seus projetos de migração.

* **Problemas de compatibilidade**. O DMA também identifica problemas de compatibilidade relacionados às áreas a seguir:

  * As alterações recentes:  Os objetos de esquema específico que podem interromper a funcionalidade de migração para o banco de dados de destino.  É recomendável corrigir esses objetos de esquema após a migração de banco de dados.
  * Alterações de comportamento: Os objetos de esquema relatados podem continuar a funcionar, mas eles podem apresentar um comportamento diferente, por exemplo degradação do desempenho.
  * Problemas de informação:  Esses objetos não afetarão a migração, mas foi preteridos do recurso de que versões do SQL Server.

Depois que a avaliação for concluída, use nosso [serviço de migração de banco de dados do Azure](https://azure.microsoft.com/services/database-migration/) (DMS) para executar a migração de bancos de dados do SQL Server para o banco de dados de instância gerenciada do SQL.  DMS dá suporte a ambos [offline](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance) (uma vez) e [online](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online) migrações de banco de dados (tempo de inatividade mínimo) para o banco de dados de instância gerenciada do SQL.

## <a name="dma-v40"></a>O DMA v4.0

A versão de v 4.0 de DMA apresenta o recurso de recomendações de SKU de banco de dados SQL do Azure, que permite que os usuários identifiquem o mínimo recomendado de SKU de banco de dados SQL do Azure com base nos contadores de desempenho coletados dos computadores de seus bancos de dados de hospedagem. Esse recurso fornece recomendações relacionadas ao preço da camada, nível de computação e tamanho máximo de dados, bem como o custo estimado por mês. Ele também oferece a capacidade de provisionar todos os seus bancos de dados do Azure em massa.

> [!NOTE]
> Essa funcionalidade está atualmente ser disponibilizado somente por meio da Interface de linha de comando (CLI).

Para obter mais detalhes, consulte o artigo [identificar a SKU certa de banco de dados de SQL do Azure para seu banco de dados local](dma-sku-recommend-sql-db.md).

## <a name="dma-v36"></a>V3.6 DMA

A versão de v3.6 do DMA apresenta "Correção automática" para os objetos de esquema que são afetados pelos bloqueadores de migração mais comuns.

Esta versão fornece correção automática para o Bloqueador de migração a seguir e problemas de mudança de comportamento:

* Os objetos de esquema que usam sintaxe Join não qualificado.
* Os objetos de esquema que usam a instrução RAISEERROR herdada.
* Instruções SQL que usam a ordem por Literal de inteiro.

O DMA executa a conversão automática de esquema para os objetos afetados pelos problemas listados e solicita confirmação antes de prosseguir com a conversão de esquema do usuário. Os usuários podem revisar as alterações de código sugerido e aceitar ou rejeitar todas as conversões de qualquer objeto de banco de dados fornecido.

DMA usa a tecnologia de síntese de programa da Microsoft (PROSA) para sugerir que correções de código. Saiba mais sobre [PROSA](https://microsoft.github.io/prose/).

## <a name="dma-v35"></a>V3.5 DMA

A versão v3.5 de DMA inclui as seguintes adições:

* Melhorias significativas de desempenho para a migração de banco de dados do SQL Azure (testes de benchmark indicam que o processo é quatro vezes mais rápido do que em versões anteriores de DMA).
* O volume de memória é ainda mais otimizado para melhorar a estabilidade do fluxo de trabalho de migração.
* A capacidade de ignorar avaliações durante as migrações de esquema e os dados (se você já realizou a avaliação e resolvidos quaisquer objetos de esquema de quebra antes da migração).
* Uma correção para resolver um problema com a ferramenta de travamento durante um caminho de compartilhamento de rede inválido é fornecido para arquivos de backup, ao realizar uma atualização de uma versão herdada do SQL Server local para uma versão posterior ou ao SQL Server em VMs do Azure.

## <a name="dma-v34"></a>DMA v3.4

A versão de v3.4 de DMA inclui as seguintes adições:

* Suporte para SQL Server 2017 como uma fonte para as migrações para Azure SQL Database.
* Aprimoramentos de estabilidade, desempenho e avaliação de correção de regra.

## <a name="dma-v33"></a>DMA v3.3

A versão v3.3 de DMA permite a migração de uma instância do SQL Server local para a nova versão do SQL Server 2017 no Windows e Linux. Enquanto o fluxo de trabalho de migração geral para Windows e Linux é a mesma, a mudança para o SQL Server 2017 para Linux requer algumas considerações adicionais.

### <a name="specifying-the-back-up-path"></a>Especificando o caminho de backup

Linux e Windows usam formatos de caminho diferentes. Como resultado, a migração para o SQL Server 2017 no Linux exige que o usuário fornecer versões de Windows e Linux do caminho para o local do arquivo físico. Você pode fornecer as duas versões do caminho de maneiras diferentes dependendo do local do arquivo físico.
Se o arquivo de backup físico estiver em um computador que executa:

* Linux, use 'samba' Compartilhar para compartilhar o arquivo com outros computadores na rede.
* Windows, use o comando '/mnt' para montar o compartilhamento no computador que executa o Linux.

> [!NOTE]
> Detalhes sobre como usar o comando '/mnt' ou um compartilhamento de 'samba' está além do escopo deste artigo.

### <a name="migrating-windows-logins"></a>Migrando logons do Windows

Enquanto a migração de logons do Active Directory (AD) é oficialmente suportada pelo SQL Server 2017 no Linux, ele requer configuração adicional para funcionar com êxito. Consulte o artigo [autenticação do Active Directory com o SQL Server no Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication) para obter informações detalhadas sobre como configurar logons do Active Directory no SQL Server 2017 no Linux. Depois de executar a configuração necessária, a instalação for concluída e você pode migrar logons do Active Directory como de costume. A autenticação SQL padrão funciona como esperado sem nenhuma configuração adicional.

## <a name="dma-v32"></a>A versão 3.2 DMA

A versão 3.2 de DMA inclui as seguintes adições:

* Migração de esquema e os dados são habilitados de bancos de dados do SQL Server local para o banco de dados SQL com um novo fluxo de trabalho de migração.
* Durante a migração de esquema para o banco de dados SQL, DMA scripts seus objetos de banco de dados de origem, fornece orientação sobre como corrigir quaisquer problemas potenciais de compatibilidade e, em seguida, implanta seu esquema para o Azure.

## <a name="dma-v31"></a>DMA v3.1

A versão v 3.1 de DMA inclui as seguintes adições:

* Recomendações de avaliação aprimorado para bancos de dados SQL do Azure em termos de agrupamentos de banco de dados, uso de procedimentos armazenados do sistema sem suporte e objetos CLR.
* Diretrizes de avaliação para níveis de compatibilidade 130, 120, 110 e 100 durante a migração de bancos de dados de SQL do Azure.

## <a name="dma-v30"></a>DMA v3.0

A versão v 3.0 de DMA estende a avaliação do banco de dados SQL do Azure para fornecer recomendações abrangentes para ajudar a corrigir problemas relacionados a:

* Problemas de bloqueio de migração.
* Parcialmente ou recursos e funções sem suporte.

## <a name="dma-v21"></a>DMA v2.1

A versão de v2.1 do DMA inclui as seguintes adições:

* Suporte de linha de comando para executar avaliações em um modo autônomo, o que ajuda a executar avaliações em grande escala. Para obter mais detalhes, consulte o artigo [executar Assistente de migração dados da linha de comando](dma-commandline.md).
* Melhorias de desempenho quando os usuários iniciem e feche o DMA.
* A capacidade de configurar o tempo limite de conexão do SQL. Para obter mais detalhes, consulte o artigo [definições de configuração para o Assistente de migração de dados](dma-configurationsettings.md).

## <a name="dma-v20"></a>DMA v2.0

A versão de v2.0 do DMA inclui recomendações de recurso de banco de dados Stretch aprimoradas para fornecer tabelas priorizadas adequadas que maximizar a economia de armazenamento.

## <a name="dma-v10"></a>DMA v1.0

O lançamento da versão 1.0 de DMA é a versão inicial, e ele fornece para:

* Descoberta de problemas que podem afetar uma atualização para uma versão local do SQL Server. Qualquer descobertas são descritas como problemas de compatibilidade e categorizados nas seguintes áreas:
  * Alterações significativas
  * Alterações de comportamento
  * Recursos preteridos
* Descoberta de novos recursos na plataforma do SQL Server de destino que pode se beneficiar do banco de dados após uma atualização. Qualquer descobertas são descritas como recomendações de recurso e categorizados nas seguintes áreas:
  * Desempenho
  * Segurança
  * Armazenamento
* Experiência do usuário moderna para executar avaliações.

## <a name="see-also"></a>Confira também

[Visão geral do Assistente de migração de dados](../dma/dma-overview.md)
