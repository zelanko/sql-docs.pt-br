---
title: Quais são as novidades do SSMA para DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8b72d53f001654a085b8d2b5d01e203fd1b29ebe
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52400319"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>Quais são as novidades do SSMA para DB2 (DB2ToSQL)
Este artigo lista SSMA para DB2 alterações em cada versão.  

## <a name="ssma-v710"></a>O SSMA v7.10
A versão de v7.10 do SSMA para DB2 contém as seguintes alterações:
- Correções direcionadas projetadas para fornecer segurança adicional e proteções de privacidade para atender às mudanças nos requisitos de globais.
- Uma correção para a conversão de blocos BEGIN-END.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v79"></a>O SSMA v7.9
A versão de v7.9 do SSMA para DB2 contém as seguintes alterações:
- Correções de destino que melhoram as métricas de qualidade e a conversão.
- Suporte a linha de comando do SSMA para alterar o mapeamento de tipo de dados e preferências de projeto.
- Suporte para a migração de dados usando o SQL Server Integration Services (SSIS). Depois de converter o esquema, é possível criar um pacote do SSIS por meio de uma opção de menu de contexto do botão direito do mouse.
- A caixa de diálogo de conexão de banco de dados SQL do SSMA também foi alterada para especificar o nome totalmente qualificado do servidor. Em versões anteriores do SSMA, o prefixo de banco de dados SQL precisava ser mencionado explicitamente dentro de configurações de projetos.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v78"></a>V 7.8 do SSMA
A versão de v 7.8 do SSMA para DB2 contém as seguintes alterações:
- Mapeamento de tipo de alteração realçada nas configurações do projeto.
- Fornecida a capacidade dos usuários desabilitar a telemetria.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v77"></a>O SSMA v7.7
A versão de v7.7 do SSMA para DB2 contém as seguintes alterações:
- SSMA para DB2 foi aprimorado com correções direcionadas que melhoram as métricas de qualidade e a conversão.
- A versão de 32 bits do SSMA para DB2 com base na demanda popular, está de volta. Em comparação com a implementação anterior (antes da v 7.4), há dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base em componentes de conectividade, que você tem. É sempre preferível usar a versão de 64 bits, se possível.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v76"></a>O SSMA v7.6
A versão de v7.6 do SSMA para DB2 foi aprimorada com correções direcionadas que melhoram as métricas de qualidade e a conversão e com suporte para SQL Server 2017 (visualização pública). Suporte para SQL Server 2017 no Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação e a versão de 32 bits da ferramenta foi descontinuada.

## <a name="ssma-v75"></a>O SSMA v7.5
A versão de v 7.5 do SSMA para DB2 foi aprimorada com vários aprimoramentos para garantir que a maior acessibilidade para pessoas com deficiências.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito para instalar o SSMA v7.5. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v74"></a>V 7.4 do SSMA
A versão de v 7.4 do SSMA para DB2 contém as seguintes alterações:
- O **tempo limite da consulta** opção agora está disponível durante a descoberta de objeto de esquema na origem e destino.
![opção de tempo limite de consulta](../media/query-timeout_red.png)

- A métrica de qualidade e a conversão foi aprimorada com correções direcionadas, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito para a instalação v SSMA 7.4. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>O SSMA 7.3
A versão 7.3 do SSMA para DB2 contém as seguintes alterações:
- Métrica de qualidade e a conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
- Estrutura de extensibilidade do SSMA exposta por meio dos seguintes itens:
  - Exporte a funcionalidade para um projeto do SQL Server Data Tools (SSDT).
    -   Agora você pode exportar os scripts de esquema do SSMA para um projeto do SSDT. Você pode usar os scripts de esquema para fazer alterações de esquema adicional e implantar seu banco de dados.
![Salvar como um comando de projeto do SSDT](../media/export-schema-scripts_red.png)
  - Bibliotecas que podem ser consumidas por SSMA para realizar conversões personalizadas.
    - Agora você pode construir o código que pode lidar com conversões de sintaxe personalizada e conversões que anteriormente não eram tratadas pelo SSMA.
      - As instruções sobre como construir um conversor personalizado estão disponíveis nesta postagem de blog [recursos de conversão do estendendo o SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Baixe um projeto de exemplo para a conversão deste [postagem de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>O SSMA v7.2
A versão de v7.2 do SSMA para DB2 contém as seguintes alterações:
- Métrica de qualidade e a conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
- Aprimoramentos de telemetria para fornecer melhor pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>O SSMA v7.1
A versão de v7.1 do SSMA para Access contém as seguintes alterações:
- Agora, o SQL Server 2017 no Windows e Linux CTP1 é uma plataforma de destino com suporte para a migração. Esse recurso está na visualização técnica e permite a movimentação de dados e esquema para servidores de SQL de destino.
- Agora, o SSMA dá suporte a atualizações automáticas para baixar a versão mais recente do SSMA assim que ele está disponível.
- Agora, os binários instaláveis do SSMA são entregues por meio de arquivos de pacote do Windows installer (. msi).

**Recursos**

[Estendendo os recursos da SQL Server Migration Assistant conversão](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Avaliar e migrar dados de plataformas de dados não Microsoft para SQL Server *(com o exemplo do Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Maio de 2016  
A versão de maio de 2016 do SSMA para DB2 contém as seguintes alterações:  

-  Adicionado suporte para SQL Server 2016.
-  Conversão das tabelas na memória e regulares do DB2 adicionado aos recursos na memória e hekaton do SQL Server.
-  Conversão adicionado DB2 de controles de acesso a objetos de política do SQL Server (segurança em nível de linha para DB2).
-  Conversão das tabelas de versão do sistema do DB2 adicionado às tabelas temporais do SQL Server.
-  Aprimorado o analisador de DB2 e o resolvedor.
-  Removida a verificação de instalador para .net 2.0.
-  Removido desnecessárias *. dll do instalador do Db2.
-  Corrigido "salvar o projeto" e "Abrir projeto" comandos para o Console do SSMA.
-  Corrigido o comando "securepassword" para o Console do SSMA.
-  Correção de contagem de objetos para o carregamento inicial.
-  Corrigido o bug nas configurações globais.
  
## <a name="march-2016"></a>Março de 2016  
A versão de preview de março de 2016 do SSMA para DB2 contém as seguintes alterações:  
  
-  Adicionado suporte para migração para o SQL Server 2016.  
  
## <a name="january-2016"></a>Janeiro de 2016  
A versão de manutenção de janeiro de 2016 do SSMA para DB2 contém as seguintes alterações:  
  
-  Adicionado suporte para um número de funções padrão.  
-  Correção de erros do analisador de DB2.  
-  Fixo DB2 v9 zOS suporte (RFC 5690920).  
-  DB2 fixa não resolvidos erros identificador durante a conversão.  
-  Item de Menu exibição adicionado Log para o SSMA (RFC 5706203).  
-  Adicionada a telemetria.
  
## <a name="november-2014"></a>Novembro de 2014  
A versão de novembro de 2014 do SSMA para DB2 é a versão inicial.
