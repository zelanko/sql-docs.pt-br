---
title: O que há de novo no SSMA para Oracle (OracleToSQL) | Microsoft Docs
description: Saiba mais sobre as alterações feitas no Assistente de Migração do SQL Server (SSMA) para Oracle (OracleToSQL) para cada versão.
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 12/17/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
ms.author: alexiva
ms.openlocfilehash: 84a94725df5f3d1d817ed9f6de1048b9a54d6c64
ms.sourcegitcommit: a16b98d3bf3eeb58f5d2aeece2464f8a96e2b4a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2020
ms.locfileid: "97665837"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>O que há de novo no SSMA para Oracle (OracleToSQL)

Este artigo lista Assistente de Migração do SQL Server (SSMA) para alterações de Oracle em cada versão.

## <a name="ssma-v816"></a>8.16 do SSMA v

A versão v 8.16 do SSMA para Oracle contém as seguintes alterações:

* Adicionar suporte para colunas de identidade
* Remover suporte para analisador herdado
* Correção do problema com objetos que não estão sendo atualizados do banco de dados

## <a name="ssma-v815"></a>8.15 do SSMA v

Além de várias melhorias de acessibilidade, a versão v 8.15 do SSMA para Oracle contém as seguintes alterações:

* Adicionar configuração para usar especificação de tipo completo `%type` para `%rowtype` atributos e
* Relatórios de avaliação do renovando para trabalhar em navegadores modernos
* Autoridade de uso fornecida pelo banco de dados para autenticação do Azure AD
* Melhorar a nomenclatura para instruções carregadas de arquivos

## <a name="ssma-v814"></a>8.14 do SSMA v

Além de várias melhorias para garantir maior acessibilidade para pessoas com deficiências, a versão v 8.14 do SSMA para Oracle contém as seguintes alterações:

* Armazena a versão completa do servidor de origem/destino nos metadados do projeto (requer atualização do projeto)
* Usar dicionários de dados DBA para descoberta de objetos quando possível
* Corrigir problemas de vários analisadores ( `PIVOT` / `UNPIVOT` , `MERGE` , cotação alternativa)
* Corrigir a conversão de `INSERTING` / `DELETING` / `UPDATING` funções especiais em gatilhos

## <a name="ssma-v813"></a>8.13 do SSMA v

A versão v 8.13 do SSMA para Oracle contém as seguintes alterações:

* Corrigir a conversão `SQLCODE` de `SQLERRM` funções especiais em procedimentos locais
* Considere as conversões implícitas de tipo ao converter o procedimento e as chamadas de função
* Melhorar o log da cadeia de conexão de origem para ajudar a solucionar problemas de conexão

## <a name="ssma-v812"></a>SSMA v 8.12

A versão v 8.12 do SSMA para Oracle contém as seguintes alterações:

* Suporte para cláusulas de fatoração de subconsulta dentro de `INSERT` / `UPDATE` / `MERGE` / `DELETE` instruções
* Mensagem de conversão para `ON DELETE SET NULL` cláusula em casos de várias referências circulares ou de vários caminhos
* Conversão aprimorada de cursores criados a partir da cadeia de caracteres SQL dinâmica
* Atualizar ODP.NET para v 19.8

## <a name="ssma-v811"></a>8.11 do SSMA v

A versão v 8.11 do SSMA para Oracle contém as seguintes alterações:

* Suporte para subconsultas na `INSERT ... VALUES` instrução
* Conversão aprimorada da `COMMIT` instrução
* Corrigir o bug na `CONNECT BY LEVEL` conversão de cláusula
* Lógica de recuperação de erro do analisador atualizada para menos ávido
* Usar a biblioteca MSAL.NET para autenticação de Azure Active Directory interativa

## <a name="ssma-v810"></a>SSMA v 8.10

A versão v 8.10 do SSMA para Oracle contém pequenas melhorias de desempenho, bem como as seguintes alterações:

* Correção para o problema do testador com tabelas organizadas por índice
* Correção para os nomes dos procedimentos armazenados estendidos no pacote de extensões

## <a name="ssma-v89"></a>8.9 do SSMA v

A versão v 8.9 do SSMA para Oracle contém as seguintes alterações:

* Conversão de literais de cadeia de caracteres SQL dinâmica
* Conversão para `LAG` `FIRST_VALUE` e `LAST_VALUE` funções analíticas
* Adicionar suporte para `ALTER TRIGGER` / `ALTER INDEX` DDL básica (habilitar/desabilitar, etc.)
* Conversão aprimorada para colunas que correspondem a nomes de funções internas
* Gerar índices exclusivos filtrados para `NULL` colunas habilitadas
* Conversão de declaração de variável aprimorada para o Azure Synapse Analytics
* Correção do problema com caracteres especiais no nome do projeto

## <a name="ssma-v88"></a>8.8 do SSMA v

A versão v 8.8 do SSMA para Oracle inclui:

* Melhorias na estabilidade da sincronização de objetos do SQL Server
* Melhorias de desempenho de GUI durante a avaliação e conversão
* Conversão aprimorada de `OVER PARTITION` cláusulas analíticas
* Nova conversão para a `LEAD` função analítica
* Nova conversão para cláusulas de fatoração de subconsulta
* Nova `REPLICATE` opção de distribuição para o Azure Synapse Analytics
* Novo analisador de sintaxe Oracle para melhorar ainda mais o desempenho da conversão

## <a name="ssma-v87"></a>SSMA v 8.7

A versão v 8.7 do SSMA para Oracle tem pequenas correções e melhorias de desempenho na interface gráfica do usuário.

Além disso, o SSMA para Oracle agora permite filtrar objetos com base no estado de validade na caixa de diálogo ' Seleção avançada de objetos '.

> [!IMPORTANT]
> Com o SSMA v 8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se precisar instalar essa versão, você poderá baixar o arquivo de tempo de execução [aqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v 8.6

Além de um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho, a versão do v 8.6 do SSMA para Oracle foi aprimorada com a adição de uma configuração que permite aos usuários omitir as propriedades estendidas do SSMA no código convertido.

Para aproveitar essa configuração, no SSMA para Oracle, navegue até **ferramentas**  >  **configurações do projeto**  >    >  **conversão** geral e **, em** seguida, atualize o valor da configuração **omitir propriedades estendidas** para **Sim**.

![Omitir a configuração de propriedades estendidas](../oracle/media/ssma-omit-extended-properties.png)

Além disso, o SSMA para Oracle agora fornece uma análise aprimorada da `XMLTABLE` cláusula.

> [!IMPORTANT]
> Com o SSMA v 8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se precisar instalar essa versão, você poderá baixar o arquivo de tempo de execução [aqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v 8.5

A versão v 8.5 do SSMA para Oracle foi aprimorada com suporte para autenticação Azure Active Directory e suporte básico para recursos JSON no SQL Server, junto com um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho.

Além disso, o SSMA para Oracle foi aprimorado com suporte para:

* Limitando o número de objetos selecionados para descoberta a 990 (o `WHERE .. IN (..)` limite de cláusula da Oracle é de 1000 itens).
* Migração de dados do `RAW` para o `UNIQUEIDENTIFIER` .
* Análise da `PARALLEL_ENABLE` cláusula.

Por fim, a versão v 8.5 do SSMA para Oracle agora fornece:

* Desempenho aprimorado de constantes empacotadas convertidas.
* Uma atualização para o Oracle Provedor de Dados for .NET para a versão 19.5.0.

> [!IMPORTANT]
> Com o SSMA v 8.5, o .NET 4.7.2 é um pré-requisito de instalação. Se precisar instalar essa versão, você poderá baixar o arquivo de tempo de execução [aqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v 8.4

A versão v 8.4 do SSMA para Oracle foi aprimorada com correções direcionadas que foram projetadas para resolver problemas de acessibilidade e corrigir um bug relacionado a colunas de índice máximo (para permitir 32 em vez de 16) para SQL Server 2016 e versões posteriores.

Além disso, esta versão do SSMA para Oracle adiciona conversão para `SYS_REFCURSOR` parâmetros de procedimento armazenado `OUT` .

> [!IMPORTANT]
> Com o SSMA versões 7,4 a 8,4, o .NET 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v83"></a>SSMA v 8.3

A versão v 8.3 do SSMA para Oracle foi aprimorada com correções direcionadas que foram projetadas para melhorar a qualidade e a conversão de métricas. Além disso, esta versão do SSMA para Oracle fornece correções que:

* Solucionar problemas de acessibilidade.
* Adicione suporte básico para o `hierarchyid` tipo em SQL Server.
* Resolva um problema com um tipo de retorno desconhecido para uma função chamada por meio de sinônimo.
* Atualize ODP.NET para v 19.3.

## <a name="ssma-v82"></a>SSMA v 8.2

A versão v 8.2 do SSMA para Oracle é aprimorada para:

* Adicione suporte para `DBMS_OUTPUT.ENABLE` / `DISABLE` .
* Remova `CAST AS FLOAT` as `BINARY_FLOAT` `BINARY_DOUBLE` colunas e na consulta de migração de dados padrão.
* Corrigir sequências atualizar se o valor atual tiver sido alterado.
* Corrija o bug relacionado à má interpretação de pseudovariáveis ( `ROWNUM` etc.) se já existir uma coluna com o mesmo nome.
* Corrigir uma falha que ocorre na conversão de `FOR` loops com identificador não resolvido ambíguo.

Além disso, essa versão inclui um conjunto direcionado de correções projetadas para melhorar a qualidade e a conversão de métricas, bem como correções para:

* Um problema com índices não clusterizados desabilitados após a migração de dados.
* Detecção de .NET Framework durante a instalação silenciosa.
* Uma falha intermitente que ocorre quando uma nova versão é baixada.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v 8.1 para v 8.2. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v81"></a>SSMA v 8.1

A versão v 8.1 do SSMA para Oracle foi aprimorada com correções direcionadas que foram projetadas para melhorar a qualidade e a conversão de métricas.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v 8.0 para o v 8.1. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v80"></a>SSMA v 8.0

A versão v 8.0 do SSMA para Oracle foi aprimorada com correções direcionadas projetadas para melhorar a qualidade e a conversão de métricas. Esta versão também oferece os seguintes novos recursos:

* Suporte para o **Azure SQL instância gerenciada** como um destino. Agora você pode criar novos projetos destinados ao Azure SQL Instância Gerenciada:

  ![Projeto do SQL MI](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > O pacote de extensão do SSMA para Oracle também foi atualizado para permitir instalações remotas no Azure SQL Instância Gerenciada:
  >
  > ![Pacote de extensão do SSMA para Oracle](../media/ssma-oracle-ext-pack.png)

  Alguns recursos, incluindo o testador e a migração de dados do lado do servidor, não têm suporte ao direcionar o Azure SQL Instância Gerenciada. Leia mais sobre isso [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/).

* **Supervisor de correção** após a conversão. Saiba mais sobre isso [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Seleção preliminar de banco de dados/esquema.

  Ao se conectar à fonte, o usuário agora pode selecionar bancos de dados/esquemas de interesse. Selecionar somente os esquemas que você planeja migrar economizará tempo durante a conexão inicial e melhorará o desempenho geral do SSMA.

  ![Objetos de filtro do SSMA](../media/ssma-filter-objects.png)

* A capacidade de usar o driver .NET oficial e gerenciado para se conectar ao Oracle. O driver de OCI não é mais um pré-requisito para o uso de Assistente de Migração do SQL Server para Oracle.

* A capacidade de Mapear `ROWID` e `UROWID` para `VARCHAR` por padrão. Alterado de `uniqueidentifier` para acomodar a migração de dados para colunas explícitas `ROWID` .

## <a name="ssma-v710"></a>7.10 do SSMA v

A versão v 7.10 do SSMA para Oracle contém as seguintes alterações:

* Correções direcionadas projetadas para fornecer segurança adicional e proteções de privacidade para atender às alterações nos requisitos globais.
* Uma melhoria de conversão relacionada a consultas hierárquicas.

## <a name="ssma-v79"></a>7.9 do SSMA v

A versão v 7.9 do SSMA para Oracle contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Suporte para migrar instruções "Continue" do Oracle para SQL Server.
* Suporte na linha de comando do SSMA para alterar o mapeamento de tipo de dados e as preferências do projeto.
* Suporte para migrar dados usando SQL Server Integration Services (SSIS). Depois de converter o esquema, é possível criar um pacote do SSIS usando uma opção de menu de contexto de clique com o botão direito do mouse.
* A caixa de diálogo conexão do banco de dados SQL do Azure no SSMA também foi alterada para especificar o nome do servidor totalmente qualificado. Nas versões anteriores do SSMA, o prefixo do banco de dados SQL do Azure tinha que ser explicitamente mencionado dentro das configurações de projetos.

## <a name="ssma-v78"></a>SSMA v 7.8

A versão v 7.8 do SSMA para Oracle contém as seguintes alterações:

* Suporte para:
  * Expressão de linha para a `IN` cláusula.
  * Conversões implícitas de tipo.
  * `UID` conversão para o banco de dados SQL do Azure.
* Alterar o mapeamento de tipo realçado nas **configurações do projeto**.
* A capacidade dos usuários de desabilitar a telemetria.

## <a name="ssma-v77"></a>7.7 do SSMA v

A versão v 7.7 do SSMA para Oracle contém as seguintes alterações:

* O SSMA para Oracle foi aprimorado com correções direcionadas que melhoram a qualidade e a conversão de métricas.
* Com base na demanda popular, a versão de 32 bits do SSMA para Oracle está de volta. Em comparação com a implementação anterior (antes da v 7.4), há dois pacotes do instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base nos componentes de conectividade que tem. É sempre preferível usar a versão de 64 bits, se possível.
* SQL Server suporte a 2017 agora é oficial com o pacote de extensão Oracle com suporte no Linux também (nova opção de instalação remota). Observe que a funcionalidade do pacote de extensão é limitada quando instalada no Linux, já que não há suporte para os recursos de migração de dados do servidor e testador.
* O SSMA para Oracle permite que você migre exibições materializadas como tabelas regulares (configuráveis por meio das configurações em **configurações do projeto**  ->  **sincronização**  ->  **descobrir tabelas para exibições materializadas**).

## <a name="ssma-v76"></a>SSMA v 7.6

A versão v 7.6 do SSMA para Oracle foi aprimorada com correções direcionadas que melhoram as métricas de qualidade e conversão e com suporte para SQL Server 2017 (visualização pública). O suporte para SQL Server 2017 no Windows e no Linux está em visualização pública e não deve ser usado para migrações de produção.

## <a name="ssma-v75"></a>SSMA v 7.5

A versão v 7.5 do SSMA para Oracle contém as seguintes alterações:

* Aprimorado com várias melhorias para garantir maior acessibilidade para pessoas com deficiências.
* Atualizado para melhorar a métrica de qualidade e conversão com correções direcionadas, como o tratamento aprimorado de tipos de dados de data e float durante a migração de dados, com base nos comentários dos clientes.

## <a name="ssma-v74"></a>SSMA v 7.4

A versão v 7.4 do SSMA para Oracle contém as seguintes alterações:

* O SSMA para Oracle agora dá suporte à análise de Synapse do Azure como uma plataforma de destino para migração.

  ![Janela Novo Projeto](../media/new-project.png)
  * O oferece suporte às opções de armazenamento data warehouse, conforme mostrado na imagem a seguir:

  ![opções de armazenamento para data warehouse](../media/storage-options_red.png)
  * O oferece suporte às opções de distribuição de dados, conforme mostrado na imagem a seguir:

  ![distribuição de dados para data warehouse](../media/data-distribution_red.png)

* A opção de **tempo limite de consulta** agora está disponível durante a descoberta de objeto de esquema na origem e no destino.

  ![opção de tempo limite de consulta](../media/query-timeout_red.png)

* A métrica de qualidade e conversão foi aprimorada com correções direcionadas, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .NET 4.5.2 é um pré-requisito para a instalação do SSMA v 7.4. Além disso, a partir da v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>SSMA v 7.3

A versão v 7.3 do SSMA para Oracle contém as seguintes alterações:

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

A versão v 7.2 do SSMA para Oracle contém as seguintes alterações:

* Métrica de qualidade e conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
* Aprimoramentos de telemetria para fornecer melhores pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>SSMA v 7.1

A versão v 7.1 do SSMA para Oracle contém as seguintes alterações:

* SQL Server 2017 no Windows e Linux CTP1 agora é uma plataforma de destino com suporte para migração. Esse recurso está em visualização técnica e permite a movimentação de esquema e dados para servidores SQL de destino.
* O SSMA agora dá suporte a atualizações automáticas para baixar a versão mais recente do SSMA assim que estiver disponível.
* Os binários instaláveis do SSMA agora são entregues por meio de arquivos de pacote Windows Installer (. msi).

## <a name="may-2016"></a>Maio de 2016

A versão de maio de 2016 do SSMA para Oracle contém as seguintes alterações:

* Adicionado suporte para SQL Server 2016.
* Adicionada a conversão de tabelas de arquivamento do Oracle Flashback para SQL Server tabelas temporais.

  > [!NOTE]
  > O SSMA não copia dados de histórico de tabelas de arquivamento de dados do Oracle Flashback. Como resultado, os dados do histórico devem ser copiados manualmente durante o processo de migração. Além disso, embora o SSMA não exiba a tabela de histórico no SQL Server Gerenciador de metadados porque ele é tratado como uma tabela do sistema, você pode exibir a tabela de histórico em SQL Server Management Studio.
  >
  > O SQL Server 2016 não dá suporte a vários recursos do Oracle Flashback, incluindo:
  >
  >   * Consulta de transação do Oracle Flashback
  >   * `DBMS_FLASHBACK` Pacote
  >   * Transação do flashback
  >   * Arquivo de dados do flashback
  >   * Tabela flashback
  >   * Descartar flashback
  >   * Banco de dados flashback

* Adicionada a conversão da política do Oracle VPD em SQL Server objetos de política (Segurança em Nível de Linha para Oracle).
* Tempo reduzido de carregamento inicial para Oracle.
* Analisador e resolvedor aprimorados.
* Verificação do instalador removida para .NET 2,0.
* Dependência do pacote de extensão atualizado do .NET 3,5 para o .NET 4,0.
* Corrigidos `save-project` e `open-project` comandos para o console do SSMA.
* `securepassword`Comando fixo para o console do SSMA.
* Contagem fixa de objetos para carregamento inicial.
* Correção da conversão de tipos de dados de caractere para Oracle.
* Corrigido o bug nas configurações globais.

## <a name="march-2016"></a>Março de 2016

A versão de visualização de março de 2016 do SSMA para Oracle adicionou suporte para:

* Migração para SQL Server 2016.
* Migração do Oracle Segurança em Nível de Linha (com algumas limitações).
* Migrando o Oracle nas tabelas de memória para SQL Server repositório de coluna.

## <a name="january-2016"></a>Janeiro de 2016

A versão de manutenção de janeiro de 2014 do SSMA para Oracle contém as seguintes alterações:

* Suporte adicionado para índices clusterizados.
* Correção de consultas de esquema Oracle lentas (RFC 5076207).
* Correção da conexão ao Azure do console.
* Item de menu Exibir log adicionado ao SSMA (RFC 5706203).
* Telemetria adicionada.

## <a name="july-2014"></a>Julho de 2014

A versão de julho de 2014 do SSMA para Oracle contém as seguintes alterações:

* Adicionado suporte para o banco de dados SQL do Azure.
* Funcionalidade do pacote de extensão movida para o esquema para dar suporte ao banco de dados SQL do Azure.
* Suporte adicionado para exibições materializadas da Oracle.
* Adicionado suporte para tabelas com otimização de memória SQL Server 2014.
* Aprimoramentos de desempenho incluídos testados para bancos de dados com mais de 10 mil objetos.
* Foram adicionadas melhorias na interface do usuário para lidar com um grande número de objetos.
* Adicionado o realce de esquemas LOB bem conhecidos.
* Melhorias de velocidade de conversão incluídas.
* Adicionado suporte para mostrar contagens de objeto na interface do usuário.
* Tamanho de relatório reduzido em mais de 25%.
* Mensagens de erro aprimoradas para construções não analisadas.

## <a name="april-2014"></a>Abril de 2014

A versão de abril de 2014 do SSMA para Oracle contém as seguintes alterações:

* Suporte adicionado do MS SQL Server 2014.
* Adição de suporte do Oracle 12 e da otimização de consultas.
* Correção de bugs referentes à conversão no Azure.
* Correção de bugs em relação a páginas de relatório invisíveis no IE 10.

## <a name="january-2012"></a>Janeiro de 2012

A versão de janeiro de 2012 do SSMA para Oracle adiciona suporte para `RowType` e `RecordType` parâmetros de entrada padronizados para `NULL` .

## <a name="july-2011"></a>julho de 2011

A versão de julho de 2011 do SSMA para Oracle contém as seguintes alterações:

* Suporte adicionado para conversão de sequência Oracle para [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] gerador de sequência.
* Relatório de erros aprimorado durante a migração de dados.
* Conversão aprimorada de instrução usando palavras reservadas.
* Melhor conversão implícita de valor de data em uma função.

## <a name="april-2011"></a>Abril de 2011

A versão de abril de 2011 do SSMA para Oracle contém as seguintes alterações:

* Produto consolidado "SSMA para Oracle", que dá suporte ao [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] e ao [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] .
* Adicionado suporte para conexão e migração para o [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] .
* Mecanismo de migração de dados aprimorado do lado do cliente, oferecendo suporte à migração paralela de dados.
* Melhor desempenho de migração de dados com o `Simple` e os `Bulk` modelos de recuperação registrados.
* Suporte adicionado para compatibilidade com versões anteriores de projetos criados por versões mais antigas do SSMA (v 4.0 e v 4.2).
* Foi adicionada a capacidade de instalar o SSMA para o produto Oracle v 5.0 lado a lado (SxS) com versões mais antigas do SSMA (v 4.0 e v 4.2).
* Suporte adicionado para relatórios de tipos de User-Defined (inclui subtipo, `VARRAY` ,, `NESTED TABLE` tabela de objetos e exibição de objeto) e seus usos em blocos PL/SQL com mensagens de erro especiais.

## <a name="july-2010"></a>Julho de 2010

A versão de julho de 2010 do SSMA para Oracle foi adicionada:

* Suporte para migrar para o SQL Server 2008 R2.
* Um novo aplicativo de console do SSMA para execução de linha de comando.
* Suporte para migração de dados usando Server-Side e Client-Side mecanismos de migração de dados.
* Suporte para a instrução "SELECT personalizado" na migração de dados.
* Suporte para migração do Oracle 11g R2.

## <a name="june-2008"></a>Junho de 2008

A versão de junho de 2008 do SSMA para Oracle contém as seguintes alterações:

* Foram adicionadas melhorias ao relatório de avaliação, incluindo informações adicionais para sinônimos, fonte bruta para objetos analisáveis, painéis e SQL Server a remoção de logotipo e persistência de layout.
* Aprimoramentos adicionados na conversão de objeto:
  * Pacotes `DBMS_LOB` , `DBMS_SQL` conversão adicionada.
  * A conversão de junções foi revisada.
  * Modificação de coleções e conversão de registros, agora conversão de registros em casos simples liberados por meio de variáveis separadas para cada campo.
  * Melhorias de implementação de registros e coleções.
  * Funções de agregação de janela adicionadas.
  * `ROLLUP`/`CUBE` cláusula adicionada.
  * Melhoria para `NEXTVAL` / `CURVAL` .
  * As colunas agrupadas na `SET` cláusula, conjuntos de agrupamento e ID de agrupamento foram adicionadas.
  * `MERGE` instrução adicionada.
  * Suporte a novos tipos DateTime e conversão de registros e coleções como tipos de dados CLR adicionados.
* Novos recursos adicionados do testador. Agora, as tabelas podem ser testadas como objetos usando o testador, uma ordem de chamada de vários objetos que podem ser testados no caso de teste pode ser alterada, o usuário pode testar procedimentos e funções com registros e coleções como parâmetros e valores de retorno, e um analisador de dependências foi adicionado para verificar apenas as tabelas usadas.
  
## <a name="august-2007"></a>Agosto de 2007

A versão de agosto de 2007 do SSMA para Oracle adicionou:

* Um novo componente de testador permite criar, gerenciar e executar casos de teste para verificar o código SQL convertido.
* O suporte para conversão de subtipos, coleções e módulos locais do Oracle foi adicionado ao conversor do SQL.
* Um novo recurso de sincronização permite sincronizar objetos específicos com o SQL Server banco de dados.
* Novas opções de conversão.
  
## <a name="april-2007"></a>Abril de 2007

A versão de abril de 2007 do SSMA para Oracle foi a versão inicial.
