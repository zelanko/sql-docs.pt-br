---
title: Quais são as novidades do SSMA para MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 06/11/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
author: HJToland3
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 5f3ea9905f0a44e7863154b93283ea8ef2f49f7b
ms.sourcegitcommit: 40e55e55a73e39d447da87d9178f2b6067f39c6f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2019
ms.locfileid: "66841068"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>Novidades no SSMA para MySQL (MySQLToSql)

Este artigo lista os SQL Server Migration Assistant (SSMA) do MySQL alterações em cada versão.

## <a name="ssma-v82"></a>SSMA v8.2

A versão 8.1 do SSMA para MySQL é aprimorada com um conjunto direcionado de correções projetadas para melhorar a qualidade e métricas de conversão, bem como correções para:

* Um problema com os índices não clusterizados desabilitados após a migração de dados.
* Detecção do .NET Framework durante a instalação silenciosa.
* Uma falha de intermitente que ocorre quando uma nova versão é baixada.

> [!NOTE]
> Um problema conhecido com a atualização automática pode fazer com que a falha de uma atualização do SSMA v8.1 v 8.2. Se você encontrar esse erro, baixe a nova versão e instalá-lo manualmente.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v81"></a>SSMA v8.1

A versão 8.1 do SSMA para MySQL é aprimorada com correções direcionadas são projetadas para melhorar as métricas de qualidade e a conversão.

> [!NOTE]
> Um problema conhecido com a atualização automática pode fazer com que a falha de uma atualização do SSMA v8.0 8.1. Se você encontrar esse erro, baixe a nova versão e instalá-lo manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

A versão v 8.0 do SSMA para MySQL é aprimorada com correções direcionadas projetadas para melhorar a qualidade e a conversão de métricas. Esta versão também oferece os seguintes recursos novos:

* Suporte para **banco de dados de instância gerenciada do SQL** como um destino. Agora você pode criar novos projetos direcionados ao banco de dados de instância gerenciada do SQL:

  ![Projeto de banco de dados SQL para a MI](../media/ssma-newproject-sqldbmi.png)

* Após a conversão **correção advisor**. Saiba mais sobre ele [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Seleção de banco de dados ou o esquema preliminar.

  Ao se conectar à fonte, o usuário pode agora selecionar bancos de dados/esquemas de interesse. Selecionando apenas os esquemas que você planeja migrar economizar tempo durante a conexão inicial e melhorar o desempenho geral do SSMA.

  ![Objetos de filtro do SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

A versão de v7.10 do SSMA para MySQL contém as seguintes alterações:

* Correções direcionadas projetadas para fornecer segurança adicional e proteções de privacidade para atender às mudanças nos requisitos de globais.
* Uma correção para a conversão de espaços entre a lista de argumentos e o nome da função.

## <a name="ssma-v79"></a>SSMA v7.9

A versão de v7.9 do SSMA para MySQL contém as seguintes alterações:

* Correções de destino que melhoram as métricas de qualidade e a conversão.
* Suporte parcial para tipos de dados espaciais Migrando do MySQL para o banco de dados SQL.
* Suporte a linha de comando do SSMA para alterar o mapeamento de tipo de dados e preferências de projeto.
* Suporte para a migração de dados usando o SQL Server Integration Services (SSIS). Depois de converter o esquema, é possível criar um pacote do SSIS por meio de uma opção de menu de contexto do botão direito do mouse.
* A caixa de diálogo de conexão de banco de dados SQL do SSMA também foi alterada para especificar o nome totalmente qualificado do servidor. Em versões anteriores do SSMA, o prefixo de banco de dados SQL precisava ser mencionado explicitamente dentro de configurações de projetos.

## <a name="ssma-v78"></a>SSMA v7.8

A versão de v 7.8 do SSMA para MySQL contém as seguintes alterações:

* Alterar o mapeamento de tipo realçado nas configurações do projeto.
* A capacidade dos usuários desabilitar a telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

A versão de v7.7 do SSMA para MySQL contém as seguintes alterações:

* SSMA para MySQL foi aprimorado com correções direcionadas que melhoram as métricas de qualidade e a conversão.
* A versão de 32 bits do SSMA para MySQL com base na demanda popular, está de volta. Em comparação com a implementação anterior (antes da v 7.4), há dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base em componentes de conectividade, que você tem. É sempre preferível usar a versão de 64 bits, se possível.
* Agora, o SSMA para MySQL tem modo de conexão da cadeia de caracteres de Conexão ODBC, que permite que você use os drivers ODBC de terceiros que são compatíveis com o MySQL.

## <a name="ssma-v76"></a>SSMA v7.6

A versão de v7.6 do SSMA para MySQL foi aprimorada com correções direcionadas que melhoram as métricas de qualidade e a conversão e com suporte para SQL Server 2017 (visualização pública). Suporte para SQL Server 2017 no Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

## <a name="ssma-v75"></a>SSMA v7.5

A versão de v 7.5 do SSMA para MySQL foi aprimorada com vários aprimoramentos para garantir que a maior acessibilidade para pessoas com deficiências.

## <a name="ssma-v74"></a>SSMA v7.4

A versão de v 7.4 do SSMA para MySQL contém as seguintes alterações:

* O **tempo limite da consulta** opção agora está disponível durante a descoberta de objeto de esquema na origem e destino.

    ![opção de tempo limite de consulta](../media/query-timeout_red.png)
* A métrica de qualidade e a conversão foi aprimorada com correções direcionadas, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito para a instalação v SSMA 7.4. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>SSMA v7.3

A versão 7.3 do SSMA para MySQL contém as seguintes alterações:

* Métrica de qualidade e a conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
* Estrutura de extensibilidade do SSMA exposta por meio dos seguintes itens:
  * Exporte a funcionalidade para um projeto do SQL Server Data Tools (SSDT).
    * Agora você pode exportar os scripts de esquema do SSMA para um projeto do SSDT. Você pode usar os scripts de esquema para fazer alterações de esquema adicional e implantar seu banco de dados.

      ![Salvar como um comando de projeto do SSDT](../media/export-schema-scripts_red.png)
  * Bibliotecas que podem ser consumidas por SSMA para realizar conversões personalizadas.
    * Agora você pode construir o código que pode lidar com conversões de sintaxe personalizada e conversões que anteriormente não eram tratadas pelo SSMA.
      * As instruções sobre como construir um conversor personalizado estão disponíveis nesta postagem de blog [recursos de conversão do estendendo o SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Baixe um projeto de exemplo para a conversão deste [postagem de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2

A versão de v7.2 do SSMA para MySQL contém as seguintes alterações:

* Métrica de qualidade e a conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
* Aprimoramentos de telemetria para fornecer melhor pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

A versão de v7.1 do SSMA para MySQL contém as seguintes alterações:

* Agora, o SQL Server 2017 no Windows e Linux CTP1 é uma plataforma de destino com suporte para a migração. Esse recurso está na visualização técnica e permite a movimentação de dados e esquema para servidores de SQL de destino.
* Agora, o SSMA dá suporte a atualizações automáticas para baixar a versão mais recente do SSMA assim que ele está disponível.
* Agora, os binários instaláveis do SSMA são entregues por meio de arquivos de pacote do Windows installer (. msi).

## <a name="may-2016"></a>Maio de 2016  
A versão de maio de 2016 do SSMA para MySQL contém as seguintes alterações:

* Adicionado suporte para SQL Server 2016.
* Analisador aprimorado e o resolvedor.
* Removida a verificação de instalador para .net 2.0.
* Dependência do pacote de extensão atualizada do .net 3.5 para o .net 4.0.
* Mapeamento de tipo padrão fixo BigInt para MySql.
* Corrigido "salvar o projeto" e "Abrir projeto" comandos para o Console do SSMA.
* Corrigido o comando "securepassword" para o Console do SSMA.
* Correção de contagem de objetos para o carregamento inicial.
* Carregando os objetos MsSql fixos.
* Corrigido o bug nas configurações globais.

## <a name="march-2016"></a>Março de 2016

A versão de preview de março de 2016 do SSMA para MySQL adiciona suporte para a migração para o SQL Server 2016. 
  
## <a name="january-2016"></a>Janeiro de 2016

A versão de manutenção de janeiro de 2016 do SSMA para MySQL contém as seguintes alterações:  

* Item de Menu exibição adicionado Log para o SSMA (RFC 5706203).  
* Adicionada a telemetria.  
  
## <a name="july-2014"></a>Julho de 2014

A versão de julho de 2014 do SSMA para MySQL contém as seguintes alterações:  
  
* Melhor conversão de código de BD SQL do Azure. 
* Funcionalidade do pacote de extensão é movido para o esquema para dar suporte ao BD SQL do Azure.  
* Melhorias de desempenho é testado para bancos de dados com mais de 10 mil objetos.  
* Aprimoramentos da interface do usuário para lidar com um grande número de objetos.  
* O realce de "bem conhecidas" esquemas LOB (de modo que eles podem ser ignorados na conversão).  
* Melhorias de velocidade de conversão.  
* Mostram contagens de objetos na interface do usuário.  
* Redução de tamanho de relatório por mais de 25%.  
* Mensagens de erro aprimoradas para construções não analisadas.  
  
## <a name="april-2014"></a>Abril de 2014

A versão de abril de 2014 do SSMA para MySQL contém as seguintes alterações:  
  
* Adicionado suporte do MS SQL Server 2014.  
* Bugs corrigidos em relação à conversão para o Azure  
* Bugs corrigidos em relação à páginas de relatório invisível no IE 10.  
  
## <a name="july-2011"></a>Julho de 2011

A versão de julho de 2011 do SSMA para MySQL contém as seguintes alterações:  
  
* Suporte para conversão de limite para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deslocamento "Denali".  
* Aprimorado relatórios de erros durante a migração de dados.  
  
## <a name="april-2011"></a>Abril de 2011

A versão de abril de 2011 do SSMA para MySQL contém as seguintes alterações:  
  
* Único pode ser instalado do "SSMA para MySQL", que dá suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" e o SQL Azure.  
* A capacidade de conectar-se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
* Mecanismo de migração aprimorada de dados do cliente, que dão suporte a migração paralela de dados.  
* Desempenho de migração de dados aprimorada com simples e Bulk logged modelos de recuperação.  
* O SSMA para MySQL Console versão dá suporte à compatibilidade com versões anteriores. Você pode abrir os projetos criados por versões anterior para o SSMA v5.0.  
* SSMA para MySQL v5.0 produto pode ser instalado lado a lado (SxS) com as versões mais antigas do produto do SSMA.  
  
## <a name="july-2010"></a>Julho de 2010

A versão de julho de 2010 do SSMA para MySQL contém os seguintes recursos:  
  
1. **Aperfeiçoamentos na Interface do usuário:**  
  
    * Guia de 'modo SQL' para objetos de banco de dados MySQL  
    * Guia 'Configurações' para objetos de banco de dados MySQL  
    * Guia de 'Dados' para tabelas com MySQL  
    * Configurações de projeto atualizado nas páginas de migração e de conversão  
    * 'Configurações de migração de dados' no nível de tabela  
  
2. **Melhorias para se conectar ao SQL Server e MySQL:**  
  
    * Conectividade SSL no MySQL  
    * Conectividade criptografada no SQL Server  
  
3. **Aprimoramentos para o Gerenciador de Metabase do MySQL:**  
  
    * Carregar todos os objetos de banco de dados MySQL e seus respectivos guias.  
  
4. **Aprimoramentos para a conversão de objeto:**
  
    * Conversão de objetos de Metabase do MySQL - procedimentos, funções, exibições, gatilhos e instruções.  
    * Suporte limitado para tipos de dados espaciais em tabelas.
    * Opção de converter funções de MySQL para procedimentos armazenados do SQL Server  
    * Opção de aplicar o mapeamento de modos SQL e o conjunto de caracteres durante a conversão do objeto  
  
5. **Aprimoramentos para a migração de dados:**  
  
    * Suporte para migração de dados usando mecanismos de migração de dados do lado do cliente e do servidor  
    * Suporte para a migração de dados espaciais  
    * SQL personalizado para a migração de dados para tabelas  
  
6. **SSMA para MySQL Console:**  
  
    * Dar suporte ao recurso de Console de SSMA para MySQL  
    * Suporte para interface de nível de Script  
  
## <a name="january-2010"></a>Janeiro de 2010

A versão de janeiro de 2010 do SSMA para MySQL é a versão inicial. Continha os seguintes recursos: 
  
* Adicionado suporte para a migração para os dois locais do SQL Server e SQL do Azure.  
  
* **Recurso de instantâneo:** Migração de esquema e dados do MySQL tabelas/índices/restrições.
