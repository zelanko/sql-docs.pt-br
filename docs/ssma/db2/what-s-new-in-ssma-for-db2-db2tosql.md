---
title: O que há de novo no SSMA para DB2 (DB2ToSQL) | Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
ms.author: jtoland;alexiva
ms.openlocfilehash: 53a159627750a5ec66b5aa0b3fd6510c647e26a5
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625519"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>O que há de novo no SSMA para DB2 (DB2ToSQL)

Este artigo lista o SQL Server Migration Assistant (SSMA) para alterações de DB2 em cada versão.

## <a name="ssma-v88"></a>SSMA v8.8

A versão v8.8 do SSMA para DB2 inclui:

* Melhorias na estabilidade da sincronização de objetos sql
* Melhorias no desempenho da GUI durante a avaliação e conversão
* Mapeamento atualizado `ROWID` `varbinary(40)` para facilitar a migração de dados
* Conversão melhorada `SELECT ... FROM NEW/OLD TABLE` de declarações
* Nova conversão `ALTER` de declarações para procedimentos e funções
* Nova conversão de atribuições de desestruturação

## <a name="ssma-v87"></a>SSMA v8.7

A versão v8.7 do SSMA para DB2 inclui um novo analisador de sintaxe DB2, bem como pequenas correções e melhorias de desempenho na interface gráfica do usuário.

Além disso, o SSMA para DB2 agora fornece:

* Uma correção para a descoberta de chaves estrangeiras ao migrar de DB2 em LUW.
* Conversão melhorada `SELECT ... FOR UPDATE` de declaração.
* Conversão melhorada `COUNT` para função em tabelas MQ.
* Conversão `SAVEPOINT` de declarações.
* Conversão para emular o `NULL` comportamento `ORDER BY` do DB2 para valores na cláusula.
* Suporte de análise para declaração DO CONJUNTO DE RESULTADOS ASSOCIADOS.

> [!IMPORTANT]
> Com o SSMA v8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v8.6

Além de um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho, a versão v8.6 do SSMA para DB2 foi aprimorada adicionando uma configuração que permite que os usuários omitam propriedades estendidas ssma no código convertido.

Para aproveitar essa configuração, no SSMA para DB2, navegue até as**configurações** > gerais do projeto **de ferramentas** > **conversão****geral** > e, em seguida, em **Misc,** atualize o valor da configuração **Propriedades Estendidas omita** para **Sim**.

![Omita configuração de propriedades estendidas](../db2/media/ssma-omit-extended-properties.png)

Além disso, o SSMA para DB2 agora fornece:

* Uma correção para conversão de funções que usam valores de argumento padrão.
* Análise melhorada da `PARAMETER` cláusula para funções.
* A capacidade de `LEAVE` converter a declaração.

> [!IMPORTANT]
> Com o SSMA v8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v8.5

A versão v8.5 do SSMA para DB2 é aprimorada com suporte para autenticação do Azure Active Directory e suporte básico para recursos JSON no servidor SQL, juntamente com um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho.

Além disso, o SSMA para DB2 foi aprimorado com:

* Suporte para adicionar `GET DIAGNOSTICS` conversão `ROW_NUMBER`para declaração com .
* Uma correção para um bug relacionado a espaços no início do nome do objeto não sendo respeitado.

> [!IMPORTANT]
> Com o SSMA v8.5, .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v8.4

A versão v8.4 do SSMA para DB2 é aprimorada com correções direcionadas que são projetadas para resolver problemas de acessibilidade e corrigir um bug relacionado às colunas de índice max (para permitir 32 em vez de 16) para as versões SQL Server 2016 e posteriores.

> [!IMPORTANT]
> Com as versões SSMA 7.4 embora 8.4, .NET 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v83"></a>SSMA v8.3

A versão v8.3 do SSMA para DB2 é aprimorada com correções direcionadas que são projetadas para melhorar as métricas de qualidade e conversão. Além disso, esta versão do SSMA para DB2 fornece correções que:

* Abordar problemas de acessibilidade.
* Adicione suporte `hierarchyid` básico para o tipo no SQL Server.
* Substitua o uso da função TRIM `RTRIM` / `LTRIM`em consultas de detecção z/OS por .
* Permitir que o usuário especifique a coleção do `NULLID`pacote ao se conectar no 'modo padrão' (padrão a ).
* Adicionar conversão `CREATE TABLE AS SELECT`para .
* Melhore as conversões para tabelas temporárias globais.
* Resolva um problema com a ordem de verificação de exclusividade do objeto para priorizar tabelas sobre restrições, caso os nomes colidam.
* Resolva um problema com o `DATE` `TIMESTAMP` carregamento de valores de coluna padrão para e para z/OS.
* Suporte ao caractere de alimentação `NEL`da linha Unicode (também conhecido como ).
* Resolva um problema com `RETURN TO` conversão do cursor com cláusula ausente.
* Adicione suporte para `GOTO`rótulos e .

## <a name="ssma-v82"></a>SSMA v8.2

A versão v8.2 do SSMA para DB2 é aprimorada para resolver problemas com conexões ao Banco de Dados SQL Do Azure sql da ferramenta de console SSMA e faltando COUNT_BIG coluna na declaração de visualizações durante a conversão. Além disso, esta versão inclui um conjunto direcionado de correções projetadas para melhorar as métricas de qualidade e conversão, bem como correções para:

* Um problema com índices não agrupados desativados após a migração de dados.
* Detecção de .NET Framework durante a instalação silenciosa.
* Um acidente intermitente que ocorre quando uma nova versão é baixada.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v8.1 para o v8.2. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

A versão v8.1 do SSMA para DB2 é aprimorada para fornecer correções direcionadas que são projetadas para melhorar as métricas de qualidade e conversão.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v8.0 para v8.1. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

A versão v8.0 do SSMA para DB2 é aprimorada para fornecer correções direcionadas projetadas para melhorar as métricas de qualidade e conversão. Esta versão também oferece os seguintes novos recursos:

* Suporte à instância gerenciada do banco de **dados SQL do Azure** como alvo. Agora você pode criar novos projetos direcionados à instância gerenciada do banco de dados SQL do Azure:

  ![Projeto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Orientador de **correção pós-conversão**. Saiba mais sobre isso [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Base de dados preliminar/seleção de esquemas.

  Ao se conectar à fonte, o usuário agora pode selecionar bancos de dados/esquemas de interesse. Selecionar apenas os esquemas que você planeja migrar economizará tempo durante a conexão inicial e melhorará o desempenho geral do SSMA.

  ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

A versão v7.10 do SSMA para DB2 contém as seguintes alterações:

* Correções direcionadas projetadas para fornecer proteções adicionais de segurança e privacidade para atender às mudanças nos requisitos globais.
* Uma correção `BEGIN-END` para conversão de blocos.

## <a name="ssma-v79"></a>SSMA v7.9

A versão v7.9 do SSMA para DB2 contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Suporte na linha de comando SSMA para alterar mapeamento de tipo de dados e preferências de projeto.
* Suporte para migração de dados usando SSIS (SSIS Server Integration Services, serviços de integração de servidores SQL). Depois de converter o esquema, é possível criar um pacote SSIS usando uma opção de menu de contexto com o botão direito do mouse.
* A caixa de diálogo de conexão Banco de dados Azure SQL no SSMA também foi alterada para especificar o nome do servidor totalmente qualificado. Nas versões anteriores do SSMA, o prefixo do Banco de Dados SQL do Azure tinha que ser explicitamente mencionado dentro das configurações dos projetos.

## <a name="ssma-v78"></a>SSMA v7.8

A versão v7.8 do SSMA para DB2 contém as seguintes alterações:

* Alterar mapeamento de tipo destacado nas *Configurações do projeto*.
* A capacidade dos usuários de desativar a telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

A versão v7.7 do SSMA para DB2 contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Com base na demanda popular, a versão de 32 bits do SSMA para DB2 está de volta. Em comparação com a implementação anterior (anterior ao v7.4), existem dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base nos componentes de conectividade que você tem. É sempre preferível usar a versão de 64 bits, se possível.

## <a name="ssma-v76"></a>SSMA v7.6

A versão v7.6 do SSMA para DB2 é aprimorada com correções direcionadas que melhoram as métricas de qualidade e conversão e com suporte para o SQL Server 2017 (visualização pública). O suporte ao SQL Server 2017 no Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

## <a name="ssma-v75"></a>SSMA v7.5

A versão v7.5 do SSMA para DB2 é aprimorada com várias melhorias para garantir maior acessibilidade para pessoas com deficiência.

## <a name="ssma-v74"></a>SSMA v7.4

A versão v7.4 do SSMA para DB2 contém as seguintes alterações:

* A **opção de tempo de tempo de consulta** está agora disponível durante a descoberta de objetos de esquema na origem e no destino.

  ![opção de tempo de consulta](../media/query-timeout_red.png)

* A métrica de qualidade e conversão foi melhorada com correções direcionadas, com base no feedback do cliente.

  > [!IMPORTANT]
  > .NET 4.5.2 é um pré-requisito para instalar o SSMA v7.4. Além disso, começando com o v7.4, a versão de 32 bits do SSMA foi descontinuada.

## <a name="ssma-v73"></a>SSMA v7.3

A versão v7.3 do SSMA para DB2 contém as seguintes alterações:

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

A versão v7.2 do SSMA para DB2 contém as seguintes alterações:

* Melhor qualidade e métrica de conversão com correções direcionadas com base no feedback do cliente.
* Melhorias na telemetria para fornecer melhores pontos de dados para solucionar problemas dos clientes e melhorar as taxas de conversão da SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

A versão v7.1 do SSMA para DB2 contém as seguintes alterações:

* O SQL Server 2017 no Windows e linux CTP1 é agora uma plataforma-alvo suportada para migração. Esse recurso está na pré-visualização técnica e permite que o esquema e a movimentação de dados direcionem os servidores SQL.
* Suporte para atualizações automáticas para baixar a versão mais recente do SSMA assim que estiver disponível.
* Binários instalados do SSMA agora são entregues através de arquivos de pacote do Windows Installer (.msi).

## <a name="may-2016"></a>Maio de 2016

A versão de maio de 2016 do SSMA para DB2 contém as seguintes alterações:

* Suporte adicionado ao SQL Server 2016.
* Adicionada conversão de memória DB2 e tabelas regulares aos recursos de memória e hekaton do SQL Server.
* Adicionada conversão de controles de acesso DB2 para objetos da Política do Servidor SQL (Segurança de nível de linha para DB2).
* Adicionada conversão de tabelas com versão do sistema DB2 para tabelas temporais do SQL Server.
* Parser e resolver DB2 melhorados.
* Verificação do instalador removido para .NET 2.0.
* Removido \*.dll desnecessário do instalador Db2.
* Fixo `save-project` `open-project` e comandos para console SSMA.
* Comando `securepassword` fixo para console SSMA.
* Contagem fixa de objetos para carregamento inicial.
* Corrigido bug em configurações globais.
  
## <a name="march-2016"></a>Março de 2016

A versão prévia de março de 2016 do SSMA para DB2 adiciona suporte para migração para o SQL Server 2016.

## <a name="january-2016"></a>Janeiro de 2016

A versão de manutenção de janeiro de 2016 do SSMA para DB2 contém as seguintes alterações:
  
* Adicionado suporte para uma série de funções padrão.
* Erros de analisador DB2 corrigidos.
* Suporte ao DB2 v9 zOS fixo (RFC 5690920).
* Corrigimos erros de identificadores não resolvidos do DB2 durante a conversão.
* Adicionado Ver o item do menu de log ao SSMA (RFC 5706203).
* Adicionado Telemetria.
  
## <a name="november-2014"></a>Novembro de 2014

O lançamento de novembro de 2014 do SSMA para DB2 foi o lançamento inicial.
