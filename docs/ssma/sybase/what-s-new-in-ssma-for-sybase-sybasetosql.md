---
title: O que há de novo no SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
ms.author: jtoland;alexiva
ms.openlocfilehash: 7f23c7e1c676b4ade42b43cf963e0fa6956f93c6
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625594"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>O que há de novo no SSMA para SAP ASE (SybaseToSQL)

Este artigo lista as alterações do SQL Server Migration Assistant (SSMA) para SAP ASE (anteriormente SSMA for Sybase) em cada versão.

## <a name="ssma-v88"></a>SSMA v8.8

A versão v8.8 do SSMA para SAP ASE inclui:

* Melhorias na estabilidade da sincronização de objetos sql
* Melhorias no desempenho da GUI durante a avaliação e conversão
* Corrigir para o problema com caracteres ausentes em definições SQL para objetos

## <a name="ssma-v87"></a>SSMA v8.7

A versão v8.7 do SSMA para SAP ASE tem pequenas correções e melhorias de desempenho na interface gráfica do usuário.

> [!IMPORTANT]
> Com o SSMA v8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v8.6

Além de um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho, a versão v8.6 do SSMA para SAP ASE foi aprimorada adicionando uma configuração que permite que os usuários omitam propriedades estendidas sSMA no código convertido.

Para aproveitar essa configuração, no SSMA para SAP ASE, navegue até**configurações** > **gerais** > de projetos de **Tools** > **ferramentas**e, em seguida, em **Misc,** atualize o valor da configuração **Omit Extended Properties** para **Sim**.

![Omita configuração de propriedades estendidas](../sybase/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> Com o SSMA v8.5 e posterior, o .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v8.5

A versão v8.5 do SSMA para SAP ASE é aprimorada com suporte para autenticação do Azure Active Directory e suporte básico para recursos JSON no servidor SQL, juntamente com um conjunto direcionado de correções projetadas para melhorar a usabilidade e o desempenho.

Além disso, o SSMA para SAP ASE agora permite ocultar tabelas e visualizações do sistema (excluí-las da conversão).

> [!IMPORTANT]
> Com o SSMA v8.5, .NET 4.7.2 é um pré-requisito de instalação. Se você precisar instalar esta versão, você pode baixar o arquivo de tempo de execução a partir [daqui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v8.4

A versão v8.4 do SSMA para SAP ASE é aprimorada com correções direcionadas que são projetadas para resolver problemas de acessibilidade e corrigir um bug relacionado às colunas de índice max (para permitir 32 em vez de 16) para as versões SQL Server 2016 e posteriores.

> [!IMPORTANT]
> Com as versões SSMA 7.4 a 8.4, .NET 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v83"></a>SSMA v8.3

A versão v8.3 do SSMA para SAP ASE é aprimorada com correções direcionadas que são projetadas para melhorar as métricas de qualidade e conversão. Além disso, esta versão do SSMA para SAP ASE fornece correções que:

* Abordar problemas de acessibilidade
* Adicionar suporte `hierarchyid` básico para o tipo no SQL Server

## <a name="ssma-v82"></a>SSMA v8.2

A versão v8.2 do SSMA para SAP ASE é aprimorada com um conjunto direcionado de correções projetadas para melhorar as métricas de qualidade e conversão, bem como correções para:

* Um problema com índices não agrupados desativados após a migração de dados.
* Detecção de .NET Framework durante a instalação silenciosa.
* Um acidente intermitente que ocorre quando uma nova versão é baixada.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v8.1 para o v8.2. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

A versão v8.1 do SSMA para SAP ASE é aprimorada com correções direcionadas que são projetadas para melhorar as métricas de qualidade e conversão.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v8.0 para v8.1. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

A versão v8.0 do SSMA para SAP ASE é aprimorada com correções direcionadas projetadas para melhorar as métricas de qualidade e conversão. Além disso, esta versão oferece os seguintes novos recursos:

* Suporte à instância gerenciada do banco de **dados SQL do Azure** como alvo. Agora você pode criar novos projetos direcionados à instância gerenciada do banco de dados SQL do Azure:

  ![Projeto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Orientador de **correção pós-conversão**. Saiba mais sobre isso [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Base de dados preliminar/seleção de esquemas.

  Ao se conectar à fonte, o usuário agora pode selecionar bancos de dados/esquemas de interesse. Selecionar apenas os esquemas que você planeja migrar economizará tempo durante a conexão inicial e melhorará o desempenho geral do SSMA.

  ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

A versão v7.10 do SSMA para SAP ASE é aprimorada com correções direcionadas projetadas para fornecer proteções adicionais de segurança e privacidade para atender às mudanças nos requisitos globais.

## <a name="ssma-v79"></a>SSMA v7.9

A versão v7.9 do SSMA para SAP ASE contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Suporte na linha de comando SSMA para alterar mapeamento de tipo de dados e preferências de projeto.
* Suporte para migração de dados usando SSIS (SSIS Server Integration Services, serviços de integração de servidores SQL). Depois de converter o esquema, é possível criar um pacote SSIS usando uma opção de menu de contexto com o botão direito do mouse.
* A caixa de diálogo de conexão Banco de dados Azure SQL no SSMA também foi alterada para especificar o nome do servidor totalmente qualificado. Nas versões anteriores do SSMA, o prefixo do Banco de Dados SQL do Azure tinha que ser explicitamente mencionado dentro das configurações dos projetos.

## <a name="ssma-v78"></a>SSMA v7.8

A versão v7.8 do SSMA para SAP ASE contém as seguintes alterações:

* Alterar mapeamento de tipo destacado nas **Configurações do projeto**.
* A capacidade dos usuários de desativar a telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

A versão v7.7 do SSMA para SAP ASE contém as seguintes alterações:

* O SSMA para SAP ASE foi aprimorado com correções direcionadas que melhoram as métricas de qualidade e conversão.
* Com base na demanda popular, a versão de 32 bits do SSMA para SAP ASE está de volta. Em comparação com a implementação anterior (antes ao v7.4), existem dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base nos componentes de conectividade que você tem. É sempre preferível usar a versão de 64 bits, se possível.

## <a name="ssma-v76"></a>SSMA v7.6

A versão v7.6 do SSMA para SAP ASE contém as seguintes alterações:

* Correções direcionadas que melhoram as métricas de qualidade e conversão e com suporte para o SQL Server 2017 (visualização pública). O suporte ao SQL Server 2017 no Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.
* Suporte para conversão de funções Sybase.

## <a name="ssma-v75"></a>SSMA v7.5

A versão v7.5 do SSMA para SAP ASE (anteriormente SSMA for Sybase) contém as seguintes alterações:

* Diversas melhorias para garantir maior acessibilidade às pessoas com deficiência.
* Suporte `CREATE OR REPLACE` para sintaxe.

## <a name="ssma-v74"></a>SSMA v7.4

A versão v7.4 do SSMA para Sybase contém as seguintes alterações:

* A **opção de tempo de tempo de consulta** está agora disponível durante a descoberta de objetos de esquema na origem e no destino.

  ![opção de tempo de consulta](../media/query-timeout_red.png)
* A métrica de qualidade e conversão foi melhorada com correções direcionadas, com base no feedback do cliente.

  > [!IMPORTANT]
  > .NET 4.5.2 é um pré-requisito para instalar o SSMA v7.4. Além disso, começando com o v7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>SSMA v7.3

A versão v7.3 do SSMA para Sybase contém as seguintes alterações:

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

A versão v7.2 do SSMA para Sybase contém as seguintes alterações:

* Melhor qualidade e métrica de conversão com correções direcionadas com base no feedback do cliente.
* Melhorias na telemetria para fornecer melhores pontos de dados para solucionar problemas dos clientes e melhorar as taxas de conversão da SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

A versão v7.1 do SSMA para Sybase contém as seguintes alterações:

* O SQL Server 2017 no Windows e linux CTP1 é agora uma plataforma-alvo suportada para migração. Esse recurso está na pré-visualização técnica e suporta esquema e movimentação de dados para direcionar servidores SQL.
* Suporte para atualizações automáticas para baixar a versão mais recente do SSMA assim que estiver disponível.
* Binários instalados do SSMA agora são entregues através de arquivos de pacote do Windows Installer (.msi).

## <a name="may-2016"></a>Maio de 2016

A versão de maio de 2016 do SSMA para Sybase contém as seguintes alterações:

* Suporte adicionado ao SQL Server 2016.
* Verificação do instalador removido para .NET 2.0.
* Dependência atualizada do pacote de extensão de .NET 3.5 a .NET 4.0.
* Fixo `save-project` `open-project` e comandos para console SSMA.
* Comando `securepassword` fixo para console SSMA.
* Contagem fixa de objetos para carregamento inicial.
* Corrigido bug em configurações globais.

## <a name="march-2016"></a>Março de 2016

A versão de pré-visualização de março de 2016 do SSMA para o Sybase adiciona suporte à migração para o SQL Server 2016.

## <a name="january-2016"></a>Janeiro de 2016

A versão de manutenção de janeiro de 2016 do SSMA para sybase contém as seguintes alterações:

* Adicionado Ver o item do menu de log ao SSMA (RFC 5706203).
* Adicionado Telemetria.

## <a name="july-2014"></a>Julho de 2014

A versão de julho de 2014 do SSMA para Sybase contém as seguintes alterações:

* Conversão aprimorada do código Azure SQL DB.
* Mudou a funcionalidade do pacote de extensão para esquema para suportar o Azure SQL DB.
* Adicionamos melhorias de desempenho testadas para bancos de dados com mais de 10k objetos.
* Adicionamos melhorias de IU para lidar com um grande número de objetos.
* Adicionado a capacidade de destacar esquemas lob bem conhecidos (para que eles possam ser ignorados na conversão).
* Adicionado melhorias na velocidade de conversão.
* Adicionado a capacidade de mostrar contagens de objetos em UI.
* Tamanho do relatório reduzido em mais de 25%.
* Mensagens de erro melhoradas para construções não parsed.

## <a name="april-2014"></a>Abril de 2014

A versão de abril de 2014 do SSMA para Sybase contém as seguintes alterações:

* Suporte adicionado ao MS SQL Server 2014.
* Corrigimos bugs em relação à conversão para o Azure.
* Corrigimos bugs em relação às páginas de relatórios invisíveis no IE 10.

## <a name="january-2012"></a>Janeiro de 2012

A versão de janeiro de 2012 do SSMA para Sybase contém as seguintes alterações:

* Adicionado suporte para conversão de gatilho de reversão.
* Providenciou correção `@@ROWCOUNT` para `@@ERROR` conversão `SET` e na mesma declaração.

## <a name="july-2011"></a>julho de 2011

A versão de julho de 2011 do SSMA para o Sybase fornece relatórios de erros melhorados durante a migração de dados.

## <a name="april-2011"></a>abril de 2011

A versão de abril de 2011 do SSMA para Sybase contém as seguintes alterações:

* Produto consolidado "SSMA for Sybase", [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]que [!INCLUDE [ssSQL11](../../includes/ssSQL11-md.md)] suporta , e Azure SQL.
* Suporte adicional para conectar e [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]migrar para .
* Adicionou um novo recurso para converter e migrar bancos de dados Sybase para o Azure SQL.
* Mecanismo de migração de dados do lado do cliente aprimorado, suportando migração paralela de dados.
* Melhor desempenho de migração de dados com modelos de recuperação registrados simples e a granel.
* Adicionada a capacidade de converter e migrar adequadamente os bancos de dados Sybase sensíveis a maiúsculas e minúsculas para o SQL Server sensível a maiúsculas e minúsculas.
* O suporte adicionado à conversão de declarações de adesão do Sybase ASE Non-ANSI às instruções de adesão ao SQL Server ANSI foi estendido para declarações DELETE e UPDATE.
* Forneceu opções adicionais de conectividade para se conectar aos servidores Sybase ASE usando o provedor Sybase ASE ODBC e os provedores de ADO.NET Sybase ASE.
* Removeu a dependência de `SysDB`um banco de dados separado chamado , que contém as funções de emulação do Sybase (instalado como parte do Extension Pack).
* Adicionada a capacidade de instalar SSMA para [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] Sybase Extension Pack em clusters.
* Adicionado a compatibilidade retrógrada de projetos criados por versões anteriores do SSMA (v4.0 e v4.2).
* Adicionada a capacidade de instalar o SSMA para sybase v5.0 produto lado a lado (SxS) com versões mais antigas do SSMA (v4.0 e v4.2).

## <a name="july-2010"></a>Julho de 2010

A versão de julho de 2010 do SSMA para o Sybase acrescentou:

* Suporte para migração para o SQL Server 2008 R2.
* Um novo aplicativo ssma console para execução de linha de comando.
* Suporte para migração de dados usando mecanismos de migração de dados do lado do servidor e do lado do cliente.
* Suporte à declaração "Custom SELECT" na migração de dados.
* Suporte para migração do Sybase ASE 15.0.3 e 15.5.

## <a name="june-2008"></a>junho de 2008

A versão de junho de 2008 do SSMA para sybase contém as seguintes alterações:

* Adicionado SSMA Tester, que testa automaticamente a conversão de objetos de banco de dados e a migração de dados feita pela SSMA. Depois que todas as etapas de migração do SSMA estiverem concluídas, use o SSMA Tester para verificar se os objetos convertidos funcionam da mesma maneira e que todos os dados foram transferidos corretamente.
* Adicionado conversão pré-SQL. O usuário agora pode especificar declarações temporárias de tabela (e outro objeto) para cada procedimento de origem a ser usado na conversão.
* Melhorias adicionadas na conversão de objetos:
  * Junta a conversão revisada.
  * Agregados e não agregados sem ter/grupo por cláusulas.
  * A `IDENTITY` função `SELECT INTO` com uma declaração.
  * Restrições e índices agrupados em somente dados bloqueados.
  * Tabelas temporárias `SELECT INTO`criadas por .
  * Restrições / Índices para tabelas temporárias.
  * Novos [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] tipos de data-hora são suportados.
  * Suporte a conectividade sybase 15.0 e tipos de dados.

## <a name="may-2007"></a>maio de 2007

A versão de maio de 2007 do SSMA para o Sybase acrescentou:

* A capacidade de carregar o conteúdo do banco de dados mais rapidamente ao salvar um projeto.
* Suporte para comentários inseridos pelo usuário no modo SQL formatado pelo SQL Server.
* Melhorias na conversão de objetos.

## <a name="november-2006"></a>novembro de 2006

A versão em novembro de 2006 do SSMA para sybase contém as seguintes alterações:

* Adicionado novas configurações globais:
  * Você pode optar por mostrar números de linha nas janelas do editor.
  * Você pode configurar o SSMA para solicitar a substituição de objetos duplicados, ou sempre ou nunca substituir objetos duplicados durante a conversão de esquemas.
* Adicionada uma nova opção de conversão que permite configurar como a SSMA lida com as seguintes situações:
  * Uma `CAST` `CONVERT` ou declaração que contenha uma seqüência binária.
  * Verifica valores nulos em expressões de igualdade.
  * Tabelas proxy.
  * Números de erro `RAISERROR`de mensagem do usuário para .
  * `UPDATE`declarações que contêm identificadores não resolvidos.
* Adicionada uma nova opção de migração que permite especificar como [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] a SSMA deve lidar com datas que estão fora do intervalo de datas.
* Adicionada uma configuração **SQL formatada** na guia **SQL,** que formata o código para uma melhor legibilidade.
* Correções de bugs, incluindo:
  * O SSMA `LOCK TABLE <table> IN { SHARED | EXCLUSIVE } MODE` agora converte `TABLOCK` `TABLOCKX` as instruções `SELECT` adicionando uma ou dica à consulta subseqüente na tabela.
  * Os moldes necessários são adicionados quando os tipos binários são usados em expressões de caracteres.
  * Melhorias de memória e desempenho.

## <a name="july-2006"></a>julho de 2006

A versão de julho de 2006 do SSMA for Sybase foi a versão inicial.

## <a name="see-also"></a>Confira também

[Começando com sSMA para Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
