---
title: Quais são as novidades do SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/22/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c6e423af0a859932cc78e097b7a73e1644d3cccf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836374"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>Quais são as novidades do SSMA para SAP ASE (SybaseToSQL)
Este artigo lista SSMA para SAP ASE (anteriormente conhecido como SSMA para Sybase) alterações em cada versão. 

## <a name="ssma-v710"></a>O SSMA v7.10
A versão de v7.10 do SSMA para SAP ASE foi aprimorada com correções direcionadas projetadas para fornecer segurança adicional e proteções de privacidade para atender às mudanças nos requisitos de globais.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v79"></a>O SSMA v7.9
A versão de v7.9 do SSMA para SAP ASE contém as seguintes alterações:
- Correções de destino que melhoram as métricas de qualidade e a conversão.
- Suporte a linha de comando do SSMA para alterar o mapeamento de tipo de dados e preferências de projeto.
- Suporte para a migração de dados usando o SQL Server Integration Services (SSIS). Depois de converter o esquema, é possível criar um pacote do SSIS por meio de uma opção de menu de contexto do botão direito do mouse.
- A caixa de diálogo de conexão de banco de dados SQL do SSMA também foi alterada para especificar o nome totalmente qualificado do servidor. Em versões anteriores do SSMA, o prefixo de banco de dados SQL precisava ser mencionado explicitamente dentro de configurações de projetos.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v78"></a>V 7.8 do SSMA
A versão de v 7.8 do SSMA para SAP ASE contém as seguintes alterações:
- Mapeamento de tipo de alteração realçada nas configurações do projeto.
- Fornecida a capacidade dos usuários desabilitar a telemetria.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v77"></a>O SSMA v7.7
A versão de v7.7 do SSMA para SAP ASE contém as seguintes alterações:
- O SSMA para SAP ASE foi aprimorado com correções direcionadas que melhoram as métricas de qualidade e a conversão.
- A versão de 32 bits do SSMA para SAP ASE com base na demanda popular, está de volta. Em comparação com a implementação anterior (antes da v 7.4), há dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base em componentes de conectividade, que você tem. É sempre preferível usar a versão de 64 bits, se possível.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v76"></a>O SSMA v7.6
A versão de v7.6 do SSMA para SAP ASE contém as seguintes alterações:
- O SSMA para SAP ASE foi aprimorado com correções direcionadas que melhoram as métricas de qualidade e a conversão e com suporte para SQL Server 2017 (visualização pública). Suporte para SQL Server 2017 no Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.
- O SSMA para SAP ASE foi atualizado para fornecer suporte para conversão de funções do Sybase.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação e a versão de 32 bits da ferramenta foi descontinuada.

## <a name="ssma-v75"></a>O SSMA v7.5
A versão de v 7.5 do SSMA para SAP ASE contém as seguintes alterações:
-   Aprimorado com vários aprimoramentos para garantir que a maior acessibilidade para pessoas com deficiências.
-   Atualizado para fornecer suporte para sintaxe CREATE ou REPLACE.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito para instalar o SSMA v7.5. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.  

## <a name="ssma-v74"></a>V 7.4 do SSMA
A versão de v 7.4 do SSMA para Sybase contém as seguintes alterações:
- O **tempo limite da consulta** opção agora está disponível durante a descoberta de objeto de esquema na origem e destino.
![opção de tempo limite de consulta](../media/query-timeout_red.png)
- A métrica de qualidade e a conversão foi aprimorada com correções direcionadas, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito para a instalação v SSMA 7.4. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.  

## <a name="ssma-v73"></a>O SSMA 7.3
A versão 7.3 do SSMA para Sybase contém as seguintes alterações:
- Métrica de qualidade e a conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
- Estrutura de extensibilidade do SSMA exposta por meio dos seguintes itens:
  - Exporte a funcionalidade para um projeto do SQL Server Data Tools (SSDT).
    -   Agora você pode exportar os scripts de esquema do SSMA para um projeto do SSDT. Você pode usar os scripts de esquema para fazer alterações de esquema adicional e implantar seu banco de dados.
![Salvar como um comando de projeto do SSDT](../media/export-schema-scripts_red.png)
  - Bibliotecas que podem ser consumidas por SSMA para realizar conversões personalizadas.
    - Agora você pode construir o código que pode lidar com conversões de sintaxe personalizada e conversões que anteriormente não eram tratadas pelo SSMA.
      - As instruções sobre como construir um conversor personalizado estão disponíveis nesta postagem de blog [recursos de conversão do estendendo o SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Baixe um projeto de exemplo para a conversão deste [postagem de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>O SSMA v7.2
A versão de v7.2 do SSMA para Sybase contém as seguintes alterações:
- Métrica de qualidade e a conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
- Aprimoramentos de telemetria para fornecer melhor pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>O SSMA v7.1
A versão de v7.1 do SSMA para Access contém as seguintes alterações:
- Agora, o SQL Server 2017 no Windows e Linux CTP1 é uma plataforma de destino com suporte para a migração. Esse recurso está na visualização técnica e dá suporte à movimentação de dados e esquema para servidores de SQL de destino.
- Agora, o SSMA dá suporte a atualizações automáticas para baixar a versão mais recente do SSMA assim que ele está disponível.
- Agora, os binários instaláveis do SSMA são entregues por meio de arquivos de pacote do Windows installer (. msi).

**Recursos**

[Estendendo os recursos da SQL Server Migration Assistant conversão](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Avaliar e migrar dados de plataformas de dados não Microsoft para SQL Server *(com o exemplo do Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Maio de 2016  
A versão de maio de 2016 do SSMA para Sybase contém as seguintes alterações:  

-  Adicionado suporte para SQL Server 2016.
-  Removida a verificação de instalador para .net 2.0.
-  Dependência do pacote de extensão atualizada do .net 3.5 para o .net 4.0.
-  Corrigido "salvar o projeto" e "Abrir projeto" comandos para o Console do SSMA.
-  Corrigido o comando "securepassword" para o Console do SSMA.
-  Correção de contagem de objetos para o carregamento inicial.
-  Corrigido o bug nas configurações globais.

## <a name="march-2016"></a>Março de 2016  
A versão de preview de março de 2016 do SSMA para Sybase contém as seguintes alterações:  
  
-  Adicionado suporte para migração para o SQL Server 2016.  
  
## <a name="january-2016"></a>Janeiro de 2016  
A versão de manutenção de janeiro de 2016 do SSMA para Sybase contém as seguintes alterações:  
  
-  Item de Menu exibição adicionado Log para o SSMA (RFC 5706203).  
-  Adicionada a telemetria. 
  
## <a name="july-2014"></a>Julho de 2014  
A versão de julho de 2014 do SSMA para Sybase contém as seguintes alterações:  
  
-  Melhor conversão de código de BD SQL do Azure.  
-  Movido funcionalidade do pacote de extensão para o esquema para dar suporte ao BD SQL do Azure.  
-  Melhorias de desempenho adicionados testadas para bancos de dados com mais de 10 mil objetos.  
-  Foram incluídos aperfeiçoamentos de interface do usuário para lidar com um grande número de objetos.  
-  Adicionada a capacidade de realçar "bem conhecidas" esquemas LOB (de modo que eles podem ser ignorados na conversão).  
-  Adicionadas as melhorias de velocidade de conversão.  
-  Adicionada a capacidade de mostrar a contagem de objetos na interface do usuário. 
-  Tamanho do relatório reduzida em mais de 25%.  
-  Mensagens de erro aprimoradas para construções não analisadas.  
  
## <a name="april-2014"></a>Abril de 2014  
A versão de abril de 2014 do SSMA para Sybase contém as seguintes alterações:  
  
-   Adicionado suporte do MS SQL Server 2014.  
-   Bugs corrigidos em relação à conversão para o Azure.  
-   Bugs corrigidos em relação à páginas de relatório invisível no IE 10.  
  
## <a name="january-2012"></a>Janeiro de 2012  
A versão de janeiro de 2012 do SSMA para Sybase contém as seguintes alterações:  
  
-   Adicionado suporte para conversão de gatilho de reversão.  
-   Fornecida a correção para a conversão de@ROWCOUNT e @@ERROR na mesma instrução SET.  
  
## <a name="july-2011"></a>Julho de 2011  
A versão de julho de 2011 do SSMA para Sybase contém as seguintes alterações:  
  
-   Aprimorado relatórios de erros durante a migração de dados.  
  
## <a name="april-2011"></a>Abril de 2011  
A versão de abril de 2011 do SSMA para Sybase contém as seguintes alterações:  
  
-   Produto "SSMA para Sybase" consolidado, o que dá suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" e o SQL Azure.  
-   Adicionado suporte para se conectar e migrar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
-   Adicionado um novo recurso para converter e migrar bancos de dados Sybase para o SQL Azure.  
-   Mecanismo de migração aprimorada de dados do cliente, que dão suporte a migração paralela de dados.  
-   Desempenho de migração de dados aprimorada com simples e Bulk logged modelos de recuperação.  
-   Adicionada a capacidade de converter corretamente e migrar bancos de dados Sybase diferencia maiusculas de minúsculas para o SQL Server diferencia maiusculas de minúsculas.  
-   Adicionado suporte para conversão de instruções de junção Sybase ASE não-ANSI para instruções de junção ANSI do SQL Server foi estendido para excluir e atualizar as instruções.  
-   Opções de conectividade adicional para se conectar a servidores de ASE do Sybase usando o provedor Sybase ASE ODBC e provedores ADO.Net do Sybase ASE de fornecido.  
-   Removida a dependência em um banco de dados separado chamado **SysDB**, que contém as funções de emulação do Sybase (instaladas como parte do pacote de extensão).  
-   Adicionada a capacidade de instalar o SSMA para Sybase pacote de extensão em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clusters.  
-   Adicionada compatibilidade com versões anteriores de projetos criados por versões anteriores do SSMA (v4.0 e v4.2).  
-   Adicionada a capacidade de instalar o SSMA para Sybase v5.0 produto lado a lado (SxS) com as versões mais antigas do SSMA (v4.0 e v4.2).  
  
## <a name="july-2010"></a>Julho de 2010  
A versão de julho de 2010 do SSMA para Sybase contém as seguintes alterações:  
  
-   Adicionado suporte para migração para o SQL Server 2008 R2.  
-   Adicionado um novo aplicativo de Console do SSMA para execução de linha de comando.  
-   Adicionado suporte para migração de dados usando mecanismos de migração de dados do lado do cliente e do servidor.  
-   Adicionado suporte para a instrução "SELECT personalizada" na migração de dados.  
-   Adicionado suporte para a migração do Sybase ASE 15.0.3 e 15.5.  
  
## <a name="june-2008"></a>Junho de 2008  
A versão de junho de 2008 do SSMA para Sybase contém as seguintes alterações:  
  
-   Adicionado o SSMA testador, quais testes automaticamente a conversão do objeto de banco de dados e a migração de dados feitas por SSMA. Depois que todas as etapas de migração do SSMA estiverem concluídas, use o SSMA testador para verificar objetos convertidos funcionam da mesma maneira e que todos os dados foi transferido corretamente.  
-   Conversão de versão anterior do SQL adicionado. Usuário agora pode especificar a tabela temporária (e outro objeto) declarações para cada procedimento de origem a ser usado na conversão.  
-   Foram incluídos aperfeiçoamentos na conversão do objeto:  
    -   Une conversão revisado.  
    -   Agregações e agregações sem ter que/grupo por cláusulas.  
    -   A função de identidade com uma instrução SELECT INTO.  
    -   Restrições em cluster e índices em somente dados bloqueados.  
    -   Tabelas temporárias criadas pelo SELECT INTO.  
    -   Restrições de / índices para tabelas temporárias.  
    -   Novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] há suporte para tipos de data e hora de 2008.  
    -   Suporte de conectividade e tipos de dados Sybase 15.0.  
  
## <a name="may-2007"></a>Maio de 2007  
A versão de maio de 2007 do SSMA para Sybase contém as seguintes alterações:  
  
-   Adicionada a capacidade de carregar o conteúdo do banco de dados mais rapidamente ao salvar um projeto.  
-   Adicionado suporte para comentários inseridos pelo usuário no SQL Server formatada de modo SQL.  
-   Foram incluídos aperfeiçoamentos na conversão do objeto.  
  
O arquivo de Ajuda não foi atualizado para esta versão. Para obter mais informações, consulte a seção Observações da documentação mais adiante neste artigo.  
  
## <a name="november-2006"></a>Novembro de 2006  
A versão de novembro de 2006 do SSMA para Sybase contém as seguintes alterações:  
  
-   Adicionadas novas configurações globais:  
    -   Você pode optar por mostrar números de linha nas janelas do editor.  
    -   Você pode configurar o SSMA para perguntar antes de substituir objetos duplicados ou sempre ou nunca substituir objetos duplicados durante a conversão do esquema.  
-   Adicionada uma nova opção de conversão que lhe permite configurar como o SSMA lida com as seguintes situações:  
    -   Uma instrução CAST ou CONVERT que contém uma cadeia de caracteres binária.  
    -   Verifica se há valores nulos em expressões de igualdade.  
    -   Tabelas de proxy.  
    -   Números de erro da mensagem de usuário para RAISERROR.  
    -   Instruções de atualização que contêm identificadores não resolvidos.  
-   Adicionada uma nova opção de migração que permite que você especifique como o SSMA deve tratar as datas que estão fora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervalo de datas.  
-   Adicionada uma **SQL formatados** definindo na **SQL** guia, que formata o código para melhor legibilidade.  
-   Correções de bugs, incluindo:  
    -   O SSMA agora converte a tabela de bloqueio *tabela* IN {SHARED | Instruções de modo exclusivo} com a adição de uma dica TABLOCK ou TABLOCKX para a consulta SELECT subsequente na tabela.  
    -   As conversões necessárias agora são adicionadas quando tipos binários são usados em expressões de caractere.  
    -   Melhorias de desempenho e de memória.  
  
## <a name="july-2006"></a>Julho de 2006  
A versão de julho de 2006 do SSMA for Sybase foi a versão inicial.  
  
## <a name="see-also"></a>Consulte também  
[Introdução ao SSMA para Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
