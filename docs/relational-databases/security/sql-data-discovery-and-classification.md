---
title: Descoberta e classificação de dados SQL | Microsoft Docs
description: Descoberta e classificação de dados SQL
documentationcenter: ''
ms.reviewer: carlrab
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.prod_service: sql-database,sql
ms.custom: security
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 02/13/2018
ms.author: giladm
author: giladm
manager: shaik
ms.openlocfilehash: 96861baa7fa28ef9f16f35c13f26327b824b44cc
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926327"
---
# <a name="sql-data-discovery-and-classification"></a>Descoberta e classificação de dados SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O recurso Descoberta e classificação de dados SQL apresenta uma nova ferramenta interna do SSMS (SQL Server Management Studio) para **descobrir**, **classificar**, **rotular** & **relatar** os dados confidenciais em seus bancos de dados.
A descoberta e a classificação dos dados mais confidenciais (de negócios, financeiros, de serviços de saúde, etc.) podem desempenhar um papel fundamental na dimensão da proteção de informações organizacionais. Esse recurso pode funcionar como a infraestrutura para:
* Ajudar a atender aos padrões de privacidade de dados.
* Controlar o acesso a e fortalecer a segurança de bancos de dados/colunas que contêm dados altamente confidenciais.

> [!NOTE]
> O recurso descoberta e classificação de dados é **compatível com o SQL Server 2008 e posteriores**. Para o Banco de Dados SQL do Azure, confira [Descoberta e Classificação de Dados do Banco de Dados SQL do Azure](https://go.microsoft.com/fwlink/?linkid=866265).

## <a id="subheading-1"></a>Visão geral
O recurso Descoberta e classificação de dados apresenta um conjunto de serviços avançados, formando um novo paradigma de Proteção de Informações do SQL que visa a proteção dos dados, não apenas do banco de dados:
* **Descoberta e recomendações** – o mecanismo de classificação verifica o banco de dados e identifica colunas que contenham dados possivelmente confidenciais. Em seguida, ele fornece uma maneira fácil de examinar e aplicar as recomendações de classificação apropriada, bem como de classificar as colunas manualmente.
* **Definição de rótulos** – rótulos de classificação de confidencialidade podem ser marcados com persistência em colunas.
* **Visibilidade** – o estado de classificação do banco de dados pode ser exibido em um relatório detalhado que pode ser impresso/exportado para ser usado para fins de auditoria e conformidade, bem como para outras necessidades.

## <a id="subheading-2"></a>Descobrindo, classificando e rotulando colunas confidenciais
A seção a seguir descreve as etapas para descobrir, classificar e rotular colunas que contenham dados confidenciais no banco de dados, bem como exibir o estado atual de classificação do banco de dados e exportar relatórios.

A classificação inclui dois atributos de metadados:
* Rótulos – os atributos de classificação principais, usados para definir o nível de confidencialidade dos dados armazenados na coluna.  
* Tipos de informações – fornecem uma granularidade adicional para o tipo dos dados armazenados na coluna.

<br>
**Para classificar o banco de dados do SQL Server:**

1. No SSMS (SQL Server Management Studio), conecte-se ao SQL Server.

2. No Pesquisador de Objetos do SSMS, clique com botão direito do mouse no banco de dados que você deseja classificar e escolha **Tarefas** > **Classificar Dados...**.

    ![Painel de navegação][1]

3. O mecanismo de classificação verifica o banco de dados em busca de colunas que contenham dados possivelmente confidenciais e fornece uma lista de **classificações de coluna recomendadas**:

    * Para exibir a lista de classificações de coluna recomendadas, clique na caixa de notificação de recomendações na parte superior ou no painel de recomendações na parte inferior da janela:

        ![Painel de navegação][2]

        ![Painel de navegação][3]

    * Examine a lista de recomendações:
        * Para aceitar uma recomendação para uma coluna específica, marque a caixa de seleção na coluna à esquerda da linha relevante. Você também pode marcar *todas as recomendações* como aceitas, marcando a caixa de seleção no cabeçalho da tabela de recomendações.

        * Também é possível alterar o tipo de informações e o rótulo de confidencialidade recomendados usando as caixas suspensas.        

        ![Painel de navegação][4]

    * Para aplicar as recomendações selecionadas, clique no botão **Aceitar recomendações selecionadas** azul.

        ![Painel de navegação][5]

4. Você também pode **classificar manualmente** as colunas como uma alternativa ou, além da classificação de recomendação:

    * Clicar em **Adicionar classificação** no menu superior da janela.

        ![Painel de navegação][6]

    * Na janela de contexto que é aberta, selecionar o esquema > a tabela > a coluna que você deseja classificar e, em seguida, o tipo de informações e o rótulo confidencialidade. Em seguida, clicar no botão **Adicionar classificação** azul na parte inferior da janela do contexto.

        ![Painel de navegação][7]

5. Para concluir sua classificação e definir um rótulo (uma marca) persistente para as colunas do banco de dados com os novos metadados de classificação, clique em **Salvar** no menu superior da janela.

    ![Painel de navegação][8]


6. Para gerar um relatório com um resumo completo do estado de classificação do banco de dados, clique em **Exibir Relatório** no menu superior da janela.

    ![Painel de navegação][9]

    ![Painel de navegação][10]


## <a id="subheading-3"></a>Acessando os metadados de classificação

Os metadados de classificação para *Tipos de informação* e *Rótulos de confidencialidade* são armazenados nas seguintes Propriedades estendidas: 
* sys_information_type_name
* sys_sensitivity_label_name

Os metadados podem ser acessados usando a exibição do catálogo das Propriedades estendidas [sys.extended_properties](https://docs.microsoft.com/en-us/sql/relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties).

O exemplo de código a seguir retorna todas as colunas classificadas com suas classificações correspondentes:

```sql
SELECT
    schema_name(O.schema_id) AS schema_name,
    O.NAME AS table_name,
    C.NAME AS column_name,
    information_type,
    sensitivity_label 
FROM
    (
        SELECT
            IT.major_id,
            IT.minor_id,
            IT.information_type,
            L.sensitivity_label 
        FROM
        (
            SELECT
                major_id,
                minor_id,
                value AS information_type 
            FROM sys.extended_properties 
            WHERE NAME = 'sys_information_type_name'
        ) IT 
        FULL OUTER JOIN
        (
            SELECT
                major_id,
                minor_id,
                value AS sensitivity_label 
            FROM sys.extended_properties 
            WHERE NAME = 'sys_sensitivity_label_name'
        ) L 
        ON IT.major_id = L.major_id AND IT.minor_id = L.minor_id
    ) EP
    JOIN sys.objects O
    ON  EP.major_id = O.object_id 
    JOIN sys.columns C 
    ON  EP.major_id = C.object_id AND EP.minor_id = C.column_id
```

## <a id="subheading-4"></a>Próximas etapas

Para o Banco de Dados SQL do Azure, confira [Descoberta e Classificação de Dados do Banco de Dados SQL do Azure](https://go.microsoft.com/fwlink/?linkid=866265).

Considere proteger suas colunas confidenciais aplicando mecanismos de segurança no nível da coluna:

* [Máscara de Dados Dinâmicos](https://docs.microsoft.com/en-us/sql/relational-databases/security/dynamic-data-masking) para ofuscar as colunas confidenciais em uso.
* [Always Encrypted](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/always-encrypted-database-engine) para criptografar as colunas confidenciais em repouso.

<!--Anchors-->
[SQL Data Discovery & Classification overview]: #subheading-1
[Discovering, classifying & labeling sensitive columns]: #subheading-2
[Accessing the classification metadata]: #subheading-3
[Next Steps]: #subheading-4

<!--Image references-->
[1]: ./media/sql-data-discovery-and-classification/1_data_classification_explorer_menu.png
[2]: ./media/sql-data-discovery-and-classification/2_recommendations_notification_box.png
[3]: ./media/sql-data-discovery-and-classification/3_recommendations_panel.png
[4]: ./media/sql-data-discovery-and-classification/4_recommendations.png
[5]: ./media/sql-data-discovery-and-classification/5_accept_recommendations_button.png
[6]: ./media/sql-data-discovery-and-classification/6_add_classification_button.png
[7]: ./media/sql-data-discovery-and-classification/7_manual_classification.png
[8]: ./media/sql-data-discovery-and-classification/8_save.png
[9]: ./media/sql-data-discovery-and-classification/9_view_report.png
[10]: ./media/sql-data-discovery-and-classification/10_report.png
