---
title: Transformação Dimensão de Alteração Lenta | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.slowlychangingdimtrans.f1
helpviewer_keywords:
- Slowly Changing Dimension transformation
- slowly changing dimensions
- SCD transformation
- updating slowly changing dimensions
ms.assetid: f8849151-c171-4725-bd25-f2c33a40f4fe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 18c269bfa245135e95a101d725ed4a592889e7a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62900196"
---
# <a name="slowly-changing-dimension-transformation"></a>transformação Dimensão de Alteração Lenta
  A transformação Dimensão de Alteração Lenta coordena a atualização e a inserção de registros em tabelas de dimensão do data warehouse. Por exemplo, você pode usar essa transformação para configurar as saídas de transformação que inserem e atualizam registros na tabela DimProduct do banco de dados OLAP da [!INCLUDE[ssSampleDBDWobject](../../../includes/sssampledbdwobject-md.md)] com dados da tabela Production.Products no banco de dados OLTP da AdventureWorks.  
  
> [!IMPORTANT]  
>  O Assistente para Dimensões de Alteração Lenta somente tem suporte para conexões ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 A transformação Dimensão de Alteração Lenta oferece as seguintes funcionalidades para gerenciar dimensões de alteração lenta:  
  
-   Corresponder linhas de entrada com linhas na tabela de pesquisa para identificar linhas novas e existentes.  
  
-   Identificar linhas de entrada que contêm alterações quando não são permitidas alterações.  
  
-   Identificar registros de membros deduzidos que exigem atualização.  
  
-   Identificar linhas de entrada que contêm alterações históricas que exigem inserção de registros novos e atualizar registros expirados.  
  
-   Detectar linhas de entrada que contêm alterações que exigem a atualização de registros existentes, incluindo registros expirados.  
  
 A transformação Dimensão de Alteração Lenta dá suporte a quatro tipos de alterações: atributo de alteração, atributo histórico, atributo fixo e membro deduzido.  
  
-   Alterar atributos de alteração substitui registros existentes. Esse tipo de alteração é equivalente a uma alteração do Tipo 1. A transformação Dimensão de Alteração Lenta dirige estas linhas a uma saída nomeada **Saída de Atualizações de Atributos de Alteração**.  
  
-   As alterações de atributos históricos criam registros novos em vez de atualizar registros existentes. A única alteração que é permitida em um registro existente é uma atualização de uma coluna que indica se o registro é atual ou expirado. Esse tipo de alteração é equivalente a uma alteração do Tipo 2. A transformação Dimensão de Alteração Lenta dirige estas linhas a duas saídas: **Saída de Inserções de Atributos Históricos** e **Nova Saída**.  
  
-   Alterações de atributo fixo indicam que o valor da coluna não deve ser alterado. A transformação Dimensão de Alteração Lenta detecta as alterações e pode direcionar as linhas com alterações a uma saída nomeada **Saída de Atributos Fixos**.  
  
-   O membro deduzido indica que a linha é um registro de membro deduzido na tabela de dimensão. Um membro deduzido existe quando uma tabela de fatos faz referência a um membro de dimensão que ainda não foi carregado. Um registro de membro deduzido mínimo é criado em antecipação a dados de dimensão relevantes, que são fornecidos em um carregamento subsequente dos dados de dimensão. A transformação Dimensão de Alteração Lenta direciona estas linhas a uma saída nomeada **Atualizações de Membros Deduzidos**. Quando os dados do membro deduzido são carregados, você pode atualizar o registro existente em vez de criar um novo.  
  
> [!NOTE]  
>  A transformação Dimensão de Alteração Lenta não oferece suporte a alterações do Tipo 3, que exigem alterações na tabela de dimensão. Ao identificar colunas com o tipo de atualização de atributo fixo, você pode capturar os valores de dados que são candidatos para alterações do Tipo 3.  
  
 Em tempo de execução, a transformação Dimensão de Alteração Lenta tenta inicialmente corresponder a linha de entrada a um registro na tabela de pesquisa. Se nenhuma correspondência for encontrada, a linha de entrada será um novo registro; portanto, a transformação Dimensão de Alteração Lenta não executará nenhum trabalho adicional e direcionará a linha para a **Nova Saída**.  
  
 Se uma correspondência é encontrada, a transformação Dimensão de Alteração Lenta detecta se a linha contém alterações. Se a linha contém alterações, a transformação Dimensão de Alteração Lenta identifica o tipo de atualização de cada coluna e direciona a linha para a **Saída de Atualizações de Atributos de Alteração**, a **Saída de Atributo Fixo**, a **Saída de Inserções de Atributos Históricos**ou a **Saída de Atualizações de Membro Deduzido**. Se houver uma linha inalterada, a transformação Dimensão de Alteração Lenta direcionará a linha para a **Saída Inalterada**.  
  
## <a name="slowly-changing-dimension-transformation-outputs"></a>Saídas de transformação Dimensão de Alteração Lenta  
 A transformação Dimensão de Alteração Lenta tem uma entrada e até seis saídas. Uma saída direciona uma linha ao subconjunto de fluxo de dados que corresponde aos requisitos de atualização e inserção da linha. Essa transformação não oferece suporte a uma saída de erro.  
  
 A tabela a seguir descreve as saídas de transformação e os requisitos de seus fluxos de dados subsequentes. Os requisitos descrevem o fluxo de dados que o Assistente de Dimensão da Alteração Lenta cria.  
  
|Saída|DESCRIÇÃO|Requisitos de fluxo de dados|  
|------------|-----------------|----------------------------|  
|**Saída de Atualizações de Atributos de Alteração**|O registro na tabela de pesquisa é atualizado. Esta saída é usada para linhas de atributos de alteração.|Uma transformação Comando OLE DB atualiza o registro usando uma instrução UPDATE.|  
|**Saída de Atributos Fixos**|Os valores em linhas que não devem ser alterados não correspondem a valores na tabela de pesquisa. Esta saída é usada para linhas de atributos fixos.|Nenhum fluxo de dados padrão é criado. Se a transformação está configurada para continuar depois de encontrar alterações em colunas de atributo fixo, você deve criar um fluxo de dados que capture essas linhas.|  
|**Saída de Inserções de Atributos Históricos**|A tabela de pesquisa contém pelo menos uma linha correspondente. A linha marcada como "atual" deve ser marcada agora como "expirada". Esta saída é usada para linhas de atributos históricos.|As transformações Colunas Derivadas criam colunas para a linha expirada e os indicadores de linha atuais. Uma transformação Comando OLE DB atualiza o registro que deve ser marcado agora como "expirado." A linha com os valores da nova coluna é direcionada para a Nova Saída, na qual a linha é inserida e marcada como "atual".|  
|**Saída de Atualizações de Membro Deduzido**|Linhas para membros de dimensão deduzidos são inseridas. Esta saída é usada para linhas de membro deduzido.|Uma transformação Comando OLE DB atualiza o registro usando uma instrução SQL UPDATE.|  
|**Nova Saída**|A tabela de pesquisa não contém linhas correspondentes. A linha é adicionada à tabela de dimensão. Esta saída é usada para novas linhas e alterações em linhas de atributos históricos.|Uma transformação Coluna Derivada define o indicador da linha atual e um destino de OLE DB insere a linha.|  
|**Saída Inalterada**|Os valores na tabela de pesquisa correspondem aos valores de linha. Esta saída é usada para linhas inalteradas.|Nenhum fluxo de dados padrão é criado porque a transformação Dimensão de Alteração Lenta não executa nenhum trabalho. Se você quiser capturar estas linhas, deverá criar um fluxo de dados para esta saída.|  
  
## <a name="business-keys"></a>Chaves de negócio  
 A transformação Dimensão de Alteração Lenta exige pelo menos uma coluna de chave de negócio.  
  
 A transformação Dimensão de Alteração Lenta não oferece suporte a chaves de negócio nulas. Se os dados incluem linhas nas quais a coluna de chave de negócio é nula, essas linhas devem ser removidas do fluxo de dados. Você pode usar a transformação Divisão Condicional para filtrar linhas cujas colunas de chaves de negócio contêm valores nulos. Para obter mais informações, consulte [Conditional Split Transformation](conditional-split-transformation.md).  
  
## <a name="optimizing-the-performance-of-the-slowly-changing-dimension-transformation"></a>Otimizando o desempenho da transformação Dimensão de Alteração Lenta  
 Para obter sugestões de como melhorar o desempenho da transformação Dimensão de Alteração Lenta, consulte [Recursos de desempenho de fluxo de dados](../data-flow-performance-features.md).  
  
## <a name="troubleshooting-the-slowly-changing-dimension-transformation"></a>Solucionando problemas da transformação Dimensão de Alteração Lenta  
 Você pode efetuar log das chamadas que a transformação Dimensão de Alteração Lenta faz a provedores de dados externos. Você pode usar essa capacidade de log para solucionar problemas de conexões, comandos e consultas a fontes de dados externas realizadas pela transformação Dimensão de Alteração Lenta. Para efetuar log das chamadas feitas pela transformação Dimensão de Alteração Lenta aos provedores de dados externos, habilite o log do pacote e selecione o evento **Diagnóstico** no nível de pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-slowly-changing-dimension-transformation"></a>Configurando a transformação Dimensão de Alteração Lenta  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas de Transformação](transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="configuring-the-slowly-changing-dimension-transformation-outputs"></a>Configurando saídas da transformação Dimensão de Alteração Lenta  
 Coordenar a atualização e a inserção de registros em tabelas de dimensão pode ser uma tarefa complexa, especialmente se ambas as alterações, Tipo 1 e Tipo 2, são usadas. [!INCLUDE[ssIS](../../../includes/ssis-md.md)] O Designer oferece dois modos de configurar o suporte a dimensões de alteração lenta:  
  
-   A caixa de diálogo **Editor Avançado** , na qual você seleciona uma conexão, define propriedades de componentes comuns e personalizadas, escolhe colunas de entrada e define propriedades de coluna nas seis saídas. Para concluir a tarefa de configurar o suporte a uma dimensão de alteração lenta, você deve criar manualmente o fluxo de dados para as saídas usadas pela transformação Dimensão de Alteração Lenta. Para obter mais informações, consulte [Data Flow](../data-flow.md).  
  
-   O Assistente para Carregar Dimensão, que guia você pelas etapas de configuração da transformação Dimensão de Alteração Lenta e de criação do fluxo de dados para saídas de transformação. Para alterar a configuração de dimensões de alteração lenta, execute novamente o Assistente para Carregar Dimensão. Para obter mais informações, consulte [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [Otimizando o Assistente de Dimensão Variável Lentamente](https://go.microsoft.com/fwlink/?LinkId=199481), em blogs.msdn.com.  
  
  
