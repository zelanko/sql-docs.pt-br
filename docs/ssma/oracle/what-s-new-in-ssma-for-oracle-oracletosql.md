---
title: Quais são as novidades do SSMA para Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 06/11/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 20fc72ce649d8ab66c43fe1c8f3a87775d83f9fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086781"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>Quais são as novidades do SSMA para Oracle (OracleToSQL)
Este artigo lista os SQL Server Migration Assistant (SSMA) para que as alterações do Oracle em cada versão.

## <a name="ssma-v82"></a>SSMA v8.2

A versão v 8.2 do SSMA para Oracle é aprimorada para:

* Adicione suporte para DBMS_OUTPUT. HABILITAR/DESABILITAR.
* Remover CONVERSÃO como FLOAT para as colunas BINARY_FLOAT e BINARY_DOUBLE em default consulta de migração de dados.
* Corrija as sequências de atualização se o valor atual é alterado.
* Correção de bug relacionada a interpretação errônea de pseudo colunas (ROWNUM, etc.) se existe uma coluna com o mesmo nome.
* Corrigi uma falha que ocorre a conversão para loops com o identificador não resolvido ambíguo.

Além disso, esta versão inclui um conjunto direcionado de correções projetadas para melhorar a qualidade e métricas de conversão, bem como correções para:

* Um problema com os índices não clusterizados desabilitados após a migração de dados.
* Detecção do .NET Framework durante a instalação silenciosa.
* Uma falha de intermitente que ocorre quando uma nova versão é baixada.

> [!NOTE]
> Um problema conhecido com a atualização automática pode fazer com que a falha de uma atualização do SSMA v8.1 v 8.2. Se você encontrar esse erro, baixe a nova versão e instalá-lo manualmente.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v81"></a>SSMA v8.1

A versão 8.1 do SSMA para Oracle é aprimorada com correções direcionadas são projetadas para melhorar as métricas de qualidade e a conversão.

> [!NOTE]
> Um problema conhecido com a atualização automática pode fazer com que a falha de uma atualização do SSMA v8.0 8.1. Se você encontrar esse erro, baixe a nova versão e instalá-lo manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

A versão v 8.0 do SSMA para Oracle é aprimorada com correções direcionadas projetadas para melhorar a qualidade e a conversão de métricas. Esta versão também oferece os seguintes recursos novos:

* Suporte para **banco de dados de instância gerenciada do SQL** como um destino. Agora você pode criar novos projetos direcionados ao banco de dados de instância gerenciada do SQL:

  ![Projeto de banco de dados SQL para a MI](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > O SSMA para Oracle extensão Pack também foi atualizado para permitir instalações remotas no banco de dados de instância gerenciada do SQL:
  >
  > ![SSMA para o pacote de extensão do Oracle](../media/ssma-oracle-ext-pack.png)

  Alguns recursos, incluindo migração de dados do testador e do lado do servidor, não têm suporte durante o direcionamento para o banco de dados de instância gerenciada do SQL. Leia mais sobre isso [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/).

* Após a conversão **correção advisor**. Saiba mais sobre ele [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Seleção de banco de dados ou o esquema preliminar.

  Ao se conectar à fonte, o usuário pode agora selecionar bancos de dados/esquemas de interesse. Selecionando apenas os esquemas que você planeja migrar economizar tempo durante a conexão inicial e melhorar o desempenho geral do SSMA.

  ![Objetos de filtro do SSMA](../media/ssma-filter-objects.png)

* A capacidade de usar o driver do NET oficial e gerenciado para se conectar ao Oracle. O driver do OCI não é um pré-requisito para usar o Assistente de migração do SQL Server para Oracle.

* A capacidade de mapear o ROWID e UROWID para VARCHAR por padrão. Alterado de 'uniqueidentifier' para acomodar a migração de dados para colunas ROWID explícitas.

## <a name="ssma-v710"></a>SSMA v7.10

A versão de v7.10 do SSMA para Oracle contém as seguintes alterações:

* Correções direcionadas projetadas para fornecer segurança adicional e proteções de privacidade para atender às mudanças nos requisitos de globais.
* Uma melhoria de conversão relacionada a consultas hierárquicas.

## <a name="ssma-v79"></a>SSMA v7.9

A versão de v7.9 do SSMA para Oracle contém as seguintes alterações:

* Correções de destino que melhoram as métricas de qualidade e a conversão.
* Suporte para instruções de "Continue" Migrando do Oracle para o SQL Server.
* Suporte a linha de comando do SSMA para alterar o mapeamento de tipo de dados e preferências de projeto.
* Suporte para a migração de dados usando o SQL Server Integration Services (SSIS). Depois de converter o esquema, é possível criar um pacote do SSIS por meio de uma opção de menu de contexto do botão direito do mouse.
* A caixa de diálogo de conexão de banco de dados SQL do SSMA também foi alterada para especificar o nome totalmente qualificado do servidor. Em versões anteriores do SSMA, o prefixo de banco de dados SQL precisava ser mencionado explicitamente dentro de configurações de projetos.

## <a name="ssma-v78"></a>SSMA v7.8

A versão de v 7.8 do SSMA para Oracle contém as seguintes alterações:

* Suporte para:
  * Expressão de linha para a cláusula IN.
  * Conversões de tipo implícito.
  * Conversão de UID para o banco de dados SQL.
* Alterar o mapeamento de tipo realçado nas configurações do projeto.
* A capacidade dos usuários desabilitar a telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

A versão de v7.7 do SSMA para Oracle contém as seguintes alterações:

* O SSMA para Oracle foi aprimorado com correções direcionadas que melhoram as métricas de qualidade e a conversão.
* A versão de 32 bits do SSMA para Oracle com base na demanda popular, está de volta. Em comparação com a implementação anterior (antes da v 7.4), há dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base em componentes de conectividade, que você tem. É sempre preferível usar a versão de 64 bits, se possível.
* Suporte do SQL Server 2017 agora é oficial com a extensão do pacote Oracle também suporte no Linux (nova opção de instalação remota). Observe que a funcionalidade do pacote de extensão é limitada quando instalado no Linux, como o testador e não há suporte para recursos de migração de dados do servidor.
* O SSMA para Oracle permite que você migre Exibições materializadas como tabelas regulares (configurável por meio das configurações no **configurações do projeto** -> **sincronização**  ->  **Descobrir tabelas de backup para os modos de exibição materializada**).

## <a name="ssma-v76"></a>SSMA v7.6

A versão de v7.6 do SSMA para Oracle é aprimorada com correções direcionadas que melhoram as métricas de qualidade e a conversão e com suporte para SQL Server 2017 (visualização pública). Suporte para SQL Server 2017 no Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

## <a name="ssma-v75"></a>SSMA v7.5

A versão de v 7.5 do SSMA para Oracle contém as seguintes alterações:

* Aprimorado com vários aprimoramentos para garantir que a maior acessibilidade para pessoas com deficiências.
* Atualizado para melhorar a métrica de qualidade e a conversão com correções direcionadas, como a melhoria no tratamento dos tipos de dados de data e float durante a migração de dados, com base nos comentários dos clientes.

## <a name="ssma-v74"></a>SSMA v7.4

A versão de v 7.4 do SSMA para Oracle contém as seguintes alterações:

* O SSMA para Oracle agora oferece suporte a SQL Data Warehouse do Azure como uma plataforma de destino para migração.

  ![Janela novo projeto](../media/new-project.png)
  * Suporta as opções de armazenamento do Data Warehouse, conforme mostrado na imagem a seguir:

  ![Opções de armazenamento para o data warehouse](../media/storage-options_red.png)
  * Suporta as opções de distribuição de dados conforme mostrado na imagem a seguir:

  ![distribuição de dados para o data warehouse](../media/data-distribution_red.png)

* O **tempo limite da consulta** opção agora está disponível durante a descoberta de objeto de esquema na origem e destino.

  ![opção de tempo limite de consulta](../media/query-timeout_red.png)

* A métrica de qualidade e a conversão foi aprimorada com correções direcionadas, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito para a instalação v SSMA 7.4. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>SSMA v7.3

A versão 7.3 do SSMA para Oracle contém as seguintes alterações:

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

A versão de v7.2 do SSMA para Oracle contém as seguintes alterações:

* Métrica de qualidade e a conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
* Aprimoramentos de telemetria para fornecer melhor pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

A versão de v7.1 do SSMA para Oracle contém as seguintes alterações:

* Agora, o SQL Server 2017 no Windows e Linux CTP1 é uma plataforma de destino com suporte para a migração. Esse recurso está na visualização técnica e permite a movimentação de dados e esquema para servidores de SQL de destino.
* Agora, o SSMA dá suporte a atualizações automáticas para baixar a versão mais recente do SSMA assim que ele está disponível.
* Agora, os binários instaláveis do SSMA são entregues por meio de arquivos de pacote do Windows installer (. msi).

## <a name="may-2016"></a>Maio de 2016

A versão de maio de 2016 do SSMA para Oracle contém as seguintes alterações:  

* Adicionado suporte para SQL Server 2016.
* Conversão das tabelas de arquivo morto do Oracle flashback adicionado às tabelas temporais do SQL Server.

  > [!NOTE]
  > O SSMA não copia dados de histórico de tabelas de arquivo morto de dados do Oracle Flashback. Como resultado, os dados de histórico devem ser copiados manualmente durante o processo de migração. Além disso, enquanto o SSMA não exibe a tabela de histórico no Gerenciador de metadados do SQL Server porque ela é tratada como uma tabela do sistema, você pode exibir a tabela de histórico no SQL Server Management Studio.
  >
  > SQL Server 2016 não dá suporte a vários recursos do Oracle Flashback, incluindo:
  >
  > * Consulta de transação do Oracle Flashback
  > * Pacote DBMS_FLASHBACK
  > * Transação de Flashback
  > * Arquivo morto de dados de Flashback
  > * Tabela de Flashback
  > * Soltar Flashback
  > * Banco de dados de Flashback
* Conversão da política de VPD do Oracle adicionado aos objetos de política do SQL Server (segurança em nível de linha para Oracle).
* Reduzido o tempo de carregamento inicial para Oracle.
* Analisador aprimorado e o resolvedor.
* Removida a verificação de instalador para .net 2.0.
* Dependência do pacote de extensão atualizada do .net 3.5 para o .net 4.0.
* Corrigido "salvar o projeto" e "Abrir projeto" comandos para o Console do SSMA.
* Corrigido o comando "securepassword" para o Console do SSMA.
* Correção de contagem de objetos para o carregamento inicial.
* Corrigida a conversão dos tipos de dados de caractere para Oracle.
* Corrigido o bug nas configurações globais.
  
## <a name="march-2016"></a>Março de 2016

A versão de preview de março de 2016 do SSMA para Oracle adicionou suporte para:  
  
* Migração para o SQL Server 2016.  
* Migrando Oracle nível de segurança de linha (com algumas limitações).  
* Migrando do Oracle em tabelas de memória para o SQL Server coluna Store.  
  
## <a name="january-2016"></a>Janeiro de 2016

Janeiro de 2014 versão de manutenção do SSMA para Oracle contém as seguintes alterações:  
  
* Adicionado suporte para índices clusterizados.  
* Correção de consultas de esquema lentas Oracle (RFC 5076207).  
* Fixo se conectar ao Azure no console do.  
* Item de Menu exibição adicionado Log para o SSMA (RFC 5706203). 
* Adicionada a telemetria.
  
## <a name="july-2014"></a>Julho de 2014

A versão de julho de 2014 do SSMA para Oracle contém as seguintes alterações:  
  
* Adicionado suporte para o BD SQL do Azure.
* Funcionalidade do pacote de extensão é movido para o esquema para dar suporte ao BD SQL do Azure.
* Adicionado suporte para modos de exibição materializada Oracle.  
* Tabelas com otimização de adição de suporte para a memória do SQL Server 2014.  
* Melhorias de desempenho incluídos testadas para bancos de dados com mais de 10 mil objetos.  
* Foram incluídos aperfeiçoamentos de interface do usuário para lidar com um grande número de objetos.  
* Adicionado o realce de esquemas LOB "conhecidas".  
* Melhorias de velocidade de conversão incluído.  
* Suporte adicionado para mostrar o objeto de conta na interface do usuário.  
* Tamanho do relatório reduzida em mais de 25%.
* Mensagens de erro aprimoradas para construções não analisadas.  
  
## <a name="april-2014"></a>Abril de 2014

A versão de abril de 2014 do SSMA para Oracle contém as seguintes alterações:  
  
* Adicionado suporte do MS SQL Server 2014.  
* Adicionado suporte de otimização do Oracle de 12 e consulta.  
* Bugs corrigidos em relação à conversão para o Azure.  
* Bugs corrigidos em relação à páginas de relatório invisível no IE 10.  
  
## <a name="january-2012"></a>Janeiro de 2012

A versão de janeiro de 2012 do SSMA para Oracle adiciona suporte para RowType e parâmetros de entrada RecordType adotou o padrão NULL.  
  
## <a name="july-2011"></a>Julho de 2011

A versão de julho de 2011 do SSMA para Oracle contém as seguintes alterações:  
  
* Adicionado suporte para conversão de sequência do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerador de sequência do "Denali".
* Aprimorado relatórios de erros durante a migração de dados.  
* Conversão aprimorada da instrução usar palavras reservadas.  
* Melhor conversão implícita do valor de data em uma função.  
  
## <a name="april-2011"></a>Abril de 2011

A versão de abril de 2011 do SSMA para Oracle contém as seguintes alterações:  
  
* Produto "SSMA para Oracle" consolidado, o que dá suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".
* Adicionado suporte para se conectar e migrar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
* Mecanismo de migração aprimorada de dados do cliente, que dão suporte a migração paralela de dados.  
* Desempenho de migração de dados aprimorada com simples e Bulk logged modelos de recuperação.  
* Adicionado suporte para compatibilidade com versões anteriores de projetos criados por versões anteriores do SSMA (v4.0 e v4.2).  
* Adicionada a capacidade de instalar o SSMA para Oracle v5.0 produto lado a lado (SxS) com as versões mais antigas do SSMA (v4.0 e v4.2).
* Adicionado suporte para tipos definidos pelo usuário (inclui o subtipo, VARRAY, tabela ANINHADA, tabela de objetos e modo de exibição do objeto) e seus usos em blocos de PL/SQL com mensagens de erro especial de relatório.  

## <a name="july-2010"></a>Julho de 2010

A versão de julho de 2010 do SSMA para Oracle adicionado:

* Suporte para migração para o SQL Server 2008 R2.  
* Um novo aplicativo de Console do SSMA para execução de linha de comando.  
* Suporte para migração de dados usando mecanismos de migração de dados do lado do cliente e do servidor.  
* Suporte para a instrução "SELECT personalizada" na migração de dados.  
* Suporte à migração do Oracle 11g R2.  
  
## <a name="june-2008"></a>Junho de 2008

A versão de junho de 2008 do SSMA para Oracle contém as seguintes alterações:  
  
* Foram incluídos aperfeiçoamentos para o relatório de avaliação, incluindo informações adicionais sobre sinônimos, origem bruta de objetos analisável, painéis e remoção de logotipo do SQL Server e persistência de layout.  
* Foram incluídos aperfeiçoamentos na conversão do objeto:  
  * Pacotes DBMS_LOB, conversão de DBMS_SQL adicionado.  
  * Une conversão revisado.  
  * Modificação de conversão de coleções e registros, agora a conversão de registros em casos simples lançados por meio de variáveis separadas para cada campo.  
  * Melhorias da implementação de registros e coleções.  
  * Funções de agregação em janela adicionadas.  
  * Cláusula ROLLUP/cubo adicionada.  
  * Melhoria para NEXTVAL/CURVAL.  
  * Colunas de agrupamento na cláusula SET, conjuntos de agrupamentos e a ID de agrupamento foram adicionadas.  
  * MESCLE instrução adicionada.  
  * Suporte de novos tipos de data e hora e a conversão de registros e coleções como tipos de dados CLR adicionados.  
* Adição de novos recursos de testador. Tabelas agora podem ser testadas como objetos usando o testador, uma ordem de chamada de vários objetos que podem ser testados no caso de teste pode ser alterada, usuário pode testar procedimentos e funções com registros e coleções como parâmetros e valores de retorno e um analisador de dependências foi adicionado para verificar somente tabelas usadas.  
  
## <a name="august-2007"></a>Agosto de 2007

A versão de agosto de 2007 do SSMA para Oracle adicionado:

* Um novo componente do TESTADOR permite criar, gerenciar e executar casos de teste para verificar se o código convertido de SQL.  
* Suporte para conversão de subtipos de Oracle, coleções e módulos locais foram adicionados ao conversor SQL.  
* Um novo recurso de sincronização permite sincronizar objetos específicos com o banco de dados do SQL Server.  
* Novas opções de conversão.  
  
## <a name="april-2007"></a>Abril de 2007

A versão de abril de 2007 do SSMA para Oracle foi a versão inicial.
