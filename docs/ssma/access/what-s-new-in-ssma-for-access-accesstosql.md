---
title: Novidades do SSMA para Access(AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 03/01/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
caps.latest.revision: 37
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3040ae9d8d73f45dc5e2128d411054e527278ab1
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774292"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>Novidades do SSMA para Access (AccessToSQL)
Este tópico lista SSMA para alterações de acesso de cada versão.  

## <a name="ssma-v77"></a>O SSMA v7.7
A versão de v7.7 do SSMA para Access contém as seguintes alterações:
- O SSMA para Access foi aprimorado com correções de destino que melhoram a métrica de qualidade e a conversão.
- A versão de 32 bits do SSMA para Access com base na demanda popular, está de volta. Em comparação com a implementação anterior (antes da v 7.4), existem dois pacotes de instalador, mas eles não podem ser instalados lado a lado. Como resultado, você deve escolher a versão mais adequada com base nos componentes de conectividade, que você tem. Sempre é preferível usar a versão de 64 bits, se possível.

> [!IMPORTANT]
> Com a v 7.4 do SSMA e versões posteriores, o .net 4.5.2 é um pré-requisito de instalação.

## <a name="ssma-v76"></a>O SSMA v7.6
A versão de v7.6 do SSMA para Access foi aprimorada com correções de destino que melhoram a qualidade e a conversão de métricas e com suporte para SQL Server 2017 (visualização pública). Suporte para SQL Server 2017 em Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

> [!IMPORTANT]
> Com v 7.4 do SSMA e versões posteriores, .net 4.5.2 é um pré-requisito de instalação e a versão de 32 bits da ferramenta foi descontinuada.

## <a name="ssma-v75"></a>V 7.5 do SSMA
A versão v 7.5 do SSMA para Access foi aprimorada com vários aprimoramentos para assegurar maior acessibilidade para pessoas com deficiências.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito de instalação v SSMA 7.5. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v74"></a>V 7.4 do SSMA
A versão v 7.4 do SSMA para Access contém as seguintes alterações:
- O **tempo limite da consulta** opção agora está disponível durante a descoberta de objeto de esquema na origem e no destino.
![opção de tempo limite de consulta](../media/query-timeout_red.png)

- A métrica de qualidade e a conversão foi aprimorada com correções de destino, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito de instalação v 7.4 do SSMA. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>O SSMA 7.3
A versão 7.3 do SSMA para Access contém as seguintes alterações:
- Métrica de qualidade e conversão aprimorada com correções de destino com base nos comentários dos clientes.
- Estrutura de extensibilidade do SSMA exposta por meio de itens a seguir:
  - Exporte funcionalidade a um projeto do SQL Server Data Tools (SSDT).
    -   Agora você pode exportar os scripts de esquema do SSMA para um projeto do SSDT. Você pode usar os scripts de esquema para fazer alterações de esquema adicionais e implantar seu banco de dados.
![Comando de projeto SSDT Salvar como](../media/export-schema-scripts_red.png)

  - Bibliotecas que podem ser consumidas por SSMA para realizar conversões personalizados.
    - Agora você pode construir o código que pode lidar com conversões de sintaxe personalizada e conversões que anteriormente não foram manipulados por SSMA.
      - Instruções sobre como construir um conversor personalizado estão disponíveis nesta postagem de blog, [recursos de conversão do estendendo o SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Projeto de exemplo para a conversão pode ser baixar este [postagem de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>V 7.2 do SSMA
A versão v 7.2 do SSMA para Access contém as seguintes alterações:
- Métrica de qualidade e conversão aprimorada com correções de destino com base nos comentários dos clientes.
- Aprimoramentos de telemetria para fornecer melhor pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>V 7.1 do SSMA
A versão v 7.1 do SSMA para Access contém as seguintes alterações:
- 2017 do SQL Server no Windows e Linux CTP1 agora é uma plataforma de destino com suporte para migração. Este recurso está na visualização técnica e oferece suporte à movimentação de dados e esquema para servidores de SQL de destino.
- O SSMA agora dá suporte a atualizações automáticas para baixar a versão mais recente do SSMA assim que ele está disponível.
- Binários instaláveis do SSMA agora são entregues por meio de arquivos de pacote do Windows installer (. msi).

**Recursos**

[Estendendo o recursos de conversão do SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
  
## <a name="may-2016"></a>Maio de 2016  
A versão de maio de 2016 do SSMA para Access contém as seguintes alterações:  
  
-  Adicionado suporte oficial para SQL Server 2016
-  Removida a seleção de instalador para .net 2.0.
-  Fixa "salvar o projeto" e "Abrir projeto" comandos do Console SSMA.
-  Comando fixa "securepassword" para o Console do SSMA.
-  Correção de contagem de objetos para o carregamento inicial.
-  Carregamento de dados fixa tabelas para as guias da interface do usuário para acesso.
-  Correção do bug nas configurações globais. 
   
## <a name="march-2016"></a>Março de 2016  
A versão de visualização de março de 2016 do SSMA para Access contém as seguintes alterações:  
  
-  Adicionado suporte para migração para o SQL Server 2016.  
   
## <a name="january-2016"></a>Janeiro de 2016  
A versão de manutenção de janeiro de 2016 do SSMA para Access contém as seguintes alterações:  
  
-  Função Fixed inválida para o padrão de um campo GUID (RFC 3894811).  
-  Suspensão fixo sobre a importação de registros de banco de dados SQL (Azure) (RFC 4919573).  
-  Item de Menu de Log de exibição adicionado para o SSMA (RFC 5706203).  
-  Telemetria adicionada.  
  
## <a name="july-2014"></a>Julho de 2014  
A versão de julho de 2014 do SSMA para Access contém as seguintes alterações:  
  
-   Conversão de código de banco de dados do Azure SQL aprimorado.  
-   Movido funcionalidade do pacote de extensão para o esquema para oferecer suporte a banco de dados de SQL do Azure.  
-   Melhorias de desempenho testado para bancos de dados com objetos de mais de 10 k.  
-   Aprimoramentos da interface do usuário adicionais para lidar com um grande número de objetos.  
-   Adicionado suporte para realce de esquemas LOB "bem conhecidas" (para que eles podem ser ignorados na conversão).  
-   Melhorias de velocidade de conversão adicional.
-   Suporte adicionado para mostrar o objeto de conta na interface do usuário.
-   Tamanho do relatório reduzida em mais de 25%.
-   Mensagens de erro aprimoradas para construções não analisadas.  
  
## <a name="april-2014"></a>Abril de 2014  
A versão de abril de 2014 do SSMA para Access contém as seguintes alterações:  
  
-   Adicionado suporte para MS SQL Server 2014.  
-   Bugs corrigidos sobre conversão para o Azure.  
-   Bugs corrigidos sobre páginas de relatório invisível no Internet Explorer 10.  
  
## <a name="january-2012"></a>Janeiro de 2012  
A versão de janeiro de 2012 do SSMA para Access contém as seguintes alterações:  
  
-   Fornecida a opção para persistir não o nome de usuário e senha para o Microsoft Access tabelas vinculadas após a migração.  
-   Defina ações em cascata para referências circulares em nenhuma ação.  
-   Fornecido adequadas mensagens indicando ações em cascata para referências circulares foram definidas como nenhuma ação.  
  
## <a name="july-2011"></a>Julho de 2011  
A versão de julho de 2011 do SSMA para Access contém as seguintes alterações:  
  
-   Melhor relatórios de erros durante a migração de dados.  
  
## <a name="april-2011"></a>Abril de 2011  
A versão de abril de 2011 do SSMA para Access contém as seguintes alterações:  
  
-   Adicionado um único pode ser instalado do "SSMA para Access", que dá suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" e SQL Azure.  
-   Adicionada a capacidade de conectar-se [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
-   SSMA adicionado para a versão do Console de acesso de suporte para compatibilidade com versões anteriores. Você pode abrir os projetos criados por versões anteriores para v 5.0 do SSMA.
-   Adicionada a capacidade de instalar o produto de v 5.0 SSMA lado a lado (SxS) com versões anteriores do produto do SSMA.  
  
## <a name="july-2010"></a>Julho de 2010  
A versão de julho de 2010 do SSMA para Access contém as seguintes alterações:  
  
-   Adicionado suporte para migração para o SQL Server 2008 R2 e SQL Azure.
-   Adicionada uma conexão segura ao SQL Server e SQL Azure.  
-   Adicionado suporte para bancos de dados do Access 2010.
-   Adicionado um novo aplicativo de Console SSMA para execução de linha de comando.
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
  
-   Adicionado um novo Assistente de migração de banco de dados que orienta você durante a migração de um único banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
-   Adicionada uma nova conversão, carga, e migração de comando que converte os bancos de dados do Access, carrega os objetos convertidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], e migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tudo em uma única etapa.  
-   Migração de consulta melhor. Migração de consulta agora converte mais selecionar consultas para modos de exibição. Para obter mais informações, consulte [converter objetos de banco de dados do Access](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c).  
-   Adicionada a capacidade de editar propriedades da tabela e índice no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **tabela** guia.  
-   Adicionadas novas configurações globais:  
    -   Você pode optar por mostrar números de linha na janela do editor.  
    -   Você pode configurar o SSMA para perguntar antes de substituir objetos duplicados ou sempre ou nunca substituir objetos duplicados durante a conversão do esquema.  
-   Adicionada uma nova opção de conversão que permite que você especifique se o SSMA exibe um aviso quando uma consulta complexa contém um caractere curinga.  
  
## <a name="july-2006"></a>Julho de 2006  
A versão de julho de 2006 do SSMA para Access foi a versão inicial.
