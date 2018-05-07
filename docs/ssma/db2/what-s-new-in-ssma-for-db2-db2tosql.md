---
title: Novidades do SSMA para DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-db2
ms.custom: ''
ms.date: 03/01/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b394ff1a8d97fcc91d81a122e620f3e1db1cf243
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>Novidades do SSMA para DB2 (DB2ToSQL)
Este tópico lista SSMA para DB2 alterações em cada versão.  

## <a name="ssma-v77"></a>O SSMA v7.7
A versão v7.7 do SSMA for DB2 contém as seguintes alterações:
- SSMA para DB2 foi aprimorado com correções de destino que melhoram a métrica de qualidade e a conversão.
- A versão de 32 bits do SSMA para DB2 com base na demanda popular, está de volta. Em comparação com a implementação anterior (antes da v 7.4), existem dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais adequada com base nos componentes de conectividade, que você tem. Sempre é preferível usar a versão de 64 bits, se possível.

> [!IMPORTANT]
> Com a v 7.4 do SSMA e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v76"></a>O SSMA v7.6
A versão v7.6 do SSMA para DB2 foi aprimorada com correções de destino que melhoram a qualidade e a conversão de métricas e com suporte para SQL Server 2017 (visualização pública). Suporte para SQL Server 2017 em Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

> [!IMPORTANT]
> Com v 7.4 do SSMA e versões posteriores, .net 4.5.2 é um pré-requisito de instalação e a versão de 32 bits da ferramenta foi descontinuada.

## <a name="ssma-v75"></a>V 7.5 do SSMA
A versão v 7.5 do SSMA para DB2 foi aprimorada com vários aprimoramentos para assegurar maior acessibilidade para pessoas com deficiências.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito de instalação v SSMA 7.5. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v74"></a>V 7.4 do SSMA
A versão v 7.4 do SSMA for DB2 contém as seguintes alterações:
- O **tempo limite da consulta** opção agora está disponível durante a descoberta de objeto de esquema na origem e no destino.
![opção de tempo limite de consulta](../media/query-timeout_red.png)

- A métrica de qualidade e a conversão foi aprimorada com correções de destino, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito de instalação v 7.4 do SSMA. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>O SSMA 7.3
A versão 7.3 do SSMA for DB2 contém as seguintes alterações:
- Métrica de qualidade e conversão aprimorada com correções de destino com base nos comentários dos clientes.
- Estrutura de extensibilidade do SSMA exposta por meio de itens a seguir:
  - Exporte funcionalidade a um projeto do SQL Server Data Tools (SSDT).
    -   Agora você pode exportar os scripts de esquema do SSMA para um projeto do SSDT. Você pode usar os scripts de esquema para fazer alterações de esquema adicionais e implantar seu banco de dados.
![Comando de projeto SSDT Salvar como](../media/export-schema-scripts_red.png)
  - Bibliotecas que podem ser consumidas por SSMA para realizar conversões personalizados.
    - Agora você pode construir o código que pode lidar com conversões de sintaxe personalizada e conversões que anteriormente não foram manipulados por SSMA.
      - Instruções sobre como construir um conversor personalizado estão disponíveis nesta postagem de blog, [recursos de conversão do estendendo o SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Projeto de exemplo para a conversão pode ser baixar este [postagem de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>V 7.2 do SSMA
A versão v 7.2 do SSMA for DB2 contém as seguintes alterações:
- Métrica de qualidade e conversão aprimorada com correções de destino com base nos comentários dos clientes.
- Aprimoramentos de telemetria para fornecer melhor pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>V 7.1 do SSMA
A versão v 7.1 do SSMA para Access contém as seguintes alterações:
- 2017 do SQL Server no Windows e Linux CTP1 agora é uma plataforma de destino com suporte para migração. Este recurso está na visualização técnica e permite a movimentação de dados e esquema para servidores de SQL de destino.
- O SSMA agora dá suporte a atualizações automáticas para baixar a versão mais recente do SSMA assim que ele está disponível.
- Binários instaláveis do SSMA agora são entregues por meio de arquivos de pacote do Windows installer (. msi).

**Recursos**

[Estendendo o recursos de conversão do SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Avaliar e migrar dados de plataformas de dados não Microsoft para SQL Server *(com exemplo de Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Maio de 2016  
A versão de maio de 2016 do SSMA for DB2 contém as seguintes alterações:  

-  Adicionado suporte para SQL Server 2016.
-  Conversão adicional de tabelas na memória e regulares do DB2 aos recursos de memória e hekaton do SQL Server.
-  Conversão adicional DB2 de controles de acesso a objetos de política do SQL Server (segurança em nível de linha para DB2).
-  Conversão de tabelas de versão de sistema do DB2 adicionado às tabelas temporais do SQL Server.
-  Analisador do DB2 e resolvedor aprimorado.
-  Removida a seleção de instalador para .net 2.0.
-  Removido dll desnecessários do instalador do Db2.
-  Fixa "salvar o projeto" e "Abrir projeto" comandos do Console SSMA.
-  Comando fixa "securepassword" para o Console do SSMA.
-  Correção de contagem de objetos para o carregamento inicial.
-  Correção do bug nas configurações globais.
  
## <a name="march-2016"></a>Março de 2016  
A versão de visualização de março de 2016 do SSMA for DB2 contém as seguintes alterações:  
  
-  Adicionado suporte para migração para o SQL Server 2016.  
  
## <a name="january-2016"></a>Janeiro de 2016  
A versão de manutenção de janeiro de 2016 do SSMA for DB2 contém as seguintes alterações:  
  
-  Adicionado suporte para um número de funções padrão.  
-  Corrigir erros de analisador do DB2.  
-  Fixa DB2 v9 zOS suporte (RFC 5690920).  
-  DB2 fixa não resolvidos erros de identificador durante a conversão.  
-  Item de Menu de Log de exibição adicionado para o SSMA (RFC 5706203).  
-  Telemetria adicionada.
  
## <a name="november-2014"></a>Novembro de 2014  
A versão de novembro de 2014 do SSMA for DB2 foi a versão inicial.
