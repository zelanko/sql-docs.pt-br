---
title: Quais são as novidades do SSMA para Access(AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 02/27/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 40d5daaaef68d4355a95fb6cef2c55628cdf4008
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955917"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>Quais são as novidades do SSMA para Access (AccessToSQL)
Este artigo lista os SQL Server Migration Assistant (SSMA) para que as alterações de acesso em cada versão.  

## <a name="ssma-v80"></a>SSMA v8.0
A versão v 8.0 do SSMA para Access foi aprimorada para fornecer correções direcionadas projetadas para melhorar a qualidade e a conversão de métricas. Esta versão também oferece os seguintes recursos novos:

* Suporte para **banco de dados de instância gerenciada do SQL** como um destino. Agora você pode criar novos projetos direcionados ao banco de dados de instância gerenciada do SQL:

  ![Projeto de banco de dados SQL para a MI](../media/ssma-newproject-sqldbmi.png)

*   Após a conversão **correção advisor**. Saiba mais sobre ele [aqui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Seleção de banco de dados ou o esquema preliminar.

    Ao se conectar à fonte, o usuário pode agora selecionar bancos de dados/esquemas de interesse. Selecionando apenas os esquemas que você planeja migrar economizar tempo durante a conexão inicial e melhorar o desempenho geral do SSMA.

    ![Objetos de filtro do SSMA](../media/ssma-filter-objects.png)

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.


## <a name="ssma-v710"></a>SSMA v7.10
A versão de v7.10 do SSMA para Access foi aprimorada com correções direcionadas projetadas para fornecer segurança adicional e proteções de privacidade para atender às mudanças nos requisitos de globais.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v79"></a>SSMA v7.9
A versão de v7.9 do SSMA para Access contém as seguintes alterações:
- Correções de destino que melhoram as métricas de qualidade e a conversão.
- Suporte a linha de comando do SSMA para alterar o mapeamento de tipo de dados e preferências de projeto.
- A caixa de diálogo de conexão de banco de dados SQL do SSMA também foi alterada para especificar o nome totalmente qualificado do servidor. Em versões anteriores do SSMA, o prefixo de banco de dados SQL precisava ser mencionado explicitamente dentro de configurações de projetos.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v78"></a>SSMA v7.8
A versão de v 7.8 do SSMA para Access contém as seguintes alterações:
- Mapeamento de tipo de alteração realçada nas configurações do projeto.
- Fornecida a capacidade dos usuários desabilitar a telemetria.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v77"></a>SSMA v7.7
A versão de v7.7 do SSMA para Access contém as seguintes alterações:
- O SSMA para Access foi aprimorado com correções direcionadas que melhoram as métricas de qualidade e a conversão.
- A versão de 32 bits do SSMA para Access com base na demanda popular, está de volta. Em comparação com a implementação anterior (antes da v 7.4), há dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais apropriada com base em componentes de conectividade, que você tem. É sempre preferível usar a versão de 64 bits, se possível.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v76"></a>SSMA v7.6
A versão de v7.6 do SSMA para Access foi aprimorada com correções direcionadas que melhoram as métricas de qualidade e a conversão e com suporte para SQL Server 2017 (visualização pública). Suporte para SQL Server 2017 no Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

> [!IMPORTANT]
> Com v SSMA 7.4 e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação e a versão de 32 bits da ferramenta foi descontinuada.

## <a name="ssma-v75"></a>SSMA v7.5
A versão de v 7.5 do SSMA para Access foi aprimorada com vários aprimoramentos para garantir que a maior acessibilidade para pessoas com deficiências.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito para instalar o SSMA v7.5. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v74"></a>SSMA v7.4
A versão de v 7.4 do SSMA para Access contém as seguintes alterações:
- O **tempo limite da consulta** opção agora está disponível durante a descoberta de objeto de esquema na origem e destino.
![opção de tempo limite de consulta](../media/query-timeout_red.png)

- A métrica de qualidade e a conversão foi aprimorada com correções direcionadas, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito para a instalação v SSMA 7.4. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>SSMA v7.3
A versão 7.3 do SSMA para Access contém as seguintes alterações:
- Métrica de qualidade e a conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
- Estrutura de extensibilidade do SSMA exposta por meio dos seguintes itens:
  - Exporte a funcionalidade para um projeto do SQL Server Data Tools (SSDT).
    -   Agora você pode exportar os scripts de esquema do SSMA para um projeto do SSDT. Você pode usar os scripts de esquema para fazer alterações de esquema adicional e implantar seu banco de dados.
![Salvar como um comando de projeto do SSDT](../media/export-schema-scripts_red.png)

  - Bibliotecas que podem ser consumidas por SSMA para realizar conversões personalizadas.
    - Agora você pode construir o código que pode lidar com conversões de sintaxe personalizada e conversões que anteriormente não eram tratadas pelo SSMA.
      - As instruções sobre como construir um conversor personalizado estão disponíveis nesta postagem de blog [recursos de conversão do estendendo o SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Baixe um projeto de exemplo para a conversão deste [postagem de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2
A versão de v7.2 do SSMA para Access contém as seguintes alterações:
- Métrica de qualidade e a conversão aprimorada com correções direcionadas com base nos comentários dos clientes.
- Aprimoramentos de telemetria para fornecer melhor pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>SSMA v7.1
A versão de v7.1 do SSMA para Access contém as seguintes alterações:
- Agora, o SQL Server 2017 no Windows e Linux CTP1 é uma plataforma de destino com suporte para a migração. Esse recurso está na visualização técnica e dá suporte à movimentação de dados e esquema para servidores de SQL de destino.
- Agora, o SSMA dá suporte a atualizações automáticas para baixar a versão mais recente do SSMA assim que ele está disponível.
- Agora, os binários instaláveis do SSMA são entregues por meio de arquivos de pacote do Windows installer (. msi).

**Recursos**

[Estendendo os recursos da SQL Server Migration Assistant conversão](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
  
## <a name="may-2016"></a>Maio de 2016  
A versão de maio de 2016 do SSMA para Access contém as seguintes alterações:  
  
-  Adicionado suporte oficial para o SQL Server 2016
-  Removida a verificação de instalador para .net 2.0.
-  Corrigido "salvar o projeto" e "Abrir projeto" comandos para o Console do SSMA.
-  Corrigido o comando "securepassword" para o Console do SSMA.
-  Correção de contagem de objetos para o carregamento inicial.
-  Correção de carregamento para as guias da interface do usuário para acesso de dados de tabelas.
-  Corrigido o bug nas configurações globais. 
   
## <a name="march-2016"></a>Março de 2016  
A versão de preview de março de 2016 do SSMA para Access contém as seguintes alterações:  
  
-  Adicionado suporte para migração para o SQL Server 2016.  
   
## <a name="january-2016"></a>Janeiro de 2016  
A versão de manutenção de janeiro de 2016 do SSMA para Access contém as seguintes alterações:  
  
-  Função Fixed inválida para o padrão de um campo GUID (RFC 3894811).  
-  Suspensão fixo sobre a importação de registros de banco de dados SQL (Azure) (RFC 4919573).  
-  Item de Menu exibição adicionado Log para o SSMA (RFC 5706203).  
-  Adicionada a telemetria.  
  
## <a name="july-2014"></a>Julho de 2014  
A versão de julho de 2014 do SSMA para Access contém as seguintes alterações:  
  
-   Melhor conversão de código de BD SQL do Azure.  
-   Movido funcionalidade do pacote de extensão para o esquema para dar suporte ao BD SQL do Azure.  
-   Melhorias de desempenho testadas para bancos de dados com mais de 10 mil objetos.  
-   Foram incluídos aperfeiçoamentos de interface do usuário para lidar com um grande número de objetos.  
-   Adicionado suporte para realce de "bem conhecidas" esquemas LOB (de modo que eles podem ser ignorados na conversão).  
-   Adicionadas as melhorias de velocidade de conversão.
-   Suporte adicionado para mostrar o objeto de conta na interface do usuário.
-   Tamanho do relatório reduzida em mais de 25%.
-   Mensagens de erro aprimoradas para construções não analisadas.  
  
## <a name="april-2014"></a>Abril de 2014  
A versão de abril de 2014 do SSMA para Access contém as seguintes alterações:  
  
-   Adicionado suporte para o MS SQL Server 2014.  
-   Bugs corrigidos em relação à conversão para o Azure.  
-   Bugs corrigidos em relação à páginas de relatório invisível no IE 10.  
  
## <a name="january-2012"></a>Janeiro de 2012  
A versão de janeiro de 2012 do SSMA para Access contém as seguintes alterações:  
  
-   Fornecidos a opção para persistir não nome de usuário e senha para o MS Access vinculadas a tabelas após a migração.  
-   Defina ações em cascata para referências circulares a nenhuma ação.  
-   Desde que as mensagens apropriadas indicando ações em cascata para referências circulares foram definidas como nenhuma ação.  
  
## <a name="july-2011"></a>Julho de 2011  
A versão de julho de 2011 do SSMA para Access contém as seguintes alterações:  
  
-   Aprimorado relatórios de erros durante a migração de dados.  
  
## <a name="april-2011"></a>Abril de 2011  
A versão de abril de 2011 do SSMA para Access contém as seguintes alterações:  
  
-   Adicionada a um único pode ser instalado do "SSMA para Access", que dá suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" e o SQL Azure.  
-   Adicionada a capacidade de conectar-se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
-   O SSMA adicionado para a versão do Console de acesso dá suporte para compatibilidade com versões anteriores. Você pode abrir os projetos criados por versões anterior para o SSMA v5.0.
-   Adicionada a capacidade de instalar o produto de v5.0 SSMA lado a lado (SxS) com as versões mais antigas do produto do SSMA.  
  
## <a name="july-2010"></a>Julho de 2010  
A versão de julho de 2010 do SSMA para Access contém as seguintes alterações:  
  
-   Adicionado suporte para migração para o SQL Server 2008 R2 e SQL do Azure.
-   Adicionada uma conexão segura ao SQL Server e SQL do Azure.  
-   Adicionado suporte para bancos de dados do Access 2010.
-   Adicionado um novo aplicativo de Console do SSMA para execução de linha de comando.
-   Adicionado suporte para o tipo de dados DateTime2 do SQL Server.
  
## <a name="june-2008"></a>Junho de 2008  
A versão de junho de 2008 do SSMA para Access contém as seguintes alterações:  
  
-   Adicionado suporte para bancos de dados do Access 2007.  
  
## <a name="may-2007"></a>Maio de 2007  
A versão de maio de 2007 do SSMA para Access contém as seguintes alterações:  
  
-   Adicionado suporte para bancos de dados do Access que usam políticas de grupo de trabalho.  
-   Fornecida a capacidade de excluir objetos convertidos do Gerenciador de metadados do SQL Server.  
-   Adicionado suporte para comentários inseridos pelo usuário no SQL Server formatada de modo SQL.  
-   Foram incluídos aperfeiçoamentos na conversão do objeto.  
  
## <a name="november-2006"></a>Novembro de 2006  
A versão de novembro de 2006 do SSMA para Access contém as seguintes alterações:  
  
-   Adicionado um novo Assistente de migração de banco de dados que orienta você durante a migração de um banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
-   Adicionada uma nova conversão, carga, e o comando de migração que converte os bancos de dados do Access, carrega os objetos convertidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e migra os dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tudo em uma única etapa.  
-   Migração de aprimorado de consultas. Migração de consulta agora converte mais selecionar consultas para modos de exibição. Para obter mais informações, consulte [converter objetos de banco de dados do Access](converting-access-database-objects-accesstosql.md).  
-   Adicionada a capacidade de editar propriedades da tabela e índice na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tabela** guia.  
-   Adicionadas novas configurações globais:  
    -   Você pode optar por mostrar números de linha nas janelas do editor.  
    -   Você pode configurar o SSMA para perguntar antes de substituir objetos duplicados ou sempre ou nunca substituir objetos duplicados durante a conversão do esquema.  
-   Adicionada uma nova opção de conversão que permite que você especifique se o SSMA exibirá um aviso quando uma consulta complexa contém um caractere curinga.  
  
## <a name="july-2006"></a>Julho de 2006  
A versão de julho de 2006 do SSMA para Access é a versão inicial.
