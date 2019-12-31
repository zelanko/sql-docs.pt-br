---
title: O que há de novo no SSMA para MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 12/04/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: ccb8c325a2e0b2966c0355be0f9cd84bd8882d24
ms.sourcegitcommit: 26868c8ac3217176b370d972a26d307598a10328
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "74834308"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>Novidades no SSMA para MySQL (MySQLToSql)

Este artigo lista Assistente de Migração do SQL Server (SSMA) para MySQL alterações em cada versão.

## <a name="ssma-v85"></a>SSMA v 8.5

A versão v 8.5 do SSMA para MySQL foi aprimorada com suporte para autenticação de Azure Active Directory e suporte básico para recursos JSON no SQL Server, junto com um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho.

> [!IMPORTANT]
> Com o SSMA v 8.5, o .NET 4.7.2 é um pré-requisito de instalação. Se precisar instalar essa versão, você poderá baixar o arquivo de tempo de execução [aqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v 8.4

A versão v 8.4 do SSMA para MySQL foi aprimorada com correções direcionadas que foram projetadas para resolver problemas de acessibilidade e corrigir um bug relacionado a colunas de índice máximo (para permitir 32 em vez de 16) para SQL Server 2016 e versões posteriores.

> [!IMPORTANT]
> Com o SSMA versões 7,4, embora 8,4, o .NET 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v83"></a>SSMA v 8.3

A versão v 8.3 do SSMA para MySQL foi aprimorada com correções direcionadas que foram projetadas para melhorar a qualidade e a conversão de métricas. Além disso, esta versão do SSMA para MySQL fornece correções que:

* Solucionar problemas de acessibilidade
* Adicionar suporte básico para o tipo ' hierarchyid ' no SQL Server

## <a name="ssma-v82"></a>SSMA v 8.2

A versão v 8.2 do SSMA para MySQL foi aprimorada com um conjunto direcionado de correções projetadas para melhorar a qualidade e as métricas de conversão, bem como correções para:

* Um problema com índices não clusterizados desabilitados após a migração de dados.
* Detecção de .NET Framework durante a instalação silenciosa.
* Uma falha intermitente que ocorre quando uma nova versão é baixada.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v 8.1 para v 8.2. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v81"></a>SSMA v 8.1

A versão v 8.1 do SSMA para MySQL foi aprimorada com correções direcionadas que foram projetadas para melhorar a qualidade e a conversão de métricas.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v 8.0 para o v 8.1. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v80"></a>SSMA v 8.0

A versão v 8.0 do SSMA para MySQL foi aprimorada com correções direcionadas projetadas para melhorar a qualidade e a conversão de métricas. Esta versão também oferece os seguintes novos recursos:

* Suporte para **instância gerenciada do banco de dados SQL do Azure** como um destino. Agora você pode criar novos projetos destinados a Instância Gerenciada do Banco de Dados SQL do Azure:

  ![Projeto MI do BD SQL](../media/ssma-newproject-sqldbmi.png)

* **Supervisor de correção**após a conversão. Saiba mais sobre isso [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Seleção preliminar de banco de dados/esquema.

  Ao se conectar à fonte, o usuário agora pode selecionar bancos de dados/esquemas de interesse. Selecionar somente os esquemas que você planeja migrar economizará tempo durante a conexão inicial e melhorará o desempenho geral do SSMA.

  ![Objetos de filtro do SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>7.10 do SSMA v

A versão v 7.10 do SSMA para MySQL contém as seguintes alterações:

* Correções direcionadas projetadas para fornecer segurança adicional e proteções de privacidade para atender às alterações nos requisitos globais.
* Uma correção para a conversão de espaços entre o nome da função e a lista de argumentos.

## <a name="ssma-v79"></a>7.9 do SSMA v

A versão v 7.9 do SSMA para MySQL contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Suporte parcial para a migração de tipos de dados espaciais do MySQL para o Azure SQL Database.
* Suporte na linha de comando do SSMA para alterar o mapeamento de tipo de dados e as preferências do projeto.
* Suporte para migrar dados usando SQL Server Integration Services (SSIS). Depois de converter o esquema, é possível criar um pacote do SSIS usando uma opção de menu de contexto de clique com o botão direito do mouse.
* A caixa de diálogo conexão do banco de dados SQL do Azure no SSMA também foi alterada para especificar o nome do servidor totalmente qualificado. Nas versões anteriores do SSMA, o prefixo do banco de dados SQL do Azure tinha que ser explicitamente mencionado dentro das configurações de projetos.

## <a name="ssma-v78"></a>SSMA v 7.8

A versão v 7.8 do SSMA para MySQL contém as seguintes alterações:

* Alterar o mapeamento de tipo realçado nas configurações do projeto.
* A capacidade dos usuários de desabilitar a telemetria.

## <a name="ssma-v77"></a>7.7 do SSMA v

A versão v 7.7 do SSMA para MySQL contém as seguintes alterações:

* O SSMA para MySQL foi aprimorado com correções direcionadas que melhoram a qualidade e a conversão de métricas.
* Com base na demanda popular, a versão de 32 bits do SSMA para MySQL está de volta. Em comparação com a implementação anterior (antes da v 7.4), há dois pacotes do instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base nos componentes de conectividade que tem. É sempre preferível usar a versão de 64 bits, se possível.
* O SSMA para MySQL agora tem o modo de conexão de cadeia de conexão ODBC, que permite que você use qualquer driver ODBC de terceiros que seja compatível com o MySQL.

## <a name="ssma-v76"></a>SSMA v 7.6

A versão v 7.6 do SSMA para MySQL foi aprimorada com correções direcionadas que melhoram as métricas de qualidade e conversão e com suporte para SQL Server 2017 (visualização pública). O suporte para SQL Server 2017 no Windows e no Linux está em visualização pública e não deve ser usado para migrações de produção.

## <a name="ssma-v75"></a>SSMA v 7.5

A versão v 7.5 do SSMA para MySQL foi aprimorada com várias melhorias para garantir maior acessibilidade para pessoas com deficiências.

## <a name="ssma-v74"></a>SSMA v 7.4

A versão v 7.4 do SSMA para MySQL contém as seguintes alterações:

* A opção de **tempo limite de consulta** agora está disponível durante a descoberta de objeto de esquema na origem e no destino.

    ![opção de tempo limite de consulta](../media/query-timeout_red.png)
* A métrica de qualidade e conversão foi aprimorada com correções direcionadas, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .NET 4.5.2 é um pré-requisito para a instalação do SSMA v 7.4. Além disso, a partir da v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>SSMA v 7.3

A versão v 7.3 do SSMA para MySQL contém as seguintes alterações:

* Métrica de qualidade e conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
* Estrutura de extensibilidade do SSMA exposta por meio dos seguintes itens:
  * Exporte a funcionalidade para um projeto SQL Server Data Tools (SSDT).
    * Agora você pode exportar scripts de esquema do SSMA para um projeto SSDT. Você pode usar os scripts de esquema para fazer alterações de esquema adicionais e implantar seu banco de dados.

      ![Comando Save as SSDT Project](../media/export-schema-scripts_red.png)
  * Bibliotecas que podem ser consumidas pelo SSMA para executar conversões personalizadas.
    * Agora você pode construir código que pode manipular conversões e conversões de sintaxe personalizadas que não eram previamente tratadas pelo SSMA.
      * As instruções sobre como construir um conversor personalizado estão disponíveis nesta postagem de blog, [estendendo os recursos de conversão de assistente de migração do SQL Server](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Baixe um projeto de exemplo para conversão desta [postagem de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v 7.2

A versão v 7.2 do SSMA para MySQL contém as seguintes alterações:

* Métrica de qualidade e conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
* Aprimoramentos de telemetria para fornecer melhores pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>SSMA v 7.1

A versão v 7.1 do SSMA para MySQL contém as seguintes alterações:

* SQL Server 2017 no Windows e Linux CTP1 agora é uma plataforma de destino com suporte para migração. Esse recurso está em visualização técnica e permite a movimentação de esquema e dados para servidores SQL de destino.
* O SSMA agora dá suporte a atualizações automáticas para baixar a versão mais recente do SSMA assim que estiver disponível.
* Os binários instaláveis do SSMA agora são fornecidos por meio dos arquivos de pacote do Windows Installer (. msi).

## <a name="may-2016"></a>Maio de 2016  
A versão de maio de 2016 do SSMA para MySQL contém as seguintes alterações:

* Adicionado suporte para SQL Server 2016.
* Analisador e resolvedor aprimorados.
* Verificação do instalador removida para .NET 2,0.
* Dependência do pacote de extensão atualizado do .net 3,5 para o .NET 4,0.
* Corrigido o mapeamento de tipo BigInt padrão para MySql.
* Corrigidos os comandos "salvar projeto" e "Abrir projeto" para o console do SSMA.
* Foi corrigido o comando "SecurePassword" para o console do SSMA.
* Contagem fixa de objetos para carregamento inicial.
* Corrigidos o carregamento de objetos MsSql.
* Corrigido o bug nas configurações globais.

## <a name="march-2016"></a>Março de 2016

A versão de visualização de março de 2016 do SSMA para MySQL adiciona suporte para migração para o SQL Server 2016. 
  
## <a name="january-2016"></a>Janeiro de 2016

A versão de manutenção de janeiro de 2016 do SSMA para MySQL contém as seguintes alterações:  

* Item de menu Exibir log adicionado ao SSMA (RFC 5706203).  
* Telemetria adicionada.  
  
## <a name="july-2014"></a>Julho de 2014

A versão de julho de 2014 do SSMA para MySQL contém as seguintes alterações:  
  
* Conversão de código do BD SQL do Azure aprimorada. 
* A funcionalidade do pacote de extensão foi movida para o esquema para dar suporte ao BD SQL do Azure.  
* Aprimoramentos de desempenho testados para bancos de dados com mais de 10 mil objetos.  
* Aprimoramentos da interface do usuário para lidar com um grande número de objetos.  
* Realce de esquemas LOB "bem conhecidos" (para que eles possam ser ignorados na conversão).  
* Melhorias na velocidade de conversão.  
* Mostrar contagens de objetos na interface do usuário.  
* Redução do tamanho do relatório em mais de 25%.  
* Mensagens de erro aprimoradas para construções não analisadas.  
  
## <a name="april-2014"></a>Abril de 2014

A versão de abril de 2014 do SSMA para MySQL contém as seguintes alterações:  
  
* Suporte adicionado do MS SQL Server 2014.  
* Correção de bugs referentes à conversão no Azure  
* Correção de bugs em relação a páginas de relatório invisíveis no IE 10.  
  
## <a name="july-2011"></a>julho de 2011

A versão de julho de 2011 do SSMA para MySQL contém as seguintes alterações:  
  
* Suporte para conversão de limite para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deslocamento "Denali".  
* Relatório de erros aprimorado durante a migração de dados.  
  
## <a name="april-2011"></a>Abril de 2011

A versão de abril de 2011 do SSMA para MySQL contém as seguintes alterações:  
  
* Instalável única do "SSMA para MySQL", que dá [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, "Denali" e Azure SQL.  
* A capacidade de conectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
* Mecanismo de migração de dados aprimorado do lado do cliente, oferecendo suporte à migração paralela de dados.  
* Melhor desempenho de migração de dados com modelos de recuperação simples e bulk-logged.  
* A versão do console do SSMA para MySQL dá suporte à compatibilidade com versões anteriores. Você pode abrir os projetos criados por versões anteriores ao SSMA v 5.0.  
* O produto SSMA para MySQL v 5.0 pode ser instalado lado a lado (SxS) com versões mais antigas do produto SSMA.  
  
## <a name="july-2010"></a>Julho de 2010

A versão de julho de 2010 do SSMA para MySQL contém os seguintes recursos:  
  
1. **Melhorias na interface do usuário:**  
  
    * Guia ' SQL Modes ' para objetos de banco de dados MySQL  
    * Guia ' configurações ' para objetos de banco de dados MySQL  
    * Guia ' dados ' para tabelas MySQL  
    * Configurações de projeto atualizadas em páginas de conversão e migração  
    * ' Configurações de migração de dados ' no nível de tabela  
  
2. **Melhorias para se conectar ao MySQL e SQL Server:**  
  
    * Conectividade SSL no MySQL  
    * Conectividade criptografada no SQL Server  
  
3. **Melhorias no Gerenciador de metabase do MySQL:**  
  
    * Carregando todos os objetos de banco de dados MySQL e suas respectivas guias.  
  
4. **Melhorias na conversão de objetos:**
  
    * Conversão de objetos da metabase do MySQL – procedimentos, funções, exibições, gatilhos e instruções.  
    * Suporte limitado para tipos de dados espaciais em tabelas.
    * Opção para converter funções do MySQL em SQL Server procedimentos armazenados  
    * Opção para aplicar modos SQL e mapeamento de charset durante a conversão de objeto  
  
5. **Melhorias na migração de dados:**  
  
    * Suporte para migração de dados usando mecanismos de migração de dados do lado do servidor e do cliente  
    * Suporte para migração de dados espaciais  
    * SQL personalizado para migração de dados para tabelas  
  
6. **Console do SSMA para MySQL:**  
  
    * Recurso de console de suporte para o SSMA para MySQL  
    * Suporte para interface de script  
  
## <a name="january-2010"></a>Janeiro de 2010

A versão de janeiro de 2010 do SSMA para MySQL foi a versão inicial. Ele continha os seguintes recursos: 
  
* Suporte adicionado para migração para o SQL Server local e o SQL do Azure.  
  
* **Instantâneo de recurso:** Migração de esquema e dados de tabelas/índices/restrições do MySQL.
