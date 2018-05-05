---
title: Novidades do SSMA para MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
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
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
caps.latest.revision: 21
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 10f3818ac0c4f813e12ad21466caf56221502a26
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>Novidades do SSMA para MySQL (MySQLToSql)
Este tópico lista SSMA para MySQL alterações em cada versão. 

## <a name="ssma-v77"></a>O SSMA v7.7
A versão v7.7 do SSMA para MySQL contém as seguintes alterações:
- SSMA para MySQL foi aprimorado com correções de destino que melhoram a métrica de qualidade e a conversão.
- A versão de 32 bits do SSMA para MySQL com base na demanda popular, está de volta. Em comparação com a implementação anterior (antes da v 7.4), existem dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais adequada com base nos componentes de conectividade, que você tem. Sempre é preferível usar a versão de 64 bits, se possível.
- SSMA para MySQL agora tem o modo de conexão da cadeia de caracteres de Conexão ODBC, que permite que você use os drivers ODBC de terceiros que é compatível com o MySQL.

> [!IMPORTANT]
> Com a v 7.4 do SSMA e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v76"></a>O SSMA v7.6
A versão v7.6 do SSMA para MySQL foi aprimorada com correções de destino que melhoram a qualidade e a conversão de métricas e com suporte para SQL Server 2017 (visualização pública). Suporte para SQL Server 2017 em Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

> [!IMPORTANT]
> Com v 7.4 do SSMA e versões posteriores, .net 4.5.2 é um pré-requisito de instalação e a versão de 32 bits da ferramenta foi descontinuada.

## <a name="ssma-v75"></a>V 7.5 do SSMA
A versão v 7.5 do SSMA para MySQL foi aprimorada com vários aprimoramentos para assegurar maior acessibilidade para pessoas com deficiências.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito de instalação v SSMA 7.5. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v74"></a>V 7.4 do SSMA
A versão v 7.4 do SSMA para MySQL contém as seguintes alterações:
- O **tempo limite da consulta** opção agora está disponível durante a descoberta de objeto de esquema na origem e no destino.
![opção de tempo limite de consulta](../media/query-timeout_red.png)
- A métrica de qualidade e a conversão foi aprimorada com correções de destino, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito de instalação v 7.4 do SSMA. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada. 

## <a name="ssma-v73"></a>O SSMA 7.3
A versão 7.3 do SSMA para MySQL contém as seguintes alterações:
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
A versão v 7.2 do SSMA para MySQL contém as seguintes alterações:
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
A versão de maio de 2016 do SSMA para MySQL contém as seguintes alterações:.

-  Adicionado suporte para SQL Server 2016.
-  Analisador aprimorado e o resolvedor.
-  Removida a seleção de instalador para .net 2.0.
-  Dependência do pacote de extensão atualizada do .net 3.5 para o .net 4.0.
-  Typemapping de BigInt fixa padrão para MySql.
-  Fixa "salvar o projeto" e "Abrir projeto" comandos do Console SSMA.
-  Comando fixa "securepassword" para o Console do SSMA.
-  Correção de contagem de objetos para o carregamento inicial.
-  Carregando os objetos MsSql fixos.
-  Correção do bug nas configurações globais.
 
## <a name="march-2016"></a>Março de 2016  
A versão de visualização de março de 2016 do SSMA para MySQL contém as seguintes alterações:  
  
-  Adicionado suporte para migração para o SQL Server 2016. 
  
## <a name="january-2016"></a>Janeiro de 2016  
A versão de manutenção de janeiro de 2016 do SSMA para MySQL contém as seguintes alterações:  
  
-  Item de Menu de Log de exibição adicionado para o SSMA (RFC 5706203).  
-  Telemetria adicionada.  
  
## <a name="july-2014"></a>Julho de 2014  
A versão de julho de 2014 do SSMA para MySQL contém as seguintes alterações:  
  
-  Conversão de código de banco de dados do Azure SQL aprimorado. 
-  Funcionalidade do pacote de extensão é movido para o esquema para oferecer suporte a banco de dados de SQL do Azure.  
-  Melhorias de desempenho testado para bancos de dados com mais de 10 mil objetos.  
-  Aprimoramentos da interface do usuário para lidar com um grande número de objetos.  
-  Realce de esquemas LOB "bem conhecidas" (para que eles podem ser ignorados na conversão).  
-  Melhorias de velocidade de conversão.  
-  Mostre contagens de objetos na interface do usuário.  
-  Redução de tamanho de relatório por mais de 25%.  
-  Mensagens de erro aprimoradas para construções não analisadas.  
  
## <a name="april-2014"></a>Abril de 2014  
A versão de julho de 2011 do SSMA para MySQL contém as seguintes alterações:  
  
-  Adicionado suporte do MS SQL Server 2014.  
-  Bugs corrigidos sobre conversão para o Azure  
-  Bugs corrigidos sobre páginas de relatório invisível no Internet Explorer 10.  
  
## <a name="july-2011"></a>Julho de 2011  
A versão de julho de 2011 do SSMA para MySQL contém as seguintes alterações:  
  
-   Suporte para conversão de limite para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] deslocamento "Denali".  
-   Melhor relatórios de erros durante a migração de dados.  
  
## <a name="april-2011"></a>Abril de 2011  
A versão de abril de 2011 do SSMA para MySQL contém as seguintes alterações:  
  
-   Instalável do "SSMA para MySQL", que oferece suporte a um único [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" e SQL Azure.  
-   A capacidade de conectar-se [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
-   Mecanismo de migração aprimorada de dados do lado do cliente, dando suporte a migração paralela de dados.  
-   Desempenho de migração de dados aprimorada com simples e Bulk logged modelos de recuperação.  
-   SSMA para a versão do Console do MySQL dá suporte à compatibilidade com versões anteriores. Você pode abrir os projetos criados por versões anteriores para v 5.0 do SSMA.  
-   SSMA para MySQL v 5.0 produto pode ser instalado lado a lado (SxS) com versões anteriores do produto do SSMA.  
  
## <a name="july-2010"></a>Julho de 2010  
A versão de julho de 2010 do SSMA para MySQL contém os seguintes recursos:  
  
1.  **Aprimoramentos à Interface do usuário:**  
  
    -   Guia de 'modo SQL' para objetos de banco de dados MySQL  
    -   Guia "Configurações" para objetos de banco de dados MySQL  
    -   Guia de 'Dados' para tabelas de MySQL  
    -   Configurações de projeto atualizado na conversão e páginas de migração  
    -   'Configurações de migração de dados' no nível de tabela  
  
2.  **Aprimoramentos para se conectar ao SQL Server e MySQL:**  
  
    -   Conectividade SSL no MySQL  
    -   Conectividade criptografada no SQL Server  
  
3.  **Aprimoramentos ao Gerenciador de Metabase MySQL:**  
  
    -   Carregar todos os objetos de banco de dados MySQL e seus respectivos guias.  
  
4.  **Aprimoramentos para conversão do objeto:**  
  
    -   Conversão de objetos de Metabase do MySQL – procedimentos, funções, exibições, gatilhos e instruções.  
    -   Suporte limitado para tipos de dados espaciais em tabelas.  
    -   Opção de converter as funções do MySQL para procedimentos armazenados do SQL Server  
    -   Opção de aplicar o mapeamento de modos SQL e o conjunto de caracteres durante a conversão do objeto  
  
5.  **Aprimoramentos para migração de dados:**  
  
    -   Suporte para migração de dados usando os mecanismos de migração de dados do lado do cliente e do servidor  
    -   Suporte para a migração de dados espaciais  
    -   SQL personalizado para a migração de dados para tabelas  
  
6.  **SSMA para MySQL Console:**  
  
    -   Suporte a recurso de Console para o SSMA para MySQL  
    -   Suporte para interface de nível de Script  
  
## <a name="january-2010"></a>Janeiro de 2010  
A versão de janeiro de 2010 do SSMA para MySQL foi a versão inicial. Ele continha os seguintes recursos:  
  
-   Adicionado suporte para migração para os dois locais do SQL Server e SQL Azure.  
  
-   **Recurso de instantâneo:** migração de esquema e dados do MySQL tabelas/índices/restrições.
