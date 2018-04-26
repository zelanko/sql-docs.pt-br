---
title: O que há de novo no Assistente de migração de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2018
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0004406d86da4174898141d1f75c72186921b8d3
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="whats-new-in-data-migration-assistant"></a>O que há de novo no Assistente de migração de dados

Este tópico lista as adições em cada versão de dados Migration Assistant (DMA).

## <a name="dma-v34"></a>DMA v3.4
A versão de v3.4 do DMA inclui as seguintes adições:
- Suporte para SQL Server 2017 como uma fonte para migrações de banco de dados do SQL Azure.
- Aprimoramentos para correção de regra de avaliação, desempenho e estabilidade.

## <a name="dma-v33"></a>DMA v3.3
A versão de v3.3 do DMA permite a migração de uma instância do SQL Server local para a nova versão do SQL Server 2017, no Windows e Linux. Enquanto o fluxo geral de migração para o Windows e Linux é o mesmo, a mudança para o SQL Server 2017 para Linux requer algumas considerações adicionais.

### <a name="specifying-the-back-up-path"></a>Especificando o caminho de backup
Linux e Windows usam formatos de caminho diferentes. Como resultado, a migração para o SQL Server 2017 no Linux requer que o usuário fornecer versões do Windows e Linux do caminho para o local do arquivo físico. Isso é feito de diferentes maneiras, dependendo do local do arquivo físico.
Se o arquivo de backup físico estiver em um computador que está executando:
- Linux, use 'samba' share para compartilhar o arquivo com outros computadores na rede.
-   Windows, use o comando 'Manutenção' para montar o compartilhamento no computador executando o Linux.

> [!NOTE]
> Detalhes sobre como usar o comando 'Manutenção' ou um compartilhamento de 'samba' estão além do escopo deste artigo.

### <a name="migrating-windows-logins"></a>Migrando logons do Windows
Enquanto a migração de logons do Active Directory (AD) é oficialmente suportada por 2017 do SQL Server no Linux, ela requer configuração adicional para funcionar com êxito. Consulte o tópico [autenticação do Active Directory com o SQL Server no Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-active-directory-authentication) para obter informações detalhadas sobre como configurar logons do Active Directory no SQL Server 2017 no Linux. Depois de fazer isso a instalação for concluída, você pode migrar os logons do Active Directory como de costume. A autenticação SQL padrão funciona como esperado sem nenhuma configuração adicional.

## <a name="dma-v32"></a>A versão 3.2 DMA
A versão 3.2 de DMA inclui as seguintes adições:

- Migração de esquema e os dados são habilitados de bancos de dados local do SQL Server para o banco de dados do SQL Azure com um novo fluxo de trabalho de migração.

- Durante a migração de esquema para o banco de dados do SQL Azure, DMA scripts seus objetos de banco de dados de origem, fornece orientação sobre como corrigir problemas de compatibilidade potenciais e, em seguida, implanta o esquema para o Azure.

## <a name="dma-v31"></a>V DMA 3.1
A versão v 3.1 de DMA inclui as seguintes adições:

- Recomendações de avaliação aprimorado para bancos de dados do SQL Azure em termos de agrupamentos de banco de dados, o uso de procedimentos armazenados do sistema sem suporte e objetos CLR.

- Guia de avaliação para níveis de compatibilidade 130, 120, 110 e 100 durante a migração para bancos de dados do SQL Azure.

## <a name="dma-v30"></a>V DMA 3.0
A versão v 3.0 de DMA estende a avaliação de banco de dados SQL do Azure para fornecer recomendações abrangentes para ajudar a corrigir problemas relacionados a:

- Problemas de bloqueio de migração.

- Parcialmente ou não suporte a recursos e funções.

## <a name="dma-v21"></a>2.1 DMA
A versão 2.1 do DMA inclui as seguintes adições:
- Suporte de linha de comando para executar avaliações em um modo autônomo, o que ajuda a executar avaliações em escala. Para obter mais detalhes, consulte o tópico [executar dados Assistente de migração da linha de comando](dma-commandline.md).

- Melhorias de desempenho quando os usuários iniciem e feche DMA.

- A capacidade de configurar o tempo limite de conexão do SQL. Para obter mais detalhes, consulte o tópico [definições de configuração para o Assistente de migração de dados](dma-configurationsettings.md).

## <a name="dma-v20"></a>V 2.0 do DMA
A versão v 2.0 de DMA inclui recomendações do recurso de banco de Stretch aprimoradas para fornecer tabelas priorizadas adequadas que maximize a economia de armazenamento.

## <a name="dma-v10"></a>V 1.0 DMA
A versão v 1.0 de DMA é a versão inicial, e fornece para:
- Detecção de problemas que podem afetar uma atualização para uma versão local do SQL Server. Qualquer descobertas são descritas como problemas de compatibilidade, e eles são categorizados nas seguintes áreas:
    -   Alterações mais recentes
    - Alterações de comportamento
    - Recursos preteridos

- Descoberta de novos recursos na plataforma do SQL Server de destino que o banco de dados pode se beneficiar de uma atualização. Qualquer descobertas são descritas como recomendações do recurso, e eles são categorizados nas seguintes áreas:
    - Desempenho
    - Segurança
    - Armazenamento

-   Experiência de usuário moderna para executar avaliações.

## <a name="see-also"></a>Consulte também

[Visão geral do Assistente de migração de dados](../dma/dma-overview.md)
