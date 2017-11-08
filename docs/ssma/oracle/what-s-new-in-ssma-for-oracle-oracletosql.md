---
title: Novidades do SSMA para Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 09/22/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a435479b9cad332215b1f44f7d881f5055b2fefd
ms.openlocfilehash: 9e1b0d59ec958bdd5abc254ce289df88ea80e04f
ms.contentlocale: pt-br
ms.lasthandoff: 11/08/2017

---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>Novidades do SSMA para Oracle (OracleToSQL)
Este tópico lista SSMA para alterações do Oracle em cada versão.  

## <a name="ssma-v76"></a>O SSMA v7.6
A versão de v7.6 do SSMA para Oracle foi aprimorada com correções de destino que melhoram a qualidade e a conversão de métricas e com suporte para SQL Server 2017 (visualização pública). Suporte para SQL Server 2017 em Windows e Linux está em visualização pública e não deve ser usado para migrações de produção.

> [!IMPORTANT]
> Com v 7.4 do SSMA e versões posteriores, .net 4.5.2 é um pré-requisito de instalação e a versão de 32 bits da ferramenta foi descontinuada.

## <a name="ssma-v75"></a>V 7.5 do SSMA
A versão v 7.5 do SSMA para Oracle contém as seguintes alterações:
- Aprimorado com vários aprimoramentos para assegurar maior acessibilidade para pessoas com deficiências.
- Atualizado para melhorar a qualidade e a conversão métrica correções de destino, como manipulação aprimorada de tipos de dados de data e float durante a migração de dados, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito de instalação v SSMA 7.5. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v74"></a>V 7.4 do SSMA
A versão v 7.4 do SSMA para Oracle contém as seguintes alterações:

- SSMA para Oracle agora dá suporte ao Azure SQL Data Warehouse como uma plataforma de destino para migração.

    ![Nova janela de projeto](../media/new-project.png)
  - Suporta as opções de armazenamento do Data Warehouse, conforme mostrado na imagem a seguir:

    ![Opções de armazenamento para data warehouse](../media/storage-options_red.png)
  - Suporta as opções de distribuição de dados conforme mostrado na imagem a seguir:

    ![distribuição de dados para data warehouse](../media/data-distribution_red.png)

- O **tempo limite da consulta** opção agora está disponível durante a descoberta de objeto de esquema na origem e no destino.

    ![opção de tempo limite de consulta](../media/query-timeout_red.png)

- A métrica de qualidade e a conversão foi aprimorada com correções de destino, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito de instalação v 7.4 do SSMA. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

## <a name="ssma-v73"></a>O SSMA 7.3
A versão 7.3 do SSMA para Oracle contém as seguintes alterações:
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
A versão v 7.2 do SSMA para Oracle contém as seguintes alterações:
- Métrica de qualidade e conversão aprimorada com correções de destino com base nos comentários dos clientes.
- Aprimoramentos de telemetria para fornecer melhor pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.

## <a name="ssma-v71"></a>V 7.1 do SSMA
A versão v 7.1 do SSMA para Oracle contém as seguintes alterações:
- 2017 do SQL Server no Windows e Linux CTP1 agora é uma plataforma de destino com suporte para migração. Este recurso está na visualização técnica e permite a movimentação de dados e esquema para servidores de SQL de destino.
- O SSMA agora dá suporte a atualizações automáticas para baixar a versão mais recente do SSMA assim que ele está disponível.
- Binários instaláveis do SSMA agora são entregues por meio de arquivos de pacote do Windows installer (. msi).

**Recursos**

[Estendendo o recursos de conversão do SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Avaliar e migrar dados de plataformas de dados não Microsoft para SQL Server *(com exemplo de Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Maio de 2016  
A versão de maio de 2016 do SSMA para Oracle contém as seguintes alterações:  

-   Adicionado suporte para SQL Server 2016.
-   Conversão adicional das tabelas de arquivo morto de reversão do Oracle em tabelas temporais do SQL Server.
-   Conversão adicional da política de VPD Oracle conversão em objetos de política do SQL Server (segurança em nível de linha para Oracle).
-   Menor tempo de carregamento inicial para Oracle.
-   Analisador aprimorado e o resolvedor.
-   Removida a seleção de instalador para .net 2.0.
-   Dependência do pacote de extensão atualizada do .net 3.5 para o .net 4.0.
-   Fixa "salvar o projeto" e "Abrir projeto" comandos do Console SSMA.
-   Comando fixa "securepassword" para o Console do SSMA.
-   Correção de contagem de objetos para o carregamento inicial.
-   Corrigida a conversão de tipos de dados de caractere para Oracle.
-   Correção do bug nas configurações globais.
  
## <a name="march-2016"></a>Março de 2016  
A versão de visualização de março de 2016 do SSMA para Oracle contém as seguintes alterações:  
  
-   Adicionado suporte para migração para o SQL Server 2016.  
-   Adicionado suporte para migrar Oracle linha nível de segurança (com algumas limitações).  
-   Adicionado suporte para a migração de tabelas do Oracle na memória para o repositório de coluna do SQL Server.  
  
## <a name="january-2016"></a>Janeiro de 2016  
Janeiro de 2014 a versão de manutenção do SSMA para Oracle contém as seguintes alterações:  
  
-   Adicionado suporte para índices clusterizados.  
-   Corrigido consultas de esquema lenta Oracle (RFC 5076207).  
-   Fixa se conectar ao Azure do console.  
-   Item de Menu de Log de exibição adicionado para o SSMA (RFC 5706203). 
-   Telemetria adicionada.  
  
## <a name="july-2014"></a>Julho de 2014  
A versão de julho de 2014 do SSMA para Oracle contém as seguintes alterações:  
  
-   Adicionado suporte para o banco de dados do Azure SQL.  
-   Funcionalidade do pacote de extensão é movido para o esquema para oferecer suporte a banco de dados de SQL do Azure.  
-   Adicionado suporte para exibições materializadas Oracle.  
-   Tabelas com otimização de inclusão de suporte para a memória do SQL Server 2014.  
-   Melhorias de desempenho incluídos testado para bancos de dados com mais de 10 mil objetos.  
-   Aprimoramentos da interface do usuário adicionais para lidar com um grande número de objetos.  
-   Adicionado o realce de esquemas LOB "bem conhecidas".  
-   Incluíram melhorias de velocidade de conversão.  
-   Suporte adicionado para mostrar o objeto de conta na interface do usuário.  
-   Tamanho do relatório reduzida em mais de 25%.
-   Mensagens de erro aprimoradas para construções não analisadas.  
  
## <a name="april-2014"></a>Abril de 2014  
A versão de abril de 2014 do SSMA para Oracle contém as seguintes alterações:  
  
-   Adicionado suporte do MS SQL Server 2014.  
-   Adicionado suporte de otimização do Oracle 12 e consulta.  
-   Bugs corrigidos sobre conversão para o Azure.  
-   Bugs corrigidos sobre páginas de relatório invisível no Internet Explorer 10.  
  
## <a name="january-2012"></a>Janeiro de 2012  
A versão de janeiro de 2012 do SSMA para Oracle contém as seguintes alterações:  
  
-   Adicionado suporte para parâmetros de entrada RowType e RecordType adotou o padrão NULL.  
  
## <a name="july-2011"></a>Julho de 2011  
A versão de julho de 2011 do SSMA para Oracle contém as seguintes alterações:  
  
-   Adicionado suporte para conversão de sequência de Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gerador de sequência do "Denali".  
-   Melhor relatórios de erros durante a migração de dados.  
-   Melhor conversão de instrução usar palavras reservadas.  
-   Melhor conversão implícita do valor de data em uma função.  
  
## <a name="april-2011"></a>Abril de 2011  
A versão de abril de 2011 do SSMA para Oracle contém as seguintes alterações:  
  
-   Consolidados produto "SSMA para Oracle", que dá suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
-   Adicionado suporte para a conexão e a migração para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
-   Mecanismo de migração aprimorada de dados do lado do cliente, dando suporte a migração paralela de dados.  
-   Desempenho de migração de dados aprimorada com simples e Bulk logged modelos de recuperação.  
-   Adicionado suporte para compatibilidade com versões anteriores de projetos criados por versões anteriores do SSMA (v 4.0 e v 4.2).  
-   Adicionada a capacidade de instalar o SSMA para Oracle v 5.0 produtos lado a lado (SxS) com as versões mais antigas do SSMA (v 4.0 e v 4.2).  
-   Adicionado suporte para tipos definidos pelo usuário (inclui o subtipo, VARRAY, tabela ANINHADA, tabela de objetos e modo de exibição do objeto) e seus usos em blocos de PL/SQL com mensagens de erro especial de emissão de relatórios.  

## <a name="july-2010"></a>Julho de 2010  
A versão de julho de 2010 do SSMA para Oracle contém as seguintes alterações:  
  
-   Adicionado suporte para migração para o SQL Server 2008 R2.  
-   Adicionado um novo aplicativo de Console SSMA para execução de linha de comando.  
-   Adicionado suporte para migração de dados usando os mecanismos de migração de dados do lado do cliente e do servidor.  
-   Adicionado suporte para a instrução "SELECT personalizado" na migração de dados.  
-   Adicionado suporte para migração do Oracle 11g R2.  
  
## <a name="june-2008"></a>Junho de 2008  
A versão de junho de 2008 do SSMA para Oracle contém as seguintes alterações:  
  
-   Foram incluídos aperfeiçoamentos para o relatório de avaliação, incluindo informações adicionais sobre sinônimos, origem bruto para objetos analisável, painéis e remoção de logotipo do SQL Server e conservação de layout.  
-   Foram incluídos aperfeiçoamentos na conversão do objeto:  
    -   Pacotes DBMS_LOB, conversão de DBMS_SQL adicionado.  
    -   Une conversão revisado.  
    -   Modificação de conversão de registros e coleções, agora a conversão de registros em casos simples lançados por meio de variáveis separadas para cada campo.  
    -   Aperfeiçoamentos de implementação de registros e coleções.  
    -   Funções de agregação em janela adicionadas.  
    -   Cláusula ROLLUP/cubo adicionada.  
    -   Aperfeiçoamento de NEXTVAL/CURVAL.  
    -   Colunas de agrupamento na cláusula SET, conjuntos de agrupamentos e a ID de agrupamento foram adicionadas.  
    -   MESCLE instrução adicionada.  
    -   Suporte de novos tipos de data/hora e a conversão de registros e coleções como tipos de dados CLR adicionados.  
-   Adicionado novos recursos do avaliador. Tabelas agora podem ser testadas como objetos usando o testador, a ordem de chamada de vários objetos podem ser testados no caso de teste pode ser alterada, usuário pode testar procedimentos e funções com registros e coleções como parâmetros e retornar valores e dependências de um analisador foi adicionado para verificar somente tabelas usaram.  
  
## <a name="august-2007"></a>Agosto de 2007  
A versão de agosto de 2007 do SSMA para Oracle contém as seguintes alterações:  
  
-   Adicionado que um novo componente TESTER lhe permite criar, gerenciar e executar casos de teste para verificar o código SQL convertido.  
-   Adicionado suporte para conversão de subtipos Oracle, coleções e módulos locais foram adicionados para o conversor de SQL.  
-   Adicionado que um novo recurso de sincronização permite sincronizar objetos específicos com o banco de dados do SQL Server.  
-   Adicionadas novas opções de conversão.  
  
## <a name="april-2007"></a>Abril de 2007  
A versão de abril de 2007 do SSMA para Oracle foi a versão inicial.

