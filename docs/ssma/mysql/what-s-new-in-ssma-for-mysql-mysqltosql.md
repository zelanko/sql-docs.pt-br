---
title: O que há de novo no SSMA para MySQL (MySQLToSql) | Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
ms.author: jtoland;alexiva
ms.openlocfilehash: 9d5c33bbb9e09a5a833c928547a5ec659fe43c96
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625547"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>Novidades no SSMA para MySQL (MySQLToSql)

Este artigo lista o SQL Server Migration Assistant (SSMA) para alterações do MySQL em cada versão.

## <a name="ssma-v88"></a>SSMA v8.8

A versão v8.8 do SSMA para MySQL inclui:

* Melhorias na estabilidade da sincronização de objetos sql
* Melhorias no desempenho da GUI durante a avaliação e conversão

## <a name="ssma-v87"></a>SSMA v8.7

A versão v8.7 do SSMA para MySQL tem pequenas correções e melhorias de desempenho na interface gráfica do usuário.

Além disso, o SSMA para MySQL agora fornece conversão para `LIMIT` cláusula ao atingir o Azure SQL.

> [!IMPORTANT]
> Com o SSMA v8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v8.6

Além de um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho, a versão v8.6 do SSMA para MySQL foi aprimorada adicionando uma configuração que permite que os usuários omitam propriedades estendidas sSMA no código convertido.

Para aproveitar essa configuração, no SSMA para MySQL, navegue até**configurações** > **gerais** > de projetos de **Tools** > **ferramentas**e, em seguida, em **Misc,** atualize o valor da configuração **Omit Extended Properties** para **Sim**.

![Omita configuração de propriedades estendidas](../mysql/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> Com o SSMA v8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v8.5

A versão v8.5 do SSMA para MySQL é aprimorada com suporte para autenticação do Azure Active Directory e suporte básico para recursos JSON no servidor SQL, juntamente com um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho.

> [!IMPORTANT]
> Com o SSMA v8.5, .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v8.4

A versão v8.4 do SSMA para MySQL é aprimorada com correções direcionadas que são projetadas para resolver problemas de acessibilidade e corrigir um bug relacionado às colunas de índice max (para permitir 32 em vez de 16) para as versões SQL Server 2016 e posteriores.

> [!IMPORTANT]
> Com as versões SSMA 7.4 embora 8.4, .NET 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v83"></a>SSMA v8.3

A versão v8.3 do SSMA para MySQL é aprimorada com correções direcionadas que são projetadas para melhorar as métricas de qualidade e conversão. Além disso, esta versão do SSMA para MySQL fornece correções que:

* Abordar problemas de acessibilidade.
* Adicione suporte `hierarchyid` básico para o tipo no SQL Server.

## <a name="ssma-v82"></a>SSMA v8.2

A versão v8.2 do SSMA para MySQL é aprimorada com um conjunto direcionado de correções projetadas para melhorar as métricas de qualidade e conversão, bem como correções para:

* Um problema com índices não agrupados desativados após a migração de dados.
* Detecção de .NET Framework durante a instalação silenciosa.
* Um acidente intermitente que ocorre quando uma nova versão é baixada.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v8.1 para o v8.2. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

A versão v8.1 do SSMA para MySQL é aprimorada com correções direcionadas que são projetadas para melhorar as métricas de qualidade e conversão.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v8.0 para v8.1. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

A versão v8.0 do SSMA para MySQL é aprimorada com correções direcionadas projetadas para melhorar as métricas de qualidade e conversão. Esta versão também oferece os seguintes novos recursos:

* Suporte à instância gerenciada do banco de **dados SQL do Azure** como alvo. Agora você pode criar novos projetos direcionados à instância gerenciada do banco de dados SQL do Azure:

  ![Projeto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Orientador de **correção pós-conversão**. Saiba mais sobre isso [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Base de dados preliminar/seleção de esquemas.

  Ao se conectar à fonte, o usuário agora pode selecionar bancos de dados/esquemas de interesse. Selecionar apenas os esquemas que você planeja migrar economizará tempo durante a conexão inicial e melhorará o desempenho geral do SSMA.

  ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

A versão v7.10 do SSMA para MySQL contém as seguintes alterações:

* Correções direcionadas projetadas para fornecer proteções adicionais de segurança e privacidade para atender às mudanças nos requisitos globais.
* Uma correção para conversão de espaços entre nome de função e lista de argumentos.

## <a name="ssma-v79"></a>SSMA v7.9

A versão v7.9 do SSMA para MySQL contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Suporte parcial para migração de tipos de dados espaciais do MySQL para o Azure SQL Database.
* Suporte na linha de comando SSMA para alterar mapeamento de tipo de dados e preferências de projeto.
* Suporte para migração de dados usando SSIS (SSIS Server Integration Services, serviços de integração de servidores SQL). Depois de converter o esquema, é possível criar um pacote SSIS usando uma opção de menu de contexto com o botão direito do mouse.
* A caixa de diálogo de conexão Banco de dados Azure SQL no SSMA também foi alterada para especificar o nome do servidor totalmente qualificado. Nas versões anteriores do SSMA, o prefixo do Banco de Dados SQL do Azure tinha que ser explicitamente mencionado dentro das configurações dos projetos.

## <a name="ssma-v78"></a>SSMA v7.8

A versão v7.8 do SSMA para MySQL contém as seguintes alterações:

* Alterar mapeamento de tipo destacado nas Configurações do projeto.
* A capacidade dos usuários de desativar a telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

A versão v7.7 do SSMA para MySQL contém as seguintes alterações:

* O SSMA para MySQL foi aprimorado com correções direcionadas que melhoram as métricas de qualidade e conversão.
* Com base na demanda popular, a versão de 32 bits do SSMA para MySQL está de volta. Em comparação com a implementação anterior (antes do v7.4), existem dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base nos componentes de conectividade que você tem. É sempre preferível usar a versão de 64 bits, se possível.
* O SSMA para MySQL agora tem o modo de conexão Conexão Conexão ODBC, que permite que você use quaisquer drivers ODBC de terceiros compatíveis com o MySQL.

## <a name="ssma-v76"></a>SSMA v7.6

A versão v7.6 do SSMA para MySQL foi aprimorada com correções direcionadas que melhoram as métricas de qualidade e conversão e com suporte para o SQL Server 2017 (visualização pública). O suporte ao SQL Server 2017 no Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

## <a name="ssma-v75"></a>SSMA v7.5

A versão v7.5 do SSMA para MySQL foi aprimorada com várias melhorias para garantir maior acessibilidade para pessoas com deficiência.

## <a name="ssma-v74"></a>SSMA v7.4

A versão v7.4 do SSMA para MySQL contém as seguintes alterações:

* A **opção de tempo de tempo de consulta** está agora disponível durante a descoberta de objetos de esquema na origem e no destino.

    ![opção de tempo de consulta](../media/query-timeout_red.png)
* A métrica de qualidade e conversão foi melhorada com correções direcionadas, com base no feedback do cliente.

> [!IMPORTANT]
> .NET 4.5.2 é um pré-requisito para instalar o SSMA v7.4. Além disso, começando com o v7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>SSMA v7.3

A versão v7.3 do SSMA para MySQL contém as seguintes alterações:

* Melhor qualidade e métrica de conversão com correções direcionadas com base no feedback do cliente.
* Estrutura de extensibilidade ssma exposta através dos seguintes itens:
  * Exportar funcionalidade para um projeto SSDT (SSDT) de SQL Server Data Tools.
    * Agora você pode exportar scripts de esquema de SSMA para um projeto SSDT. Você pode usar os scripts do esquema para fazer alterações adicionais de esquema e implantar seu banco de dados.

      ![Salvar como comando de projeto SSDT](../media/export-schema-scripts_red.png)
  * Bibliotecas que podem ser consumidas pela SSMA para realizar conversões personalizadas.
    * Agora você pode construir códigos que podem lidar com conversões e conversões de sintaxe personalizadas que não foram tratadas anteriormente pela SSMA.
      * Instruções sobre como construir um conversor personalizado estão disponíveis neste post de blog, [estendendo os recursos de conversão do SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Baixe um projeto de exemplo para conversão a partir deste [post do blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2

A versão v7.2 do SSMA para MySQL contém as seguintes alterações:

* Melhor qualidade e métrica de conversão com correções direcionadas com base no feedback do cliente.
* Melhorias na telemetria para fornecer melhores pontos de dados para solucionar problemas dos clientes e melhorar as taxas de conversão da SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

A versão v7.1 do SSMA para MySQL contém as seguintes alterações:

* O SQL Server 2017 no Windows e linux CTP1 é agora uma plataforma-alvo suportada para migração. Esse recurso está na pré-visualização técnica e permite que o esquema e a movimentação de dados direcionem os servidores SQL.
* O SSMA agora suporta atualizações automáticas para baixar a versão mais recente do SSMA assim que estiver disponível.
* Binários instalados do SSMA agora são entregues através de arquivos de pacote do Windows Installer (.msi).

## <a name="may-2016"></a>Maio de 2016

A versão de maio de 2016 do SSMA para MySQL contém as seguintes alterações:

* Suporte adicionado ao SQL Server 2016.
* Melhor apare e resolver.
* Verificação do instalador removido para .NET 2.0.
* Dependência atualizada do pacote de extensão de .NET 3.5 a .NET 4.0.
* Mapeamento padrão do tipo BigInt para MySql.
* Fixo `save-project` `open-project` e comandos para console SSMA.
* Comando `securepassword` fixo para console SSMA.
* Contagem fixa de objetos para carregamento inicial.
* Corrigimos o carregamento de objetos MsSql.
* Corrigido bug em configurações globais.

## <a name="march-2016"></a>Março de 2016

A versão prévia de março de 2016 do SSMA para MySQL adiciona suporte à migração para o SQL Server 2016.
  
## <a name="january-2016"></a>Janeiro de 2016

A versão de manutenção de janeiro de 2016 do SSMA para MySQL contém as seguintes alterações:

* Adicionado Ver o item do menu de log ao SSMA (RFC 5706203).
* Adicionado Telemetria.
  
## <a name="july-2014"></a>Julho de 2014

A versão de julho de 2014 do SSMA para MySQL contém as seguintes alterações:
  
* Conversão aprimorada do código Azure SQL DB.
* A funcionalidade do pacote de extensão mudou-se para esquema para suportar o Azure SQL DB.
* Melhorias de desempenho testadas para bancos de dados com mais de 10k objetos.
* Melhorias na IA para lidar com um grande número de objetos.
* Destaque de esquemas lob bem conhecidos (para que possam ser ignorados em conversão).
* Melhorias na velocidade de conversão.
* Mostrar contagens de objetos em UI.
* Redução de tamanho do relatório em mais de 25%.
* Mensagens de erro melhoradas para construções não parsed.
  
## <a name="april-2014"></a>Abril de 2014

A versão de abril de 2014 do SSMA para MySQL contém as seguintes alterações:
  
* Suporte adicionado ao SQL Server 2014.
* Corrigimos bugs em relação à conversão para o Azure.
* Corrigimos bugs em relação às páginas de relatórios invisíveis no IE 10.
  
## <a name="july-2011"></a>julho de 2011

A versão de julho de 2011 do SSMA para MySQL contém as seguintes alterações:
  
* Suporte para `LIMIT` conversão [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] `OFFSET`de .
* Relatórios de erros aprimorados durante a migração de dados.
  
## <a name="april-2011"></a>abril de 2011

A versão de abril de 2011 do SSMA para MySQL contém as seguintes alterações:
  
* Instalável único de "SSMA for MySQL", que suporta [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]e [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] Azure SQL.
* A capacidade [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]de se conectar.
* Mecanismo de migração de dados do lado do cliente aprimorado, suportando migração paralela de dados.
* Melhor desempenho de migração de dados com modelos de recuperação registrados simples e a granel.
* A versão SSMA for MySQL Console suporta compatibilidade retrógrada. Você pode abrir os projetos criados por versões anteriores ao SSMA v5.0.
* O produto SSMA para MySQL v5.0 pode ser instalado lado a lado (SxS) com versões mais antigas do Produto SSMA.
  
## <a name="july-2010"></a>Julho de 2010

A versão de julho de 2010 do SSMA para MySQL contém os seguintes recursos:
  
**1. Melhorias na interface do usuário:**

* Guia 'Modos SQL' para objetos do banco de dados MySQL
* Guia 'Configurações' para objetos do banco de dados MySQL
* Guia 'Dados' para Tabelas MySQL
* Configurações atualizadas do projeto em páginas de conversão e migração
* 'Configurações de migração de dados' no nível da tabela
  
**2. Melhorias para conectar ao MySQL e ao SQL Server:**
  
* Conectividade SSL no MySQL
* Conectividade criptografada no sql server
  
**3. Melhorias no MySQL Metabase Explorer:**
  
* Carregando todos os Objetos de Banco de Dados MySQL e suas respectivas guias.
  
**4. Melhorias na conversão de objetos:**
  
* Conversão de objetos MySQL Metabase - Procedimentos, Funções, Visualizações, Gatilhos e Declarações.
* Suporte limitado para tipos de dados espaciais em tabelas.
* Opção para converter funções MySQL em procedimentos armazenados pelo SQL Server
* Opção para aplicar modos SQL e mapeamento charset durante a conversão de objetos
  
**5. Melhorias na migração de dados:**  
  
* Suporte para migração de dados usando mecanismos de migração de dados do lado do servidor e do lado do cliente
* Suporte para migração de dados espaciais
* SQL personalizado para migração de dados para tabelas
  
**6. SSMA para Console MySQL:**  
  
* Recurso de console de suporte para SSMA para MySQL  
* Suporte para interfrontal em nível de script  
  
## <a name="january-2010"></a>janeiro de 2010

O lançamento em janeiro de 2010 do SSMA para MySQL foi o lançamento inicial. Continha as seguintes características:
  
* Adicionado suporte para migração para sql server local e SQL Azure.  
  
* **Instantâneo de recurso:** Esquema e migração de dados de Tabelas/Índices/Restrições MySQL.
