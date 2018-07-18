---
title: O que há de novo no Assistente de migração de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/09/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 620590f03bf429dbc1633a1f78bb921def5fd585
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982148"
---
# <a name="whats-new-in-data-migration-assistant"></a>O que há de novo no Assistente de migração de dados
Este tópico lista as adições em cada versão de DMA Data Migration Assistant ().

## <a name="dma-v36"></a>V3.6 DMA
A versão de v3.6 do DMA apresenta "Correção automática" para os objetos de esquema que são afetados pelos bloqueadores de migração mais comuns.

Esta versão fornece correção automática para o Bloqueador de migração a seguir e problemas de mudança de comportamento:
- Os objetos de esquema que usam sintaxe Join não qualificado.
- Os objetos de esquema que usam a instrução RAISEERROR herdada.
- Instruções SQL que usam a ordem por Literal de inteiro.

O DMA executa a conversão automática de esquema para os objetos afetados pelos problemas listados e solicita confirmação antes de prosseguir com a conversão de esquema do usuário. Os usuários podem revisar as alterações de código sugerido e aceitar ou rejeitar todas as conversões de qualquer objeto de banco de dados fornecido.

DMA usa a tecnologia de síntese de programa da Microsoft (PROSA) para sugerir que correções de código. Saiba mais sobre [PROSA](https://microsoft.github.io/prose/).

## <a name="dma-v35"></a>V3.5 DMA
A versão v3.5 de DMA inclui as seguintes adições:
- Melhorias significativas de desempenho para a migração de banco de dados do SQL Azure (testes de benchmark indicam que o processo é quatro vezes mais rápido do que em versões anteriores de DMA).
- O volume de memória é ainda mais otimizado para melhorar a estabilidade do fluxo de trabalho de migração.
- A capacidade de ignorar avaliações durante as migrações de esquema e os dados (se você já realizou a avaliação e resolvidos quaisquer objetos de esquema de quebra antes da migração).
- Uma correção para resolver um problema com a ferramenta de travamento durante um caminho de compartilhamento de rede inválido é fornecido para arquivos de backup, ao realizar uma atualização de uma versão herdada do SQL Server local para uma versão posterior ou ao SQL Server em VMs do Azure.

## <a name="dma-v34"></a>V3.4 DMA
A versão de v3.4 de DMA inclui as seguintes adições:
- Suporte para SQL Server 2017 como uma fonte para as migrações para Azure SQL Database.
- Aprimoramentos de estabilidade, desempenho e avaliação de correção de regra.

## <a name="dma-v33"></a>V3.3 DMA
A versão v3.3 de DMA permite a migração de uma instância do SQL Server local para a nova versão do SQL Server 2017 no Windows e Linux. Enquanto o fluxo de trabalho de migração geral para Windows e Linux é a mesma, a mudança para o SQL Server 2017 para Linux requer algumas considerações adicionais.

### <a name="specifying-the-back-up-path"></a>Especificando o caminho de backup
Linux e Windows usam formatos de caminho diferentes. Como resultado, a migração para o SQL Server 2017 no Linux exige que o usuário fornecer versões de Windows e Linux do caminho para o local do arquivo físico. Você pode fornecer as duas versões do caminho de maneiras diferentes dependendo do local do arquivo físico.
Se o arquivo de backup físico estiver em um computador que executa:
- Linux, use 'samba' Compartilhar para compartilhar o arquivo com outros computadores na rede.
- Windows, use o comando '/mnt' para montar o compartilhamento no computador que executa o Linux.

> [!NOTE]
> Detalhes sobre como usar o comando '/mnt' ou um compartilhamento de 'samba' está além do escopo deste artigo.

### <a name="migrating-windows-logins"></a>Migrando logons do Windows
Enquanto a migração de logons do Active Directory (AD) é oficialmente suportada pelo SQL Server 2017 no Linux, ele requer configuração adicional para funcionar com êxito. Consulte o tópico [autenticação do Active Directory com o SQL Server no Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication) para obter informações detalhadas sobre como configurar logons do Active Directory no SQL Server 2017 no Linux. Depois de executar a configuração necessária, a instalação for concluída e você pode migrar logons do Active Directory como de costume. A autenticação SQL padrão funciona como esperado sem nenhuma configuração adicional.

## <a name="dma-v32"></a>A versão 3.2 DMA
A versão 3.2 de DMA inclui as seguintes adições:

- Migração de esquema e os dados são habilitados de bancos de dados do SQL Server local para o banco de dados SQL com um novo fluxo de trabalho de migração.
- Durante a migração de esquema para o banco de dados SQL, DMA scripts seus objetos de banco de dados de origem, fornece orientação sobre como corrigir quaisquer problemas potenciais de compatibilidade e, em seguida, implanta seu esquema para o Azure.

## <a name="dma-v31"></a>DMA v3.1
A versão v 3.1 de DMA inclui as seguintes adições:

- Recomendações de avaliação aprimorado para bancos de dados SQL do Azure em termos de agrupamentos de banco de dados, uso de procedimentos armazenados do sistema sem suporte e objetos CLR.
- Diretrizes de avaliação para níveis de compatibilidade 130, 120, 110 e 100 durante a migração de bancos de dados de SQL do Azure.

## <a name="dma-v30"></a>V 3.0 DMA
A versão v 3.0 de DMA estende a avaliação do banco de dados SQL do Azure para fornecer recomendações abrangentes para ajudar a corrigir problemas relacionados a:

- Problemas de bloqueio de migração.
- Parcialmente ou recursos e funções sem suporte.

## <a name="dma-v21"></a>O DMA v2.1
A versão de v2.1 do DMA inclui as seguintes adições:
- Suporte de linha de comando para executar avaliações em um modo autônomo, o que ajuda a executar avaliações em grande escala. Para obter mais detalhes, consulte o tópico [executar Assistente de migração dados da linha de comando](dma-commandline.md).
- Melhorias de desempenho quando os usuários iniciem e feche o DMA.
- A capacidade de configurar o tempo limite de conexão do SQL. Para obter mais detalhes, consulte o tópico [definições de configuração para o Assistente de migração de dados](dma-configurationsettings.md).

## <a name="dma-v20"></a>V 2.0 DMA
A versão de v2.0 do DMA inclui recomendações de recurso de banco de dados Stretch aprimoradas para fornecer tabelas priorizadas adequadas que maximizar a economia de armazenamento.

## <a name="dma-v10"></a>O DMA v1.0
O lançamento da versão 1.0 de DMA é a versão inicial, e ele fornece para:
- Descoberta de problemas que podem afetar uma atualização para uma versão local do SQL Server. Qualquer descobertas são descritas como problemas de compatibilidade, e eles são categorizados nas seguintes áreas:
    - Alterações significativas
    - Alterações de comportamento
    - Recursos preteridos
- Descoberta de novos recursos na plataforma do SQL Server de destino que o banco de dados pode se beneficiar de uma atualização. Qualquer descobertas são descritas como recomendações de recurso, e eles são categorizados nas seguintes áreas:
    - Desempenho
    - Segurança
    - Armazenamento
-   Experiência do usuário moderna para executar avaliações.

## <a name="see-also"></a>Confira também
[Visão geral do Assistente de migração de dados](../dma/dma-overview.md)
