---
title: O que há de novo no SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 44e59d80b21b71fbbc94b9c902edfb1019256d06
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70745289"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>O que há de novo no SSMA para SAP ASE (SybaseToSQL)

Este artigo lista Assistente de Migração do SQL Server (SSMA) para SAP ASE (anteriormente o SSMA para Sybase) alterações em cada versão.

## <a name="ssma-v84"></a>SSMA v 8.4

A versão v 8.4 do SSMA para SAP ASE foi aprimorada com correções direcionadas que foram projetadas para resolver problemas de acessibilidade e corrigir um bug relacionado a colunas de índice máximo (para permitir 32 em vez de 16) para SQL Server 2016 e versões posteriores.

> [!IMPORTANT]
> Com o SSMA v 7.4 e versões posteriores, o .NET 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v83"></a>SSMA v 8.3

A versão v 8.3 do SSMA para SAP ASE foi aprimorada com correções direcionadas que foram projetadas para melhorar a qualidade e a conversão de métricas. Além disso, esta versão do SSMA para SAP ASE fornece correções que:

* Solucionar problemas de acessibilidade
* Adicionar suporte básico para o tipo ' hierarchyid ' no SQL Server

## <a name="ssma-v82"></a>SSMA v8.2

A versão v 8.2 do SSMA para SAP ASE foi aprimorada com um conjunto direcionado de correções projetadas para melhorar a qualidade e a conversão de métricas, bem como correções para:

* Um problema com índices não clusterizados desabilitados após a migração de dados.
* Detecção de .NET Framework durante a instalação silenciosa.
* Uma falha intermitente que ocorre quando uma nova versão é baixada.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v 8.1 para v 8.2. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

A versão v 8.1 do SSMA para SAP ASE foi aprimorada com correções direcionadas que foram projetadas para melhorar a qualidade e a conversão de métricas.

> [!NOTE]
> Um problema conhecido com a atualização automática pode causar a falha de uma atualização do SSMA v 8.0 para o v 8.1. Se você encontrar esse erro, baixe a nova versão e instale-a manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

A versão v 8.0 do SSMA para SAP ASE foi aprimorada com correções direcionadas projetadas para melhorar a qualidade e a conversão de métricas. Além disso, esta versão oferece os seguintes novos recursos:

* Suporte para **instância gerenciada do banco de dados SQL do Azure** como um destino. Agora você pode criar novos projetos destinados a Instância Gerenciada do Banco de Dados SQL do Azure:

  ![Projeto MI do BD SQL](../media/ssma-newproject-sqldbmi.png)

* **Supervisor de correção**após a conversão. Saiba mais sobre isso [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Seleção preliminar de banco de dados/esquema.

  Ao se conectar à fonte, o usuário agora pode selecionar bancos de dados/esquemas de interesse. Selecionar somente os esquemas que você planeja migrar economizará tempo durante a conexão inicial e melhorará o desempenho geral do SSMA.

  ![Objetos de filtro do SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

A versão v 7.10 do SSMA para SAP ASE foi aprimorada com correções direcionadas projetadas para fornecer proteção adicional e proteções de privacidade para atender às alterações nos requisitos globais.

## <a name="ssma-v79"></a>SSMA v7.9

A versão v 7.9 do SSMA para SAP ASE contém as seguintes alterações:

* Correções direcionadas que melhoram a qualidade e as métricas de conversão.
* Suporte na linha de comando do SSMA para alterar o mapeamento de tipo de dados e as preferências do projeto.
* Suporte para migrar dados usando SQL Server Integration Services (SSIS). Depois de converter o esquema, é possível criar um pacote do SSIS usando uma opção de menu de contexto de clique com o botão direito do mouse.
* A caixa de diálogo conexão do banco de dados SQL do Azure no SSMA também foi alterada para especificar o nome do servidor totalmente qualificado. Nas versões anteriores do SSMA, o prefixo do banco de dados SQL do Azure tinha que ser explicitamente mencionado dentro das configurações de projetos.

## <a name="ssma-v78"></a>SSMA v7.8

A versão v 7.8 do SSMA para SAP ASE contém as seguintes alterações:

* Alterar o mapeamento de tipo realçado nas configurações do projeto.
* A capacidade dos usuários de desabilitar a telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

A versão v 7.7 do SSMA para SAP ASE contém as seguintes alterações:

* O SSMA para SAP ASE foi aprimorado com correções direcionadas que melhoram a qualidade e a conversão de métricas.
* Com base na demanda popular, a versão de 32 bits do SSMA para SAP ASE está de volta. Em comparação com a implementação anterior (antes da v 7.4), há dois pacotes do instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base nos componentes de conectividade que tem. É sempre preferível usar a versão de 64 bits, se possível.

## <a name="ssma-v76"></a>SSMA v7.6

A versão v 7.6 do SSMA para SAP ASE contém as seguintes alterações:

* Correções direcionadas que melhoram as métricas de qualidade e conversão e com suporte para SQL Server 2017 (visualização pública). O suporte para SQL Server 2017 no Windows e no Linux está em visualização pública e não deve ser usado para migrações de produção.
* Suporte para conversão de funções do Sybase.

## <a name="ssma-v75"></a>SSMA v7.5

A versão v 7.5 do SSMA para SAP ASE (anteriormente o SSMA para Sybase) contém as seguintes alterações:

* Várias melhorias para garantir maior acessibilidade para pessoas com deficiências.
* Suporte para criação ou substituição de sintaxe.

## <a name="ssma-v74"></a>SSMA v7.4

A versão v 7.4 do SSMA para Sybase contém as seguintes alterações:

* A opção de **tempo limite de consulta** agora está disponível durante a descoberta de objeto de esquema na origem e no destino.

  ![opção de tempo limite de consulta](../media/query-timeout_red.png)
* A métrica de qualidade e conversão foi aprimorada com correções direcionadas, com base nos comentários dos clientes.

  > [!IMPORTANT]
  > O .NET 4.5.2 é um pré-requisito para a instalação do SSMA v 7.4. Além disso, a partir da v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.  

## <a name="ssma-v73"></a>SSMA v7.3

A versão v 7.3 do SSMA para Sybase contém as seguintes alterações:

* Métrica de qualidade e conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
* Estrutura de extensibilidade do SSMA exposta por meio dos seguintes itens:
  * Exporte a funcionalidade para um projeto SQL Server Data Tools (SSDT).
    * Agora você pode exportar scripts de esquema do SSMA para um projeto SSDT. Você pode usar os scripts de esquema para fazer alterações de esquema adicionais e implantar seu banco de dados.

        ![Comando Save as SSDT Project](../media/export-schema-scripts_red.png)
  * Bibliotecas que podem ser consumidas pelo SSMA para executar conversões personalizadas.
    * Agora você pode construir código que pode manipular conversões e conversões de sintaxe personalizadas que não eram previamente tratadas pelo SSMA.
      * As instruções sobre como construir um conversor personalizado estão disponíveis nesta postagem de blog, [estendendo os recursos de conversão de assistente de migração do SQL Server](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Baixe um projeto de exemplo para conversão desta [postagem de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2

A versão v 7.2 do SSMA para Sybase contém as seguintes alterações:

* Métrica de qualidade e conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
* Aprimoramentos de telemetria para fornecer melhores pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

A versão v 7.1 do SSMA para Sybase contém as seguintes alterações:

* SQL Server 2017 no Windows e Linux CTP1 agora é uma plataforma de destino com suporte para migração. Esse recurso está em visualização técnica e dá suporte à movimentação de esquema e dados para servidores SQL de destino.
* Suporte para atualizações automáticas para baixar a versão mais recente do SSMA assim que ela estiver disponível.
* Os binários instaláveis do SSMA agora são fornecidos por meio dos arquivos de pacote do Windows Installer (. msi).

## <a name="may-2016"></a>Maio de 2016

A versão de maio de 2016 do SSMA para Sybase contém as seguintes alterações:  

* Adicionado suporte para SQL Server 2016.
* Verificação do instalador removida para .NET 2,0.
* Dependência do pacote de extensão atualizado do .net 3,5 para o .NET 4,0.
* Corrigidos os comandos "salvar projeto" e "Abrir projeto" para o console do SSMA.
* Foi corrigido o comando "SecurePassword" para o console do SSMA.
* Contagem fixa de objetos para carregamento inicial.
* Corrigido o bug nas configurações globais.

## <a name="march-2016"></a>Março de 2016

A versão de visualização de março de 2016 do SSMA para Sybase adiciona suporte para migração para o SQL Server 2016.  
  
## <a name="january-2016"></a>Janeiro de 2016

A versão de manutenção de janeiro de 2016 do SSMA para Sybase contém as seguintes alterações:  
  
* Item de menu Exibir log adicionado ao SSMA (RFC 5706203).  
* Telemetria adicionada.

## <a name="july-2014"></a>Julho de 2014

A versão de julho de 2014 do SSMA para Sybase contém as seguintes alterações:  
  
* Conversão de código do BD SQL do Azure aprimorada.  
* Funcionalidade do pacote de extensão movida para o esquema para dar suporte ao BD SQL do Azure.  
* Foram adicionados aprimoramentos de desempenho para bancos de dados com mais de 10 mil objetos.  
* Foram adicionadas melhorias na interface do usuário para lidar com um grande número de objetos.  
* Adicionada a capacidade de realçar esquemas LOB "bem conhecidos" (para que eles possam ser ignorados na conversão).  
* Melhorias na velocidade de conversão adicionada.  
* Adicionada a capacidade de mostrar contagens de objetos na interface do usuário.
* Tamanho de relatório reduzido em mais de 25%.  
* Mensagens de erro aprimoradas para construções não analisadas.  
  
## <a name="april-2014"></a>Abril de 2014

A versão de abril de 2014 do SSMA para Sybase contém as seguintes alterações:  
  
* Suporte adicionado do MS SQL Server 2014.  
* Correção de bugs referentes à conversão no Azure.  
* Correção de bugs em relação a páginas de relatório invisíveis no IE 10.  
  
## <a name="january-2012"></a>Janeiro de 2012

A versão de janeiro de 2012 do SSMA para Sybase contém as seguintes alterações:  
  
* Adicionado suporte para conversão de gatilho de reversão.
* Foi fornecida uma correção para@ROWCOUNT Converter @@ERROR e @ na mesma instrução SET.  
  
## <a name="july-2011"></a>Julho de 2011

A versão de julho de 2011 do SSMA para Sybase fornece relatórios de erros aprimorados durante a migração de dados.  
  
## <a name="april-2011"></a>Abril de 2011

A versão de abril de 2011 do SSMA para Sybase contém as seguintes alterações:  
  
* Produto consolidado "SSMA para Sybase", que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 2008, "Denali" e Azure SQL.  
* Adicionado suporte para conexão e migração para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
* Adicionou um novo recurso para converter e migrar bancos de dados Sybase para o SQL do Azure.  
* Mecanismo de migração de dados aprimorado do lado do cliente, oferecendo suporte à migração paralela de dados.  
* Melhor desempenho de migração de dados com modelos de recuperação simples e bulk-logged.
* Adicionada a capacidade de converter e migrar corretamente bancos de dados Sybase que diferenciam maiúsculas de minúsculas para SQL Server que diferenciam maiúsculas de minúsculas.  
* Suporte adicionado para conversão de instruções de junção não-ANSI do Sybase ASE para SQL Server instruções de junção ANSI foram estendidas para instruções DELETE e UPDATE.  
* Fornecemos opções de conectividade adicionais para se conectar a servidores do Sybase ASE usando o provedor ODBC ASE do Sybase e provedores de ADO.Net do Sybase ASE.
* Removida a dependência em um banco de dados separado chamado **SysDB**, que contém as funções de emulação Sybase (instaladas como parte do pacote de extensão).
* Adicionada a capacidade de instalar o SSMA para pacote de extensão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Sybase em clusters.
* Adição de compatibilidade com versões anteriores de projetos criados por versões mais antigas do SSMA (v 4.0 e v 4.2).  
* Adicionada a capacidade de instalar o produto SSMA para Sybase v 5.0 lado a lado (SxS) com versões mais antigas do SSMA (v 4.0 e v 4.2).  
  
## <a name="july-2010"></a>Julho de 2010

A versão de julho de 2010 do SSMA para Sybase adicionou:

* Suporte para migrar para o SQL Server 2008 R2.  
* Um novo aplicativo de console do SSMA para execução de linha de comando.  
* Suporte para migração de dados usando mecanismos de migração de dados do lado do servidor e do cliente.  
* Suporte para a instrução "SELECT personalizado" na migração de dados.  
* Suporte para migração do Sybase ASE 15.0.3 e 15,5.  
  
## <a name="june-2008"></a>Junho de 2008

A versão de junho de 2008 do SSMA para Sybase contém as seguintes alterações:  
  
* Foi adicionado o SSMA Tester, que testa automaticamente a conversão de objetos de banco de dados e a migração feita pelo SSMA. Depois que todas as etapas de migração do SSMA forem concluídas, use o SSMA Tester para verificar se os objetos convertidos funcionam da mesma maneira e se todos os dados foram transferidos corretamente.
* A conversão anterior ao SQL foi adicionada. Agora, o usuário pode especificar declarações de tabela temporária (e outro objeto) para cada procedimento de origem a ser usado na conversão.
* Aprimoramentos adicionados na conversão de objeto:  
  * A conversão de junções foi revisada.  
  * Agregações e não agregações sem cláusulas with/Group by.  
  * A função de identidade com uma instrução SELECT INTO.  
  * Restrições e índices clusterizados em somente dados bloqueados.  
  * Tabelas temporárias criadas por SELECT INTO.  
  * Restrições/índices para tabelas temporárias.  
  * Novos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de 2008 DateTime são suportados.  
  * Suporte a conectividade do Sybase 15,0 e tipos de datatipos.  
  
## <a name="may-2007"></a>Maio de 2007

A versão de maio de 2007 do SSMA para Sybase adicionou:  
  
* A capacidade de carregar o conteúdo do banco de dados mais rapidamente ao salvar um projeto.  
* Suporte para comentários inseridos pelo usuário no modo SQL SQL Server formatado.  
* Aprimoramentos na conversão de objetos.  

## <a name="november-2006"></a>Novembro de 2006

A versão de novembro de 2006 do SSMA para Sybase contém as seguintes alterações:  
  
* Novas configurações globais foram adicionadas:  
  * Você pode optar por Mostrar números de linha nas janelas do editor.  
  * Você pode configurar o SSMA para solicitar a substituição de objetos duplicados ou sempre ou nunca substituir objetos duplicados durante a conversão do esquema.  
* Adicionada uma nova opção de conversão que permite configurar como o SSMA lida com as seguintes situações:  
  * Uma instrução CAST ou CONVERT que contém uma cadeia de caracteres binária.  
  * Verifica se há valores nulos em expressões de igualdade.  
  * Tabelas de proxy.  
  * Números de erro de mensagem do usuário para RAISERROR.  
  * ATUALIZAR instruções que contêm identificadores não resolvidos.  
* Adicionada uma nova opção de migração que permite especificar como o SSMA deve lidar com datas que estão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fora do intervalo de datas.  
* Adicionada uma configuração **SQL formatada** na guia **SQL** , que formata o código para facilitar a legibilidade.  
* Correções de bugs, incluindo:
  * O SSMA agora converte a *tabela* de bloqueio de tabela em {Shared | EXCLUSIVO} instruções de modo adicionando uma dica TABLOCK ou TABLOCKX à consulta SELECT subsequente na tabela.  
  * As conversões necessárias agora são adicionadas quando tipos binários são usados em expressões de caracteres.  
  * Aprimoramentos na memória e no desempenho.  
  
## <a name="july-2006"></a>Julho de 2006

A versão de julho de 2006 do SSMA for Sybase foi a versão inicial.  
  
## <a name="see-also"></a>Confira também

[Introdução com o SSMA para &#40;Sybase SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
