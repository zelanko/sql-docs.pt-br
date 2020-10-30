---
title: O que há de novo no SSMA para DB2 (DB2ToSQL) | Microsoft Docs
description: Saiba mais sobre as alterações feitas no Assistente de Migração do SQL Server (SSMA) para DB2 (DB2ToSQL) para cada versão.
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 10/28/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
ms.author: alexiva
ms.openlocfilehash: b35e5a01f28feb8b5dd42f592cf2c310d6c410f3
ms.sourcegitcommit: 9c6130d498f1cfe11cde9f2e65c306af2fa8378d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93036022"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>O que há de novo no SSMA para DB2 (DB2ToSQL)

Este artigo lista Assistente de Migração do SQL Server (SSMA) para as alterações do DB2 em cada versão.

## <a name="ssma-v815"></a>8.15 do SSMA v

Além de várias melhorias de acessibilidade, a versão v 8.15 do SSMA para DB2 contém as seguintes alterações:

* Corrigir conversão de `MIN` / `MAX` funções de agregação com argumentos de data/hora
* Corrigir o bug na `VARCHAR_FORMAT` função de emulação quando o `DD` espaço reservado é usado
* Melhorar mapeamentos de tipo para `TIME` tipo de dados
* Melhorar a conversão `ROUND` de `TRUNC` funções e com argumentos numéricos
* Relatórios de avaliação do renovando para trabalhar em navegadores modernos
* Autoridade de uso fornecida pelo banco de dados para autenticação do Azure AD
* Melhorar a nomenclatura para instruções carregadas de arquivos

## <a name="ssma-v814"></a>8.14 do SSMA v

Além de várias melhorias para garantir maior acessibilidade para pessoas com deficiências, a versão v 8.14 do SSMA para DB2 requer uma atualização de projeto, pois agora armazena a versão completa do servidor de origem/destino nos metadados do projeto.

## <a name="ssma-v813"></a>8.13 do SSMA v

A versão v 8.13 do SSMA para DB2 contém as seguintes alterações:

* Suporte para índices exclusivos filtrados
* Considere as conversões implícitas de tipo ao converter o procedimento e as chamadas de função
* Melhorar o log da cadeia de conexão de origem para ajudar a solucionar problemas de conexão

## <a name="ssma-v812"></a>SSMA v 8.12

A versão v 8.12 do SSMA para DB2 contém as seguintes alterações:

* Conversão da `STRIP` função
* Análise aprimorada das opções de procedimento

## <a name="ssma-v811"></a>8.11 do SSMA v

A versão v 8.11 do SSMA para DB2 contém as seguintes alterações:

* Suporte para DB2 para i (v 7.1 e superior)
* Tradução de `SQLSTATE` e `SQLCODE`
* Mensagem de erro de conversão para operadores de efeito colateral em uma função
* Usar a biblioteca MSAL.NET para autenticação de Azure Active Directory interativa

## <a name="ssma-v810"></a>SSMA v 8.10

A versão v 8.10 do SSMA para DB2 aborda uma regressão na descoberta de chaves estrangeiras e contém melhorias de desempenho secundárias.

## <a name="ssma-v89"></a>8.9 do SSMA v

A versão v 8.9 do SSMA para DB2 contém as seguintes alterações:

* Correção para conversão da `TIMESTAMPDIFF` função
* Correção para a descoberta de índices quando o índice particionado estiver presente
* Correção da descoberta de chaves estrangeiras quando o índice primário é definido em outro esquema
* Conversão aprimorada para colunas que correspondem a nomes de funções internas
* Correção do problema com caracteres especiais no nome do projeto

## <a name="ssma-v88"></a>8.8 do SSMA v

A versão v 8.8 do SSMA para DB2 inclui:

* Melhorias na estabilidade da sincronização de objetos do SQL Server
* Melhorias de desempenho de GUI durante a avaliação e conversão
* Mapeamento atualizado de `ROWID` para `varbinary(40)` para facilitar a migração de dados
* Conversão aprimorada de `SELECT ... FROM NEW/OLD TABLE` instruções
* Nova conversão de `ALTER` instruções para procedimentos e funções
* Nova conversão de atribuições de desestruturação

## <a name="ssma-v87"></a>SSMA v 8.7

A versão v 8.7 do SSMA para DB2 inclui um analisador de sintaxe DB2 totalmente novo, bem como correções secundárias e melhorias de desempenho na interface gráfica do usuário.

Além disso, o SSMA para DB2 agora fornece:

* Uma correção para a descoberta de chaves estrangeiras ao migrar do DB2 no LUW.
* Conversão aprimorada da `SELECT ... FOR UPDATE` instrução.
* Conversão aprimorada para a `COUNT` função em tabelas do MQ.
* Conversão de `SAVEPOINT` instruções.
* Conversão para emular o comportamento de DB2's para `NULL` os valores na `ORDER BY` cláusula.
* Suporte de análise para a `ASSOCIATE RESULT SET` instrução.

> [!IMPORTANT]
> Com o SSMA v 8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se precisar instalar essa versão, você poderá baixar o arquivo de tempo de execução [aqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v 8.6

Além de um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho, a versão do v 8.6 do SSMA para DB2 foi aprimorada com a adição de uma configuração que permite aos usuários omitir as propriedades estendidas do SSMA no código convertido.

Para aproveitar essa configuração, no SSMA para DB2, navegue até **ferramentas**  >  **configurações do projeto**  >  **General**  >  **conversão** geral e **, em** seguida, atualize o valor da configuração **omitir propriedades estendidas** para **Sim** .

![Omitir a configuração de propriedades estendidas](../db2/media/ssma-omit-extended-properties.png)

Além disso, o SSMA para DB2 agora fornece:

* Uma correção para a conversão de funções que usam valores de argumento padrão.
* Análise aprimorada da `PARAMETER` cláusula para funções.
* A capacidade de converter a `LEAVE` instrução.

> [!IMPORTANT]
> Com o SSMA v 8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se precisar instalar essa versão, você poderá baixar o arquivo de tempo de execução [aqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v 8.5

A versão v 8.5 do SSMA para DB2 foi aprimorada com suporte para autenticação Azure Active Directory e suporte básico para recursos JSON no SQL Server, junto com um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho.

Além disso, o SSMA para DB2 foi aprimorado com:

* Suporte para adição de conversão para `GET DIAGNOSTICS` a instrução com `ROW_NUMBER` .
* Uma correção para um bug relacionado a espaços no início do nome do objeto não está sendo respeitado.

> [!IMPORTANT]
> Com o SSMA v 8.5, o .NET 4.7.2 é um pré-requisito de instalação. Se precisar instalar essa versão, você poderá baixar o arquivo de tempo de execução [aqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v 8.4

A versão v 8.4 do SSMA para DB2 foi aprimorada com correções direcionadas que foram projetadas para resolver problemas de acessibilidade e corrigir um bug relacionado a colunas de índice máximo (para permitir 32 em vez de 16) para SQL Server 2016 e versões posteriores.

> [!IMPORTANT]
> Com o SSMA versões 7,4, embora 8,4, o .NET 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v83"></a>SSMA v 8.3

A versão v 8.3 do SSMA para DB2 foi aprimorada com correções direcionadas que foram projetadas para melhorar a qualidade e a conversão de métricas. Além disso, esta versão do SSMA para DB2 fornece correções que:

* Solucionar problemas de acessibilidade.
* Adicione suporte básico para o `hierarchyid` tipo em SQL Server.
* Substitua o uso da função TRIM em consultas de descoberta de z/OS por `RTRIM` / `LTRIM` .
* Permitir que o usuário especifique a coleção de pacotes ao se conectar no ' modo padrão ' (o padrão é `NULLID` ).
* Adicione conversão para `CREATE TABLE AS SELECT` .
* Melhorar conversões para tabelas temporárias globais.
* Resolva um problema com a ordem de verificação de exclusividade do objeto para priorizar tabelas sobre restrições, se os nomes colidirem.
* Resolva um problema com o carregamento de valores de coluna padrão para `DATE` e `TIMESTAMP` para z/os.
* Suporte ao caractere de alimentação de linha Unicode (também conhecido como `NEL` ).
* Resolva um problema com a conversão de cursor com a `RETURN TO` cláusula Missing.
* Adicione suporte para rótulos e `GOTO` .

## <a name="ssma-v82"></a>SSMA v 8.2

A versão v 8.2 do SSMA para DB2 é aprimorada com o para resolver problemas com conexões com o banco de dados SQL do Azure da ferramenta do console do SSMA e a coluna COUNT_BIG ausente na declaração views durante a conversão. Além disso, essa versão inclui um conjunto direcionado de correções projetadas para melhorar a qualidade e a conversão de métricas, bem como correções para:

* Um problema com índices não clusterizados desabilitados após a migração de dados.
* Detecção de .NET Framework durante a instalação silenciosa.
* Uma falha intermitente que ocorre quando uma nova versão é baixada.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v 8.1 para v 8.2. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v81"></a>SSMA v 8.1

A versão v 8.1 do SSMA para DB2 é aprimorada para fornecer correções direcionadas que foram projetadas para melhorar a qualidade e a conversão de métricas.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v 8.0 para o v 8.1. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v80"></a>SSMA v 8.0

A versão v 8.0 do SSMA para DB2 é aprimorada para fornecer correções direcionadas projetadas para melhorar a qualidade e a conversão de métricas. Esta versão também oferece os seguintes novos recursos:

* Suporte para o **Azure SQL instância gerenciada** como um destino. Agora você pode criar novos projetos destinados ao Azure SQL Instância Gerenciada:

  ![Projeto do SQL MI](../media/ssma-newproject-sqldbmi.png)

* **Supervisor de correção** após a conversão. Saiba mais sobre isso [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Seleção preliminar de banco de dados/esquema.

  Ao se conectar à fonte, o usuário agora pode selecionar bancos de dados/esquemas de interesse. Selecionar somente os esquemas que você planeja migrar economizará tempo durante a conexão inicial e melhorará o desempenho geral do SSMA.

  ![Objetos de filtro do SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>7.10 do SSMA v

A versão v 7.10 do SSMA para DB2 contém as seguintes alterações:

* Correções direcionadas projetadas para fornecer segurança adicional e proteções de privacidade para atender às alterações nos requisitos globais.
* Uma correção para a conversão de `BEGIN-END` blocos.

## <a name="ssma-v79"></a>7.9 do SSMA v

A versão v 7.9 do SSMA para DB2 contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Suporte na linha de comando do SSMA para alterar o mapeamento de tipo de dados e as preferências do projeto.
* Suporte para migrar dados usando SQL Server Integration Services (SSIS). Depois de converter o esquema, é possível criar um pacote do SSIS usando uma opção de menu de contexto de clique com o botão direito do mouse.
* A caixa de diálogo conexão do banco de dados SQL do Azure no SSMA também foi alterada para especificar o nome do servidor totalmente qualificado. Nas versões anteriores do SSMA, o prefixo do banco de dados SQL do Azure tinha que ser explicitamente mencionado dentro das configurações de projetos.

## <a name="ssma-v78"></a>SSMA v 7.8

A versão v 7.8 do SSMA para DB2 contém as seguintes alterações:

* Alterar o mapeamento de tipo realçado nas *configurações do projeto* .
* A capacidade dos usuários de desabilitar a telemetria.

## <a name="ssma-v77"></a>7.7 do SSMA v

A versão v 7.7 do SSMA para DB2 contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Com base na demanda popular, a versão de 32 bits do SSMA para DB2 está de volta. Em comparação com a implementação anterior (antes da v 7.4), há dois pacotes do instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base nos componentes de conectividade que tem. É sempre preferível usar a versão de 64 bits, se possível.

## <a name="ssma-v76"></a>SSMA v 7.6

A versão v 7.6 do SSMA para DB2 foi aprimorada com correções direcionadas que melhoram as métricas de qualidade e conversão e com suporte para SQL Server 2017 (visualização pública). O suporte para SQL Server 2017 no Windows e no Linux está em visualização pública e não deve ser usado para migrações de produção.

## <a name="ssma-v75"></a>SSMA v 7.5

A versão v 7.5 do SSMA para DB2 é aprimorada com várias melhorias para garantir maior acessibilidade para pessoas com deficiências.

## <a name="ssma-v74"></a>SSMA v 7.4

A versão v 7.4 do SSMA para DB2 contém as seguintes alterações:

* A opção de **tempo limite de consulta** agora está disponível durante a descoberta de objeto de esquema na origem e no destino.

  ![opção de tempo limite de consulta](../media/query-timeout_red.png)

* A métrica de qualidade e conversão foi aprimorada com correções direcionadas, com base nos comentários dos clientes.

  > [!IMPORTANT]
  > O .NET 4.5.2 é um pré-requisito para a instalação do SSMA v 7.4. Além disso, a partir da v 7.4, a versão de 32 bits do SSMA foi descontinuada.

## <a name="ssma-v73"></a>SSMA v 7.3

A versão v 7.3 do SSMA para DB2 contém as seguintes alterações:

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

A versão v 7.2 do SSMA para DB2 contém as seguintes alterações:

* Métrica de qualidade e conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
* Aprimoramentos de telemetria para fornecer melhores pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>SSMA v 7.1

A versão v 7.1 do SSMA para DB2 contém as seguintes alterações:

* SQL Server 2017 no Windows e Linux CTP1 agora é uma plataforma de destino com suporte para migração. Esse recurso está em visualização técnica e permite a movimentação de esquema e dados para servidores SQL de destino.
* Suporte para atualizações automáticas para baixar a versão mais recente do SSMA assim que ela estiver disponível.
* Os binários instaláveis do SSMA agora são entregues por meio de arquivos de pacote Windows Installer (. msi).

## <a name="may-2016"></a>Maio de 2016

A versão de maio de 2016 do SSMA para DB2 contém as seguintes alterações:

* Adicionado suporte para SQL Server 2016.
* Adição de conversão de tabelas de DB2 na memória e regulares para SQL Server recursos na memória e hekaton.
* Adição de conversão de controles de acesso do DB2 a objetos de política de SQL Server (Segurança em Nível de Linha para DB2).
* Adicionada a conversão de tabelas de versão do sistema do DB2 para SQL Server tabelas temporais.
* Analisador e resolvedor do DB2 aprimorados.
* Verificação do instalador removida para .NET 2,0.
* Removido \* . dll desnecessário do instalador do DB2.
* Corrigidos `save-project` e `open-project` comandos para o console do SSMA.
* `securepassword`Comando fixo para o console do SSMA.
* Contagem fixa de objetos para carregamento inicial.
* Corrigido o bug nas configurações globais.
  
## <a name="march-2016"></a>Março de 2016

A versão de visualização de março de 2016 do SSMA para DB2 adiciona suporte para migração para o SQL Server 2016.

## <a name="january-2016"></a>Janeiro de 2016

A versão de manutenção de janeiro de 2016 do SSMA para DB2 contém as seguintes alterações:
  
* Suporte adicionado para várias funções padrão.
* Corrigidos os erros do analisador do DB2.
* Corrigido o suporte do zOS do DB2 v9 (RFC 5690920).
* Correção de erros de identificador não resolvidos do DB2 durante a conversão.
* Item de menu Exibir log adicionado ao SSMA (RFC 5706203).
* Telemetria adicionada.
  
## <a name="november-2014"></a>Novembro de 2014

A versão de novembro de 2014 do SSMA para DB2 foi a versão inicial.
