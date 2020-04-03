---
title: O que há de novo no SSMA para Oracle (OracleToSQL) | Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
ms.author: jtoland;alexiva
ms.openlocfilehash: 88b87aad931f28637accc95aa4d993037fcf0b0a
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625604"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>O que há de novo no SSMA para Oracle (OracleToSQL)

Este artigo lista o SQL Server Migration Assistant (SSMA) para alterações oracle em cada versão.

## <a name="ssma-v88"></a>SSMA v8.8

A versão v8.8 do SSMA para Oracle inclui:

* Melhorias na estabilidade da sincronização de objetos sql
* Melhorias no desempenho da GUI durante a avaliação e conversão
* Conversão melhorada de `OVER PARTITION` cláusulas analíticas
* Nova conversão `LEAD` para função analítica
* Nova conversão para cláusulas de fatoração de subquery
* Nova `REPLICATE` opção de distribuição para o Azure SQL Data Warehouse
* Novo analisador de sintaxe Oracle para melhorar ainda mais o desempenho de conversão

## <a name="ssma-v87"></a>SSMA v8.7

A versão v8.7 do SSMA para Oracle tem pequenas correções e melhorias de desempenho na interface gráfica do usuário.

Além disso, o SSMA para Oracle agora permite filtrar objetos com base no estado de validade na caixa de diálogo 'Seleção avançada de objetos'.

> [!IMPORTANT]
> Com o SSMA v8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v8.6

Além de um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho, a versão v8.6 do SSMA para Oracle foi aprimorada adicionando uma configuração que permite que os usuários omitam propriedades estendidas sSMA no código convertido.

Para aproveitar essa configuração, no SSMA para Oracle, navegue até as**configurações** > gerais do projeto **de ferramentas** > **conversão****geral** > e, em seguida, em **Misc,** atualize o valor da configuração **Propriedades Estendidas omitis** para **Sim**.

![Omita configuração de propriedades estendidas](../oracle/media/ssma-omit-extended-properties.png)

Além disso, o SSMA para Oracle agora `XMLTABLE` fornece um melhor parsing da cláusula.

> [!IMPORTANT]
> Com o SSMA v8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v8.5

A versão v8.5 do SSMA para Oracle é aprimorada com suporte para autenticação do Azure Active Directory e suporte básico para recursos JSON no servidor SQL, juntamente com um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho.

Além disso, o SSMA para Oracle foi aprimorado com suporte para:

* Limitando o número de objetos selecionados para `WHERE .. IN (..)` descoberta a 990 (o limite de cláusula da Oracle é de 1000 itens).
* Migração `RAW` de `UNIQUEIDENTIFIER`dados de para .
* Análise de `PARALLEL_ENABLE` cláusulas.

Finalmente, a versão v8.5 do SSMA para Oracle agora fornece:

* Melhor desempenho das constantes embaladas convertidas.
* Uma atualização para Oracle Data Provider para .NET para a versão 19.5.0.

> [!IMPORTANT]
> Com o SSMA v8.5, .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v8.4

A versão v8.4 do SSMA para Oracle é aprimorada com correções direcionadas que são projetadas para resolver problemas de acessibilidade e corrigir um bug relacionado às colunas de índice max (para permitir 32 em vez de 16) para o SQL Server 2016 e versões posteriores.

Além disso, esta versão do SSMA `SYS_REFCURSOR` para `OUT` Oracle adiciona conversão para como parâmetros de procedimento armazenados.

> [!IMPORTANT]
> Com as versões SSMA 7.4 a 8.4, .NET 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v83"></a>SSMA v8.3

A versão v8.3 do SSMA para Oracle é aprimorada com correções direcionadas que são projetadas para melhorar as métricas de qualidade e conversão. Além disso, esta versão do SSMA para Oracle fornece correções que:

* Abordar problemas de acessibilidade.
* Adicione suporte `hierarchyid` básico para o tipo no SQL Server.
* Resolva um problema com um tipo de retorno desconhecido para uma função chamada através de sinônimo.
* Atualização ODP.NET para v19.3.

## <a name="ssma-v82"></a>SSMA v8.2

A versão v8.2 do SSMA para Oracle é aprimorada para:

* Adicionar suporte `DBMS_OUTPUT.ENABLE` / `DISABLE`para .
* Remova `CAST AS FLOAT` `BINARY_FLOAT` para `BINARY_DOUBLE` e colunas na consulta de migração de dados padrão.
* Corrigir seqüências de atualização se o valor atual tiver sido alterado.
* Corrigir bug relacionado à má interpretação de`ROWNUM`pseudo-colunas (, etc.) se existir uma coluna com o mesmo nome.
* Corrija um trava-falha que ocorre convertendo `FOR` loops com identificador ambíguo não resolvido.

Além disso, esta versão inclui um conjunto direcionado de correções projetadas para melhorar as métricas de qualidade e conversão, bem como correções para:

* Um problema com índices não agrupados desativados após a migração de dados.
* Detecção de .NET Framework durante a instalação silenciosa.
* Um acidente intermitente que ocorre quando uma nova versão é baixada.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v8.1 para o v8.2. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

A versão v8.1 do SSMA para Oracle é aprimorada com correções direcionadas que são projetadas para melhorar as métricas de qualidade e conversão.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v8.0 para v8.1. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

A versão v8.0 do SSMA para Oracle é aprimorada com correções direcionadas projetadas para melhorar as métricas de qualidade e conversão. Esta versão também oferece os seguintes novos recursos:

* Suporte à instância gerenciada do banco de **dados SQL do Azure** como alvo. Agora você pode criar novos projetos direcionados à instância gerenciada do banco de dados SQL do Azure:

  ![Projeto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > O SSMA for Oracle Extension Pack também foi atualizado para permitir instalações remotas na instância gerenciada do banco de dados Azure SQL:
  >
  > ![Pacote de extensão SSMA para Oracle](../media/ssma-oracle-ext-pack.png)

  Alguns recursos, incluindo a migração de dados do lado do Tester e do servidor, não são suportados ao direcionar a instância gerenciada do banco de dados Azure SQL. Leia mais sobre isso [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/).

* Orientador de **correção pós-conversão**. Saiba mais sobre isso [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Base de dados preliminar/seleção de esquemas.

  Ao se conectar à fonte, o usuário agora pode selecionar bancos de dados/esquemas de interesse. Selecionar apenas os esquemas que você planeja migrar economizará tempo durante a conexão inicial e melhorará o desempenho geral do SSMA.

  ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

* A capacidade de usar o driver .NET oficial gerenciado para se conectar à Oracle. O driver OCI não é mais um pré-requisito para usar o SQL Server Migration Assistant para Oracle.

* A capacidade `ROWID` de `UROWID` `VARCHAR` mapear e por padrão. Alterado `uniqueidentifier` para acomodar a `ROWID` migração de dados para colunas explícitas.

## <a name="ssma-v710"></a>SSMA v7.10

A versão v7.10 do SSMA para Oracle contém as seguintes alterações:

* Correções direcionadas projetadas para fornecer proteções adicionais de segurança e privacidade para atender às mudanças nos requisitos globais.
* Uma melhoria de conversão relacionada a consultas hierárquicas.

## <a name="ssma-v79"></a>SSMA v7.9

A versão v7.9 do SSMA para Oracle contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Suporte para migrar declarações "Continuar" do Oracle para o SQL Server.
* Suporte na linha de comando SSMA para alterar mapeamento de tipo de dados e preferências de projeto.
* Suporte para migração de dados usando SSIS (SSIS Server Integration Services, serviços de integração de servidores SQL). Depois de converter o esquema, é possível criar um pacote SSIS usando uma opção de menu de contexto com o botão direito do mouse.
* A caixa de diálogo de conexão Banco de dados Azure SQL no SSMA também foi alterada para especificar o nome do servidor totalmente qualificado. Nas versões anteriores do SSMA, o prefixo do Banco de Dados SQL do Azure tinha que ser explicitamente mencionado dentro das configurações dos projetos.

## <a name="ssma-v78"></a>SSMA v7.8

A versão v7.8 do SSMA para Oracle contém as seguintes alterações:

* Suporte para:
  * Expressão de `IN` linha para a cláusula.
  * Moldes de tipo implícito.
  * `UID`conversão para Banco de Dados SQL do Azure.
* Alterar mapeamento de tipo destacado nas **Configurações do projeto**.
* A capacidade dos usuários de desativar a telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

A versão v7.7 do SSMA para Oracle contém as seguintes alterações:

* O SSMA para Oracle foi aprimorado com correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Com base na demanda popular, a versão de 32 bits do SSMA para Oracle está de volta. Em comparação com a implementação anterior (antes do v7.4), existem dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base nos componentes de conectividade que você tem. É sempre preferível usar a versão de 64 bits, se possível.
* O suporte ao SQL Server 2017 agora é oficial com o Oracle Extension Pack suportado no Linux também (nova opção de instalação remota). Observe que a funcionalidade do Extension Pack é limitada quando instalada no Linux, já que os recursos de migração de dados do lado do teste e do servidor não são suportados.
* O SSMA for Oracle permite migrar visualizações materializadas como tabelas regulares (configuráveis através das configurações em **Configurações do projeto** -> **Sincronização** -> **Descubra tabelas de backup para visualizações materializadas**).

## <a name="ssma-v76"></a>SSMA v7.6

A versão v7.6 do SSMA para Oracle é aprimorada com correções direcionadas que melhoram as métricas de qualidade e conversão e com suporte para o SQL Server 2017 (visualização pública). O suporte ao SQL Server 2017 no Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

## <a name="ssma-v75"></a>SSMA v7.5

A versão v7.5 do SSMA para Oracle contém as seguintes alterações:

* Aprimorado com diversas melhorias para garantir maior acessibilidade para pessoas com deficiência.
* Atualizado para melhorar a métrica de qualidade e conversão com correções direcionadas, como melhor manuseio de data e tipos de dados flutuantes durante a migração de dados, com base no feedback do cliente.

## <a name="ssma-v74"></a>SSMA v7.4

A versão v7.4 do SSMA para Oracle contém as seguintes alterações:

* O SSMA for Oracle agora suporta o Azure SQL Data Warehouse como uma plataforma-alvo para migração.

  ![Janela Novo Projeto](../media/new-project.png)
  * Suporta as opções de armazenamento do Data Warehouse, conforme mostrado na imagem a seguir:

  ![opções de armazenamento para data warehouse](../media/storage-options_red.png)
  * Suporta as opções de distribuição de dados conforme mostrado na imagem a seguir:

  ![distribuição de dados para data warehouse](../media/data-distribution_red.png)

* A **opção de tempo de tempo de consulta** está agora disponível durante a descoberta de objetos de esquema na origem e no destino.

  ![opção de tempo de consulta](../media/query-timeout_red.png)

* A métrica de qualidade e conversão foi melhorada com correções direcionadas, com base no feedback do cliente.

> [!IMPORTANT]
> .NET 4.5.2 é um pré-requisito para instalar o SSMA v7.4. Além disso, começando com o v7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>SSMA v7.3

A versão v7.3 do SSMA para Oracle contém as seguintes alterações:

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

A versão v7.2 do SSMA para Oracle contém as seguintes alterações:

* Melhor qualidade e métrica de conversão com correções direcionadas com base no feedback do cliente.
* Melhorias na telemetria para fornecer melhores pontos de dados para solucionar problemas dos clientes e melhorar as taxas de conversão da SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

A versão v7.1 do SSMA para Oracle contém as seguintes alterações:

* O SQL Server 2017 no Windows e linux CTP1 é agora uma plataforma-alvo suportada para migração. Esse recurso está na pré-visualização técnica e permite que o esquema e a movimentação de dados direcionem os servidores SQL.
* O SSMA agora suporta atualizações automáticas para baixar a versão mais recente do SSMA assim que estiver disponível.
* Binários instalados do SSMA agora são entregues através de arquivos de pacote do Windows Installer (.msi).

## <a name="may-2016"></a>Maio de 2016

A versão de maio de 2016 do SSMA para Oracle contém as seguintes alterações:

* Suporte adicionado ao SQL Server 2016.
* Adicionada conversão de tabelas de arquivo de flashback Oracle para tabelas temporais do SQL Server.

  > [!NOTE]
  > A SSMA não copia dados de histórico das tabelas oracle flashback data archive. Como resultado, os dados do histórico devem ser copiados manualmente durante o processo de migração. Além disso, enquanto o SSMA não exibir a tabela de histórico no explorador de metadados do SQL Server porque é tratada como uma tabela de sistema, você pode visualizar a tabela de histórico no SQL Server Management Studio.
  >
  > O SQL Server 2016 não oferece suporte a vários recursos do Oracle Flashback, incluindo:
  >
  >   * Consulta de transação oracle flashback
  >   * `DBMS_FLASHBACK` Pacote
  >   * Transação flashback de transação flashback
  >   * Arquivamento de dados de flashback
  >   * Tabela de flashback
  >   * Queda de flashback de flashback
  >   * Flashback do banco de dados

* Adicionada conversão da Política de VPD Oracle para objetos de política de servidor SQL (Segurança de nível de linha para Oracle).
* Diminuição do tempo de carregamento inicial para oracle.
* Melhor apare e resolver.
* Verificação do instalador removido para .NET 2.0.
* Dependência atualizada do pacote de extensão de .NET 3.5 a .NET 4.0.
* Fixo `save-project` `open-project` e comandos para console SSMA.
* Comando `securepassword` fixo para console SSMA.
* Contagem fixa de objetos para carregamento inicial.
* Corrigida conversão de tipos de dados de caracteres para Oracle.
* Bug corrigido em Configurações Globais.

## <a name="march-2016"></a>Março de 2016

A versão de pré-visualização de março de 2016 do SSMA para Oracle adicionou suporte para:

* Migração para SQL Server 2016.
* Migração oracle row level security (com algumas limitações).
* Migrando o Oracle em tabelas de memória para a SQL Server Column Store.

## <a name="january-2016"></a>Janeiro de 2016

A versão de manutenção de janeiro de 2014 do SSMA para Oracle contém as seguintes alterações:

* Suporte adicionado para Índices agrupados.
* Corrigimos consultas lentas do esquema Oracle (RFC 5076207).
* Fixação de conexão ao Azure a partir do console.
* Adicionado Ver o item do menu de log ao SSMA (RFC 5706203).
* Adicionado Telemetria.

## <a name="july-2014"></a>Julho de 2014

A versão de julho de 2014 do SSMA para Oracle contém as seguintes alterações:

* Suporte adicionado ao Azure SQL DB.
* A funcionalidade do pacote de extensão mudou-se para esquema para suportar o Azure SQL DB.
* Adicionado suporte para visualizações Oracle Materializadas.
* Adicionado suporte para tabelas otimizadas de memória sql server 2014.
* Incluiu melhorias de desempenho testadas para bancos de dados com mais de 10k objetos.
* Adicionamos melhorias de IU para lidar com um grande número de objetos.
* Destaque adicionado de esquemas lob bem conhecidos.
* Incluiu melhorias na velocidade de conversão.
* Suporte adicionado para mostrar contagens de objetos em UI.
* Tamanho do relatório reduzido em mais de 25%.
* Mensagens de erro melhoradas para construções não parsed.

## <a name="april-2014"></a>Abril de 2014

A versão de abril de 2014 do SSMA para Oracle contém as seguintes alterações:

* Suporte adicionado ao MS SQL Server 2014.
* Adicionado suporte ao Oracle 12 e otimização de consulta.
* Corrigimos bugs em relação à conversão para o Azure.
* Corrigimos bugs em relação às páginas de relatórios invisíveis no IE 10.

## <a name="january-2012"></a>Janeiro de 2012

A versão de janeiro de 2012 do `RowType` SSMA para Oracle adiciona suporte e `RecordType` parâmetros de entrada padrão para `NULL`.

## <a name="july-2011"></a>julho de 2011

A versão de julho de 2011 do SSMA para Oracle contém as seguintes alterações:

* Adicionado suporte para conversão [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] de seqüência Oracle para gerador de seqüência.
* Relatórios de erros aprimorados durante a migração de dados.
* Conversão melhorada de declaração usando palavras reservadas.
* Conversão implícita melhorada do valor da data em uma função.

## <a name="april-2011"></a>abril de 2011

A versão de abril de 2011 do SSMA para Oracle contém as seguintes alterações:

* Produto consolidado "SSMA for Oracle", [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] que [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]suporta , e .
* Suporte adicional para conectar e [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]migrar para .
* Mecanismo de migração de dados do lado do cliente aprimorado, suportando migração paralela de dados.
* Melhor desempenho de `Simple` migração de dados com modelos de recuperação registrados e `Bulk` registrados.
* Adicionado suporte para compatibilidade retrógrada de projetos criados por versões anteriores do SSMA (v4.0 e v4.2).
* Adicionada a capacidade de instalar SSMA para o produto Oracle v5.0 lado a lado (SxS) com versões mais antigas do SSMA (v4.0 e v4.2).
* Adicionado suporte para reportar Tipos definidos pelo `VARRAY` `NESTED TABLE`usuário (inclui subtipo, , tabela de objetos e exibição de objeto) e seus usos em blocos PL/SQL com mensagens de erro especiais.

## <a name="july-2010"></a>Julho de 2010

A versão de julho de 2010 do SSMA para oracle acrescentou:

* Suporte para migração para o SQL Server 2008 R2.
* Um novo aplicativo ssma console para execução de linha de comando.
* Suporte para migração de dados usando mecanismos de migração de dados do lado do servidor e do lado do cliente.
* Suporte à declaração "Custom SELECT" na migração de dados.
* Suporte para migração da Oracle 11g R2.

## <a name="june-2008"></a>junho de 2008

A versão de junho de 2008 do SSMA para Oracle contém as seguintes alterações:

* Adicionamos melhorias ao Relatório de Avaliação, incluindo informações adicionais para sinônimos, fonte bruta para objetos parsáveis, painéis e remoção do logotipo do SQL Server e persistência do layout.
* Melhorias adicionadas na conversão de objetos:
  * `DBMS_LOB`Pacotes, `DBMS_SQL` conversão adicionada.
  * Junta a conversão revisada.
  * Modificação de coleções e conversão de registros, agora conversão de registros em casos simples liberados via variáveis separadas para cada campo.
  * Melhorias na implementação de registros e coleções.
  * Funções de agregação de janelas adicionadas.
  * `ROLLUP`/`CUBE`cláusula adicionada.
  * Melhoria `NEXTVAL` / `CURVAL`para .
  * Foram adicionados `SET` agrupamento de colunas em cláusula, conjuntos de agrupamento e ID de agrupamento.
  * `MERGE`declaração acrescentou.
  * Suporte a novos tipos de data-hora e conversão de registros e coleções conforme os tipos de dados CLR adicionados.
* Adicionado novos recursos do Tester. As tabelas agora podem ser testadas como objetos usando o Tester, uma ordem de chamada de vários objetos testados no caso de teste pode ser alterada, o usuário pode testar procedimentos e funções com registros e coleções como parâmetros e valores de retorno, e um analisador de dependências foi adicionado para verificar apenas tabelas usadas.
  
## <a name="august-2007"></a>agosto de 2007

A versão de agosto de 2007 do SSMA para oracle acrescentou:

* Um novo componente tester permite criar, gerenciar e executar casos de teste para verificar o código SQL convertido.
* O suporte para conversão de subtipos Oracle, coleções e módulos locais foi adicionado ao conversor SQL.
* Um novo recurso de sincronização permite sincronizar objetos específicos com o banco de dados SQL Server.
* Novas opções de conversão.
  
## <a name="april-2007"></a>abril de 2007

O lançamento em abril de 2007 do SSMA para oracle foi o lançamento inicial.
